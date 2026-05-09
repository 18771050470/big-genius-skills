# 技术交付物模板

> 以下模板供 Agent 在输出技术交付物时参考。根据实际场景选择合适模板，不必全部使用。

---

## 交付物模板 1：字符设备驱动框架

```c
/*
 * [驱动名称] - [功能描述]
 * 
 * 硬件平台：[平台名称]
 * 内核版本：[版本]
 */

#include <linux/module.h>
#include <linux/platform_device.h>
#include <linux/fs.h>
#include <linux/cdev.h>
#include <linux/uaccess.h>
#include <linux/io.h>
#include <linux/interrupt.h>
#include <linux/mutex.h>

#define DEVICE_NAME "mydevice"
#define CLASS_NAME "myclass"
#define BUFFER_SIZE 1024

struct my_device {
    void __iomem *regs;
    int irq;
    struct cdev cdev;
    struct device *device;
    struct class *class;
    dev_t devno;
    char buffer[BUFFER_SIZE];
    struct mutex lock;
};

/* 文件操作 */
static int my_open(struct inode *inode, struct file *file)
{
    struct my_device *dev = container_of(inode->i_cdev, struct my_device, cdev);
    file->private_data = dev;
    return 0;
}

static int my_release(struct inode *inode, struct file *file)
{
    return 0;
}

static ssize_t my_read(struct file *file, char __user *buf, 
                       size_t count, loff_t *pos)
{
    struct my_device *dev = file->private_data;
    ssize_t ret;
    
    mutex_lock(&dev->lock);
    
    if (count > BUFFER_SIZE)
        count = BUFFER_SIZE;
    
    // 从硬件读取数据到buffer
    // ...
    
    if (copy_to_user(buf, dev->buffer, count)) {
        ret = -EFAULT;
        goto out;
    }
    
    ret = count;
out:
    mutex_unlock(&dev->lock);
    return ret;
}

static ssize_t my_write(struct file *file, const char __user *buf,
                        size_t count, loff_t *pos)
{
    struct my_device *dev = file->private_data;
    ssize_t ret;
    
    mutex_lock(&dev->lock);
    
    if (count > BUFFER_SIZE)
        count = BUFFER_SIZE;
    
    if (copy_from_user(dev->buffer, buf, count)) {
        ret = -EFAULT;
        goto out;
    }
    
    // 将buffer数据写入硬件
    // ...
    
    ret = count;
out:
    mutex_unlock(&dev->lock);
    return ret;
}

static long my_ioctl(struct file *file, unsigned int cmd, unsigned long arg)
{
    struct my_device *dev = file->private_data;
    int ret = 0;
    
    switch (cmd) {
    case MY_IOCTL_CMD1:
        // 处理命令1
        break;
    case MY_IOCTL_CMD2:
        // 处理命令2
        break;
    default:
        ret = -EINVAL;
    }
    
    return ret;
}

static const struct file_operations my_fops = {
    .owner = THIS_MODULE,
    .open = my_open,
    .release = my_release,
    .read = my_read,
    .write = my_write,
    .unlocked_ioctl = my_ioctl,
};

/* 中断处理 */
static irqreturn_t my_irq_handler(int irq, void *dev_id)
{
    struct my_device *dev = dev_id;
    
    // 读取状态寄存器
    u32 status = readl(dev->regs + STATUS_REG);
    
    // 清除中断
    writel(status, dev->regs + STATUS_REG);
    
    // 处理中断
    // ...
    
    return IRQ_HANDLED;
}

/* Platform驱动 */
static int my_probe(struct platform_device *pdev)
{
    struct my_device *dev;
    struct resource *res;
    int ret, irq;
    
    dev = devm_kzalloc(&pdev->dev, sizeof(*dev), GFP_KERNEL);
    if (!dev)
        return -ENOMEM;
    
    mutex_init(&dev->lock);
    
    /* 获取资源 */
    res = platform_get_resource(pdev, IORESOURCE_MEM, 0);
    if (!res) {
        dev_err(&pdev->dev, "Failed to get memory resource\n");
        return -ENODEV;
    }
    
    dev->regs = devm_ioremap_resource(&pdev->dev, res);
    if (IS_ERR(dev->regs))
        return PTR_ERR(dev->regs);
    
    irq = platform_get_irq(pdev, 0);
    if (irq < 0)
        return irq;
    
    ret = devm_request_irq(&pdev->dev, irq, my_irq_handler, 0, 
                           DEVICE_NAME, dev);
    if (ret) {
        dev_err(&pdev->dev, "Failed to request irq\n");
        return ret;
    }
    dev->irq = irq;
    
    /* 注册字符设备 */
    ret = alloc_chrdev_region(&dev->devno, 0, 1, DEVICE_NAME);
    if (ret) {
        dev_err(&pdev->dev, "Failed to alloc chrdev region\n");
        return ret;
    }
    
    cdev_init(&dev->cdev, &my_fops);
    dev->cdev.owner = THIS_MODULE;
    
    ret = cdev_add(&dev->cdev, dev->devno, 1);
    if (ret) {
        dev_err(&pdev->dev, "Failed to add cdev\n");
        goto err_chrdev;
    }
    
    dev->class = class_create(THIS_MODULE, CLASS_NAME);
    if (IS_ERR(dev->class)) {
        ret = PTR_ERR(dev->class);
        goto err_cdev;
    }
    
    dev->device = device_create(dev->class, NULL, dev->devno, NULL, 
                                DEVICE_NAME);
    if (IS_ERR(dev->device)) {
        ret = PTR_ERR(dev->device);
        goto err_class;
    }
    
    platform_set_drvdata(pdev, dev);
    
    dev_info(&pdev->dev, "Device probed successfully\n");
    return 0;

err_class:
    class_destroy(dev->class);
err_cdev:
    cdev_del(&dev->cdev);
err_chrdev:
    unregister_chrdev_region(dev->devno, 1);
    return ret;
}

static int my_remove(struct platform_device *pdev)
{
    struct my_device *dev = platform_get_drvdata(pdev);
    
    device_destroy(dev->class, dev->devno);
    class_destroy(dev->class);
    cdev_del(&dev->cdev);
    unregister_chrdev_region(dev->devno, 1);
    
    return 0;
}

static const struct of_device_id my_of_match[] = {
    { .compatible = "mycompany,mydevice" },
    { }
};
MODULE_DEVICE_TABLE(of, my_of_match);

static struct platform_driver my_driver = {
    .probe = my_probe,
    .remove = my_remove,
    .driver = {
        .name = DEVICE_NAME,
        .of_match_table = my_of_match,
    },
};

module_platform_driver(my_driver);

MODULE_AUTHOR("Your Name");
MODULE_DESCRIPTION("My Device Driver");
MODULE_LICENSE("GPL");
```

