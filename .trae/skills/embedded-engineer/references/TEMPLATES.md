# 技术交付物模板

> 以下模板供 Agent 在输出技术交付物时参考。根据实际场景选择合适模板，不必全部使用。

---

## 交付物模板 1：固件架构设计

```markdown
# 固件架构设计：[项目名称]

## 架构概述
- **MCU型号**：[型号]
- **主频**：[X] MHz
- **Flash**：[X] KB
- **RAM**：[X] KB
- **架构类型**：[裸机 / FreeRTOS / 其他RTOS]

## 目录结构

```
firmware/
├── Core/
│   ├── Inc/          # 头文件
│   ├── Src/          # 源文件
│   └── Startup/      # 启动文件
├── Drivers/
│   ├── CMSIS/        # CMSIS核心
│   └── STM32F4xx_HAL_Driver/  # HAL驱动
├── Middleware/
│   └── FreeRTOS/     # RTOS（如使用）
├── Application/
│   ├── main.c        # 主程序
│   ├── app/          # 应用层
│   ├── bsp/          # 板级支持包
│   └── tasks/        # RTOS任务（如使用）
└── README.md
```

## 模块划分

| 模块 | 职责 | 接口 |
|------|------|------|
| HAL层 | 外设底层驱动 | HAL_xxx_Init/Read/Write |
| BSP层 | 板级初始化 | BSP_Init/DeInit |
| 应用层 | 业务逻辑 | App_Process/Event |
| 任务层 | RTOS任务（如使用） | Task_Create/Delete |

## 内存分配

| 区域 | 大小 | 用途 |
|------|------|------|
| 代码区 | [X] KB | 程序代码 |
| 数据区 | [X] KB | 全局变量 |
| 堆区 | [X] KB | 动态分配（如使用） |
| 栈区 | [X] KB | 任务栈 |
```

---

## 交付物模板 2：状态机设计

```markdown
# 状态机设计：[模块名称]

## 状态定义

| 状态 | 说明 | 进入动作 | 退出动作 |
|------|------|---------|---------|
| IDLE | 空闲 | 关闭外设 | - |
| INIT | 初始化 | 初始化外设 | - |
| RUNNING | 运行中 | 启动定时器 | 停止定时器 |
| ERROR | 错误 | 记录错误码 | - |
| SLEEP | 休眠 | 进入低功耗 | 恢复时钟 |

## 状态转移图

```
[IDLE] --初始化请求--> [INIT]
[INIT] --初始化成功--> [RUNNING]
[INIT] --初始化失败--> [ERROR]
[RUNNING] --错误发生--> [ERROR]
[RUNNING] --休眠请求--> [SLEEP]
[SLEEP] --唤醒事件--> [RUNNING]
[ERROR] --复位请求--> [IDLE]
```

## 事件定义

| 事件 | 说明 | 触发条件 |
|------|------|---------|
| EV_INIT | 初始化请求 | 上电或软件复位 |
| EV_INIT_OK | 初始化成功 | 所有外设初始化成功 |
| EV_INIT_FAIL | 初始化失败 | 任一外设初始化失败 |
| EV_ERROR | 错误发生 | 外设错误或通信超时 |
| EV_SLEEP | 休眠请求 | 空闲超时 |
| EV_WAKEUP | 唤醒事件 | 外部中断或定时器 |
| EV_RESET | 复位请求 | 用户命令或看门狗 |

## 代码实现

```c
typedef enum {
    STATE_IDLE,
    STATE_INIT,
    STATE_RUNNING,
    STATE_ERROR,
    STATE_SLEEP,
    STATE_MAX
} State_t;

typedef enum {
    EV_INIT,
    EV_INIT_OK,
    EV_INIT_FAIL,
    EV_ERROR,
    EV_SLEEP,
    EV_WAKEUP,
    EV_RESET,
    EV_MAX
} Event_t;

State_t state_machine(State_t current_state, Event_t event) {
    switch (current_state) {
        case STATE_IDLE:
            if (event == EV_INIT) return STATE_INIT;
            break;
        case STATE_INIT:
            if (event == EV_INIT_OK) return STATE_RUNNING;
            if (event == EV_INIT_FAIL) return STATE_ERROR;
            break;
        // ... 其他状态
    }
    return current_state;
}
```
```

