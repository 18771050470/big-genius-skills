# Gotchas

> 只写嵌入式测试容易犯错的**非显而易见的事实**。通用知识不要写。

## Gotcha 1：仅在宿主机测试忽略目标机差异

**问题**：单元测试在 x86 宿主机通过，但在 ARM 目标机上失败（字节序、对齐、编译器差异）。

❌ **Before（错误做法）**
```c
// 在 x86 Linux 上测试通过
uint32_t value = 0x12345678;
uint8_t *ptr = (uint8_t *)&value;
assert(ptr[0] == 0x78);  // 小端：通过

// 但在 ARM Cortex-M（大端模式）上：
// ptr[0] == 0x12，测试失败！
```

✅ **After（正确做法）**
```c
// 使用标准函数处理字节序
#include <endian.h>

uint32_t value = 0x12345678;
uint32_t network_value = htonl(value);  // 总是转为大端（网络字节序）

// 或者显式处理，不依赖平台字节序
uint8_t bytes[4];
bytes[0] = (value >> 24) & 0xFF;
bytes[1] = (value >> 16) & 0xFF;
bytes[2] = (value >> 8) & 0xFF;
bytes[3] = value & 0xFF;

// 测试必须在目标机上执行
// 使用交叉编译 + 硬件在环测试
```

**原因**：宿主机（x86）和目标机（ARM）在字节序、数据对齐、整数大小、编译器优化等方面可能存在差异。必须在目标机或精确的仿真环境中验证。

## Gotcha 2：未测试看门狗和异常恢复

**问题**：固件在正常情况下工作良好，但看门狗超时或异常发生后无法恢复，导致设备变砖。

❌ **Before（错误做法）**
```c
// 主循环，无看门狗喂狗
void main_loop() {
    while (1) {
        read_sensors();
        process_data();
        control_output();
        // 如果 process_data 死循环，看门狗超时，设备重启
        // 但重启后可能再次进入相同状态
    }
}
```

✅ **After（正确做法）**
```c
// 看门狗管理
#define WATCHDOG_TIMEOUT_MS 1000
#define MAX_RESTART_COUNT 3

static uint8_t restart_count = 0;

void init_watchdog() {
    // 配置看门狗超时 1 秒
    IWDG->KR = 0xCCCC;  // 启动看门狗
    IWDG->KR = 0x5555;  // 允许写预分频
    IWDG->PR = 0x06;    // 预分频
    IWDG->RLR = 0xFFF;  // 重载值
}

void feed_watchdog() {
    IWDG->KR = 0xAAAA;  // 喂狗
}

void main_loop() {
    init_watchdog();
    
    while (1) {
        feed_watchdog();  // 每个循环喂狗
        
        if (restart_count >= MAX_RESTART_COUNT) {
            // 连续重启多次，进入安全模式
            enter_safe_mode();
            break;
        }
        
        read_sensors();
        process_data();
        control_output();
        
        // 测试看门狗：故意不喂狗，验证复位
        // 测试异常恢复：注入非法指令，验证 graceful degradation
    }
}

// 启动时检查复位原因
void check_reset_cause() {
    if (RCC->CSR & RCC_CSR_IWDGRSTF) {
        restart_count++;
        log_error("Watchdog reset detected, count: %d", restart_count);
    }
    RCC->CSR |= RCC_CSR_RMVF;  // 清除复位标志
}
```

**原因**：嵌入式设备通常部署在无人值守环境，必须能自动从故障中恢复。看门狗和异常恢复机制必须在测试中验证，不能仅假设有效。

## Gotcha 3：忽略栈溢出检测

**问题**：递归或大数据结构导致栈溢出，破坏堆或其他数据，故障现象奇怪且难以定位。

❌ **Before（错误做法）**
```c
// 大数组放在栈上
void process_data() {
    uint8_t buffer[4096];  // 栈上 4KB
    // 如果栈大小只有 2KB，溢出！
    read_into_buffer(buffer);
}

// 无限制的递归
void traverse_tree(node_t *node) {
    if (!node) return;
    process_node(node);
    traverse_tree(node->left);   // 树太深时栈溢出
    traverse_tree(node->right);
}
```

