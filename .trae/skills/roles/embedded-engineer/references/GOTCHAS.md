# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：在中断中使用阻塞操作

**问题**：在ISR中调用阻塞函数（如printf、HAL_Delay、OS信号量获取），导致中断响应延迟或系统死锁。

❌ **Before（错误做法）**
```c
// 错误：ISR中执行阻塞操作
void TIM2_IRQHandler(void) {
    HAL_TIM_IRQHandler(&htim2);
    printf("Timer triggered\n");  // 阻塞！printf可能用到中断，导致嵌套混乱
    HAL_Delay(100);              // 阻塞！Delay依赖SysTick中断，但当前在中断中
}
```

✅ **After（正确做法）**
```c
// 正确：ISR中只设置标志，主循环处理
volatile uint8_t timer_flag = 0;

void TIM2_IRQHandler(void) {
    HAL_TIM_IRQHandler(&htim2);
    timer_flag = 1;  // 仅设置标志
}

// 主循环
while (1) {
    if (timer_flag) {
        timer_flag = 0;
        printf("Timer triggered\n");  // 在主循环中执行
        process_timer_event();        // 处理业务逻辑
    }
}
```

**原因**：ISR中不能使用阻塞操作，因为中断上下文没有任务调度，阻塞会导致系统卡死。printf涉及UART中断，Delay依赖SysTick，都会引起中断嵌套问题。

## Gotcha 2：忽略栈溢出

**问题**：任务栈空间不足，导致栈溢出，破坏其他任务或全局变量，系统行为异常。

❌ **Before（错误做法）**
```c
// 错误：栈空间不足
void task_function(void *pvParameters) {
    uint8_t large_buffer[2048];  // 局部大数组，占用栈空间
    process_data(large_buffer);
}

// FreeRTOS配置
#define TASK_STACK_SIZE 1024  // 仅1KB栈，但局部数组就2KB
```

✅ **After（正确做法）**
```c
// 正确：静态分配大数组，增加栈空间
static uint8_t large_buffer[2048];  // 静态分配，不占栈

void task_function(void *pvParameters) {
    process_data(large_buffer);
}

// FreeRTOS配置
#define TASK_STACK_SIZE 4096  // 4KB栈，预留50%余量

// 栈监控
void vApplicationStackOverflowHook(TaskHandle_t xTask, char *pcTaskName) {
    printf("Stack overflow in task: %s\n", pcTaskName);
    Error_Handler();
}
```

**原因**：嵌入式系统内存有限，栈溢出会破坏相邻内存区域。大数组应静态分配或动态分配（内存池），并启用栈溢出检测。

## Gotcha 3：未初始化指针或变量

**问题**：使用未初始化的指针或变量，导致不可预测的行为或系统崩溃。

❌ **Before（错误做法）**
```c
// 错误：未初始化指针
uint8_t *buffer;
HAL_UART_Receive(&huart1, buffer, 10, 1000);  // buffer未初始化，指向随机地址

// 错误：未初始化变量
uint32_t count;
for (int i = 0; i < count; i++) {  // count未初始化，循环次数随机
    // ...
}
```

✅ **After（正确做法）**
```c
// 正确：初始化指针和变量
uint8_t buffer[64];
HAL_UART_Receive(&huart1, buffer, 10, 1000);

// 正确：初始化变量
uint32_t count = 0;
for (int i = 0; i < count; i++) {
    // ...
}

// 启用编译器警告
// GCC: -Wall -Wextra -Werror=uninitialized
```

**原因**：未初始化的指针可能指向任意地址（包括代码区或外设寄存器），导致HardFault。未初始化的变量值不确定，导致逻辑错误。

## Gotcha 4：忽略看门狗配置

**问题**：看门狗使能但喂狗不当，导致系统反复重启。

❌ **Before（错误做法）**
```c
// 错误：看门狗超时太短
IWDG_Init(100);  // 100ms超时

while (1) {
    process_task();  // 偶尔执行 > 100ms
    IWDG_Refresh();  // 来不及喂狗，系统重启
}
```

✅ **After（正确做法）**
```c
// 正确：合理配置看门狗
IWDG_Init(2000);  // 2秒超时，大于主循环最大执行时间 × 2

while (1) {
    IWDG_Refresh();  // 先喂狗
    process_task();  // 再执行任务
}

// 或：在多个任务点喂狗
while (1) {
    IWDG_Refresh();
    task1();
    IWDG_Refresh();
    task2();
}
```

**原因**：看门狗用于检测系统死机，超时时间必须大于系统正常运行的最大周期。喂狗位置应在关键任务完成后，而非仅仅放在循环末尾。

## Gotcha 5：低功耗模式下未保存上下文

**问题**：进入深度休眠前未保存寄存器和外设状态，唤醒后系统异常。

❌ **Before（错误做法）**
```c
// 错误：直接进入休眠，未保存状态
void enter_sleep(void) {
    HAL_PWR_EnterSTOPMode(PWR_LOWPOWERREGULATOR_ON, PWR_STOPENTRY_WFI);
    // 唤醒后时钟恢复，但外设状态丢失
}
```

✅ **After（正确做法）**
```c
// 正确：保存状态，恢复时钟和外设
void enter_sleep(void) {
    save_peripheral_states();  // 保存外设状态
    HAL_SuspendTick();         // 暂停RTOS Tick
    HAL_PWR_EnterSTOPMode(PWR_LOWPOWERREGULATOR_ON, PWR_STOPENTRY_WFI);
    // 唤醒后
    HAL_ResumeTick();          // 恢复RTOS Tick
    SystemClock_Config();      // 恢复系统时钟
    restore_peripheral_states(); // 恢复外设状态
}
```

**原因**：深度休眠会关闭主时钟和部分外设。唤醒后必须重新配置时钟和外设，否则系统运行异常。