---

## 交付物模板 3：外设驱动接口

```markdown
# 外设驱动接口：[外设名称]

## 初始化接口

```c
/**
 * @brief 初始化外设
 * @param config 配置参数
 * @return 0成功，非0失败
 */
int Driver_Init(Driver_Config_t *config);
```

## 数据收发接口

```c
/**
 * @brief 发送数据
 * @param data 数据指针
 * @param len 数据长度
 * @param timeout 超时时间（ms）
 * @return 实际发送长度，-1失败
 */
int Driver_Send(uint8_t *data, uint16_t len, uint32_t timeout);

/**
 * @brief 接收数据
 * @param buffer 接收缓冲区
 * @param len 期望接收长度
 * @param timeout 超时时间（ms）
 * @return 实际接收长度，-1失败
 */
int Driver_Receive(uint8_t *buffer, uint16_t len, uint32_t timeout);
```

## 中断/DMA接口

```c
/**
 * @brief 中断服务程序
 */
void Driver_IRQHandler(void);

/**
 * @brief DMA传输完成回调
 */
void Driver_DMA_Callback(void);
```

## 配置参数

```c
typedef struct {
    uint32_t baudrate;      // 波特率
    uint8_t data_bits;      // 数据位
    uint8_t stop_bits;      // 停止位
    uint8_t parity;         // 校验位
    uint8_t mode;           // 模式（轮询/中断/DMA）
} Driver_Config_t;
```

## 使用示例

```c
// 初始化
Driver_Config_t config = {
    .baudrate = 115200,
    .data_bits = 8,
    .stop_bits = 1,
    .parity = 0,
    .mode = MODE_DMA
};
Driver_Init(&config);

// 发送
uint8_t data[] = "Hello";
Driver_Send(data, sizeof(data), 1000);

// 接收
uint8_t buffer[64];
int len = Driver_Receive(buffer, 64, 1000);
```
```

---

## 交付物模板 4：低功耗策略

```markdown
# 低功耗策略：[项目名称]

## 功耗目标

| 模式 | 目标电流 | 最大允许 |
|------|---------|---------|
| 运行模式 | [X] mA | [Y] mA |
| 睡眠模式 | [X] μA | [Y] μA |
| 深度睡眠 | [X] μA | [Y] μA |
| 关机模式 | [X] μA | [Y] μA |

## 休眠策略

| 场景 | 休眠模式 | 唤醒源 | 唤醒时间 |
|------|---------|--------|---------|
| 空闲 < 100ms | 睡眠 | 中断 | < 10μs |
| 空闲 100ms-1s | 深度睡眠 | 定时器 | < 1ms |
| 空闲 > 1s | 关机 | 外部中断 | < 10ms |

## 外设电源管理

| 外设 | 运行模式 | 睡眠模式 | 深度睡眠 |
|------|---------|---------|---------|
| UART | 开启 | 关闭 | 关闭 |
| ADC | 开启 | 关闭 | 关闭 |
| GPIO | 保持 | 保持 | 关闭 |
| RTC | 开启 | 开启 | 开启 |

## 代码实现

```c
void Enter_LowPower_Mode(PowerMode_t mode) {
    switch (mode) {
        case MODE_SLEEP:
            HAL_SuspendTick();
            HAL_PWR_EnterSLEEPMode(PWR_MAINREGULATOR_ON, PWR_SLEEPENTRY_WFI);
            HAL_ResumeTick();
            break;
        case MODE_DEEP_SLEEP:
            save_peripheral_states();
            HAL_SuspendTick();
            HAL_PWR_EnterSTOPMode(PWR_LOWPOWERREGULATOR_ON, PWR_STOPENTRY_WFI);
            HAL_ResumeTick();
            SystemClock_Config();
            restore_peripheral_states();
            break;
        case MODE_SHUTDOWN:
            HAL_PWR_EnterSTANDBYMode();
            break;
    }
}
```

## 功耗测试记录

| 模式 | 实测电流 | 目标 | 状态 |
|------|---------|------|------|
| 运行 | [X] mA | [Y] mA | ✅/❌ |
| 睡眠 | [X] μA | [Y] μA | ✅/❌ |
| 深度睡眠 | [X] μA | [Y] μA | ✅/❌ |
```