✅ **After（正确做法）**
```c
// 大数组放在堆或静态区
static uint8_t buffer[4096];  // 静态区

void process_data() {
    read_into_buffer(buffer);
}

// 限制递归深度
#define MAX_RECURSION_DEPTH 100

void traverse_tree(node_t *node, uint8_t depth) {
    if (!node) return;
    if (depth > MAX_RECURSION_DEPTH) {
        log_error("Recursion depth exceeded");
        return;
    }
    process_node(node);
    traverse_tree(node->left, depth + 1);
    traverse_tree(node->right, depth + 1);
}

// 栈溢出检测（使用 MPU 或栈填充模式）
#define STACK_FILL_PATTERN 0xDEADBEEF

void init_stack_guard() {
    // 在栈底填充已知模式
    uint32_t *stack_bottom = get_stack_bottom();
    for (int i = 0; i < 16; i++) {
        stack_bottom[i] = STACK_FILL_PATTERN;
    }
}

bool check_stack_overflow() {
    uint32_t *stack_bottom = get_stack_bottom();
    for (int i = 0; i < 16; i++) {
        if (stack_bottom[i] != STACK_FILL_PATTERN) {
            log_error("Stack overflow detected!");
            return true;
        }
    }
    return false;
}
```

**原因**：嵌入式系统栈通常很小（几 KB），栈溢出不会触发段错误（无 MMU），而是静默破坏其他数据。必须通过 MPU、栈填充模式或静态分析检测栈溢出。

## Gotcha 4：未测试掉电和数据一致性

**问题**：设备在写数据时掉电，导致数据损坏或结构不一致，重启后无法正常工作。

❌ **Before（错误做法）**
```c
// 直接写入 Flash
void save_config(config_t *config) {
    flash_erase(CONFIG_ADDR);
    flash_write(CONFIG_ADDR, config, sizeof(config_t));
    // 如果在 flash_write 过程中掉电，数据不完整！
}
```

✅ **After（正确做法）**
```c
// 使用双备份 + CRC 校验
typedef struct {
    config_t config;
    uint32_t crc;
    uint32_t version;
} config_block_t;

#define CONFIG_SLOT_A 0x0800F000
#define CONFIG_SLOT_B 0x0800F800

void save_config(config_t *config) {
    config_block_t block;
    block.config = *config;
    block.crc = calculate_crc(config, sizeof(config_t));
    block.version = get_next_version();
    
    // 先写入备份区
    flash_erase(CONFIG_SLOT_B);
    flash_write(CONFIG_SLOT_B, &block, sizeof(block));
    
    // 确认写入成功后，再写入主区
    if (verify_flash(CONFIG_SLOT_B, &block)) {
        flash_erase(CONFIG_SLOT_A);
        flash_write(CONFIG_SLOT_A, &block, sizeof(block));
    }
}

bool load_config(config_t *config) {
    config_block_t block_a, block_b;
    
    // 读取两个区
    flash_read(CONFIG_SLOT_A, &block_a, sizeof(block_a));
    flash_read(CONFIG_SLOT_B, &block_b, sizeof(block_b));
    
    // 验证 CRC 和版本
    bool valid_a = (block_a.crc == calculate_crc(&block_a.config, sizeof(config_t)));
    bool valid_b = (block_b.crc == calculate_crc(&block_b.config, sizeof(config_t)));
    
    if (valid_a && valid_b) {
        // 都有效，使用版本新的
        *config = (block_a.version >= block_b.version) ? block_a.config : block_b.config;
        return true;
    } else if (valid_a) {
        *config = block_a.config;
        return true;
    } else if (valid_b) {
        *config = block_b.config;
        return true;
    }
    
    return false;  // 都损坏，使用默认配置
}

// 测试掉电场景
void test_power_loss_during_write() {
    // 在 flash_write 的不同阶段模拟掉电
    // 验证重启后能恢复有效配置
}
```

**原因**：嵌入式设备随时可能掉电（电池耗尽、用户拔电、电源波动）。必须设计掉电安全的数据存储机制（双备份、原子写、CRC 校验），并在测试中模拟掉电场景。
