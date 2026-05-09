# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：中断处理程序中调用睡眠函数

**问题**：在中断上下文（顶半部）中调用可能睡眠的函数，导致内核死锁或崩溃。

❌ **Before（错误做法）**
```c
// 错误：ISR中调用可能睡眠的函数
static irqreturn_t my_irq_handler(int irq, void *dev_id) {
    struct my_device *dev = dev_id;
    
    // 错误！kmalloc(GFP_KERNEL)可能睡眠
    char *buf = kmalloc(1024, GFP_KERNEL);
    
    // 错误！mutex_lock可能睡眠
    mutex_lock(&dev->lock);
    
    // 处理数据...
    
    mutex_unlock(&dev->lock);
    kfree(buf);
    return IRQ_HANDLED;
}
```

✅ **After（正确做法）**
```c
// 正确：ISR中只处理紧急事务，复杂工作放到workqueue
static irqreturn_t my_irq_handler(int irq, void *dev_id) {
    struct my_device *dev = dev_id;
    
    // 1. 读取状态寄存器（快速操作）
    u32 status = readl(dev->regs + STATUS_REG);
    
    // 2. 清除中断（快速操作）
    writel(status, dev->regs + STATUS_REG);
    
    // 3. 将工作提交到workqueue（不睡眠）
    schedule_work(&dev->work);
    
    return IRQ_HANDLED;
}

static void my_work_handler(struct work_struct *work) {
    struct my_device *dev = container_of(work, struct my_device, work);
    
    // 在进程上下文中，可以睡眠
    char *buf = kmalloc(1024, GFP_KERNEL);  // 可以睡眠
    
    mutex_lock(&dev->lock);  // 可以睡眠
    // 处理数据...
    mutex_unlock(&dev->lock);
    
    kfree(buf);
}
```

**原因**：中断上下文不是进程上下文，没有对应的task_struct，因此不能睡眠。睡眠会导致调度器无法找到下一个运行的进程，系统死锁。

## Gotcha 2：忽略内核API返回值

**问题**：调用内核API时不检查返回值，导致后续代码在错误状态下运行，引发空指针解引用或资源泄漏。

❌ **Before（错误做法）**
```c
// 错误：不检查返回值
static int my_probe(struct platform_device *pdev) {
    struct my_device *dev;
    
    dev->regs = devm_ioremap_resource(&pdev->dev, res);  // 可能失败！
    // 如果ioremap失败，dev->regs为NULL，后续writel崩溃
    
    writel(0x1, dev->regs + CTRL_REG);  // 空指针解引用！
    
    devm_request_irq(&pdev->dev, irq, my_handler, 0, "mydev", dev);  // 可能失败！
    // 如果request_irq失败，中断未注册，但驱动继续运行
    
    return 0;
}
```

✅ **After（正确做法）**
```c
// 正确：检查所有返回值
static int my_probe(struct platform_device *pdev) {
    struct my_device *dev;
    int ret;
    
    dev->regs = devm_ioremap_resource(&pdev->dev, res);
    if (IS_ERR(dev->regs)) {
        dev_err(&pdev->dev, "Failed to ioremap\n");
        return PTR_ERR(dev->regs);
    }
    
    writel(0x1, dev->regs + CTRL_REG);
    
    ret = devm_request_irq(&pdev->dev, irq, my_handler, 0, "mydev", dev);
    if (ret) {
        dev_err(&pdev->dev, "Failed to request irq: %d\n", ret);
        return ret;
    }
    
    return 0;
}
```

**原因**：内核资源分配可能失败（内存不足、资源冲突等）。不检查返回值会导致后续代码在无效资源上操作，引发空指针解引用、资源泄漏或数据损坏。

## Gotcha 3：手动管理资源导致泄漏

**问题**：驱动中手动分配资源（kmalloc、ioremap、request_irq），但在出错路径或remove时遗漏释放，导致资源泄漏。

❌ **Before（错误做法）**
```c
// 错误：手动管理资源，容易遗漏释放
static int my_probe(struct platform_device *pdev) {
    void __iomem *regs;
    int irq;
    
    regs = ioremap(res->start, resource_size(res));
    if (!regs)
        return -ENOMEM;
    
    irq = platform_get_irq(pdev, 0);
    if (irq < 0)
        return irq;  // 错误！regs未释放，内存泄漏
    
    ret = request_irq(irq, my_handler, 0, "mydev", NULL);
    if (ret)
        return ret;  // 错误！regs未释放，内存泄漏
    
    // ...
    return 0;
}

static int my_remove(struct platform_device *pdev) {
    // 错误！忘记释放regs和irq
    return 0;
}
```