---

## 交付物模板 2：设备树节点

```dts
// 设备树节点示例：[设备名称]

/ {
    // 根节点下的设备
    mydevice: mydevice@10000000 {
        compatible = "mycompany,mydevice-v1";
        reg = <0x10000000 0x1000>;
        interrupts = <0 42 IRQ_TYPE_LEVEL_HIGH>;
        clocks = <&clk_controller 24>;
        clock-names = "core";
        dmas = <&dma_controller 0>;
        dma-names = "rx";
        pinctrl-names = "default";
        pinctrl-0 = <&mydevice_pins>;
        status = "okay";
    };
};

&pinctrl {
    // 引脚配置
    mydevice_pins: mydevice-pins {
        mux {
            groups = "uart0_pins";
            function = "uart0";
        };
        
        conf {
            pins = "PA0", "PA1";
            drive-strength = <8>;
            bias-pull-up;
        };
    };
};

&dma_controller {
    // DMA配置
    mydevice_dma: dma-channel@0 {
        compatible = "mycompany,dma-channel";
        reg = <0>;
        interrupts = <0 43 IRQ_TYPE_LEVEL_HIGH>;
    };
};
```

---

## 交付物模板 3：驱动调试记录

```markdown
# 驱动调试记录：[驱动名称]

## 环境信息
- **日期**：[日期]
- **内核版本**：[版本]
- **硬件平台**：[平台]
- **交叉编译器**：[版本]

## 调试日志

### 加载驱动
```
[    1.234567] mydevice: loading out-of-tree module taints kernel.
[    1.234789] mydevice 10000000.mydevice: Device probed successfully
[    1.234901] mydevice 10000000.mydevice: IRQ 42 registered
```

### 设备注册
```
$ ls /dev/mydevice
/dev/mydevice