✅ **After（正确做法）**
```c
// 正确：使用devm_系列函数自动管理资源
static int my_probe(struct platform_device *pdev) {
    void __iomem *regs;
    int irq, ret;
    
    regs = devm_ioremap_resource(&pdev->dev, res);
    if (IS_ERR(regs))
        return PTR_ERR(regs);  // 自动释放，无泄漏
    
    irq = platform_get_irq(pdev, 0);
    if (irq < 0)
        return irq;  // 自动释放regs，无泄漏
    
    ret = devm_request_irq(&pdev->dev, irq, my_handler, 0, "mydev", NULL);
    if (ret)
        return ret;  // 自动释放regs和irq，无泄漏
    
    // ...
    return 0;
}

static int my_remove(struct platform_device *pdev) {
    // devm_资源自动释放，无需手动操作
    return 0;
}
```

**原因**：手动资源管理容易在错误路径中遗漏释放。devm_系列函数将资源与device绑定，设备移除时自动释放，避免泄漏。

## Gotcha 4：无锁访问共享数据

**问题**：多线程或中断/进程并发访问共享数据时未加锁保护，导致竞态条件和数据损坏。

❌ **Before（错误做法）**
```c
// 错误：无锁访问共享数据
struct my_device {
    int count;
    struct list_head list;
};

// 进程上下文写入
static ssize_t my_write(struct file *file, const char __user *buf, 
                        size_t count, loff_t *pos) {
    dev->count++;  // 非原子操作！竞态条件
    list_add(&new_item, &dev->list);  // 非原子操作！链表损坏
    return count;
}

// 中断上下文读取
static irqreturn_t my_irq_handler(int irq, void *dev_id) {
    printk("count = %d\n", dev->count);  // 可能读到不一致的值
    return IRQ_HANDLED;
}
```

✅ **After（正确做法）**
```c
// 正确：根据上下文选择锁类型
struct my_device {
    int count;
    struct list_head list;
    spinlock_t lock;  // 用于中断上下文
    struct mutex mtx;  // 用于进程上下文
};

// 进程上下文：使用mutex（可以睡眠）
static ssize_t my_write(struct file *file, const char __user *buf,
                        size_t count, loff_t *pos) {
    mutex_lock(&dev->mtx);
    dev->count++;
    list_add(&new_item, &dev->list);
    mutex_unlock(&dev->mtx);
    return count;
}

// 中断上下文：使用spinlock（不能睡眠）
static irqreturn_t my_irq_handler(int irq, void *dev_id) {
    unsigned long flags;
    
    spin_lock_irqsave(&dev->lock, flags);  // 保存中断状态并关中断
    printk("count = %d\n", dev->count);
    spin_unlock_irqrestore(&dev->lock, flags);  // 恢复中断状态
    
    return IRQ_HANDLED;
}
```

**原因**：并发访问共享数据必须加锁保护。进程上下文用mutex，中断上下文用spinlock。错误选择锁类型会导致死锁（spinlock中睡眠）或竞态条件（无锁访问）。

## Gotcha 5：设备树节点compatible不匹配

**问题**：驱动中的compatible字符串与设备树节点不匹配，导致驱动probe失败。

❌ **Before（错误做法）**
```c
// 驱动代码
static const struct of_device_id my_of_match[] = {
    { .compatible = "mycompany,mydevice-v1" },
    { }
};

// 设备树
mydevice@10000000 {
    compatible = "mycompany,mydevice";  // 缺少版本号！
    reg = <0x10000000 0x1000>;
};
```

✅ **After（正确做法）**
```c
// 驱动代码：支持多个版本
static const struct of_device_id my_of_match[] = {
    { .compatible = "mycompany,mydevice-v1" },
    { .compatible = "mycompany,mydevice-v2" },
    { .compatible = "mycompany,mydevice" },  // 兼容无版本号
    { }
};
MODULE_DEVICE_TABLE(of, my_of_match);

// 设备树
mydevice@10000000 {
    compatible = "mycompany,mydevice-v1";
    reg = <0x10000000 0x1000>;
};
```

**原因**：设备树绑定要求compatible字符串精确匹配。驱动应支持多个版本，设备树应使用最具体的compatible。不匹配会导致驱动无法绑定设备。