$ ls /sys/class/myclass/mydevice/
dev    power    subsystem    uevent
```

### 功能测试

#### 读写测试
```bash
# 写入数据
echo "test data" > /dev/mydevice

# 读取数据
cat /dev/mydevice
test data
```

#### 中断测试
```
# 触发中断后查看/proc/interrupts
$ cat /proc/interrupts | grep mydevice
 42:     1234          0  mydevice  10000000.mydevice
```

#### 性能测试
```bash
# 测试读写速度
dd if=/dev/zero of=/dev/mydevice bs=1K count=1000
# 结果：速度 [X] MB/s
```

## 问题与解决

| 问题 | 现象 | 原因 | 解决方法 | 状态 |
|------|------|------|---------|------|
| [问题1] | [现象1] | [原因1] | [方法1] | ✅/❌ |
| [问题2] | [现象2] | [原因2] | [方法2] | ✅/❌ |

## 性能数据

| 指标 | 目标 | 实测 | 状态 |
|------|------|------|------|
| 中断延迟 | < 100μs | [X] μs | ✅/❌ |
| 读写速度 | > 10MB/s | [X] MB/s | ✅/❌ |
| CPU占用 | < 10% | [X]% | ✅/❌ |

## 结论
- **功能完整**：✅/❌
- **性能达标**：✅/❌
- **可交付**：✅/❌
```

---

## 交付物模板 4：寄存器映射表

```markdown
# 寄存器映射：[设备名称]

## 寄存器概览

| 偏移地址 | 名称 | 类型 | 宽度 | 复位值 | 说明 |
|---------|------|------|------|--------|------|
| 0x00 | CTRL | R/W | 32 | 0x00000000 | 控制寄存器 |
| 0x04 | STATUS | R | 32 | 0x00000000 | 状态寄存器 |
| 0x08 | DATA | R/W | 32 | 0x00000000 | 数据寄存器 |
| 0x0C | INT_EN | R/W | 32 | 0x00000000 | 中断使能 |
| 0x10 | INT_STAT | R/W | 32 | 0x00000000 | 中断状态 |
| 0x14 | BAUD | R/W | 32 | 0x00000000 | 波特率配置 |

## 寄存器详细说明

### CTRL (0x00) - 控制寄存器

| 位 | 名称 | 类型 | 说明 |
|----|------|------|------|
| 0 | EN | R/W | 模块使能：1=使能，0=禁用 |
| 1 | MODE | R/W | 工作模式：0=模式A，1=模式B |
| 2 | DMA_EN | R/W | DMA使能：1=使能DMA传输 |
| 3 | INT_EN | R/W | 中断使能：1=使能中断 |
| 7:4 | RESERVED | R | 保留，读为0 |
| 31:8 | CLK_DIV | R/W | 时钟分频系数 |

### STATUS (0x04) - 状态寄存器

| 位 | 名称 | 类型 | 说明 |
|----|------|------|------|
| 0 | BUSY | R | 忙标志：1=正在传输 |
| 1 | DONE | R | 完成标志：1=传输完成 |
| 2 | ERROR | R | 错误标志：1=发生错误 |
| 3 | FIFO_EMPTY | R | FIFO空标志 |
| 4 | FIFO_FULL | R | FIFO满标志 |
| 7:5 | RESERVED | R | 保留 |
| 15:8 | FIFO_LEVEL | R | FIFO当前数据量 |

## 配置示例

```c
// 使能模块，配置时钟分频
writel(0x0000010F, regs + CTRL);  // EN=1, MODE=1, CLK_DIV=15

// 使能中断
writel(0x00000003, regs + INT_EN);  // 使能DONE和ERROR中断

// 读取状态
u32 status = readl(regs + STATUS);
if (status & (1 << 2)) {
    // 处理错误
}
```
```
