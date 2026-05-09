# Gotchas

> 只写 Agent 容易犯错的**非显而易见的事实**。通用知识不要写。
> 每个 Gotcha 必须包含：问题描述 + ❌ Before（错误做法） + ✅ After（正确做法） + 原因解释。

## Gotcha 1：跨时钟域信号未同步

**问题**：信号从一个时钟域直接传输到另一个时钟域，导致亚稳态，数据可能错误。

❌ **Before（错误做法）**
```verilog
// 错误：直接跨时钟域传输
module cdc_bad (
    input clk_a,
    input clk_b,
    input data_a,
    output reg data_b
);
    always @(posedge clk_b) begin
        data_b <= data_a;  // 错误！data_a属于clk_a域
    end
endmodule
```

✅ **After（正确做法）**
```verilog
// 正确：双触发器同步（单bit信号）
module cdc_sync (
    input clk_a,
    input clk_b,
    input data_a,
    output reg data_b
);
    reg sync_reg1, sync_reg2;
    
    always @(posedge clk_b) begin
        sync_reg1 <= data_a;  // 第一拍：可能亚稳态
        sync_reg2 <= sync_reg1;  // 第二拍：亚稳态概率极低
        data_b <= sync_reg2;  // 稳定后的数据
    end
endmodule

// 正确：异步FIFO（多bit信号）
module cdc_fifo (
    input wr_clk,
    input rd_clk,
    input [7:0] wr_data,
    input wr_en,
    output [7:0] rd_data,
    input rd_en,
    output fifo_empty,
    output fifo_full
);
    // 使用异步FIFO IP核或手写格雷码指针同步FIFO
    // ...
endmodule
```

**原因**：跨时钟域传输时，信号可能在目标时钟的上升沿附近变化，导致触发器进入亚稳态。双触发器同步可以将亚稳态概率降低到可忽略水平。多bit信号必须用FIFO或握手协议，避免多位同时变化时部分位同步成功、部分失败。

## Gotcha 2：不完整的if/case语句产生锁存器

**问题**：组合逻辑中的if或case语句未覆盖所有条件，综合工具推断出锁存器，导致时序不可控。

❌ **Before（错误做法）**
```verilog
// 错误：不完整的if语句产生锁存器
module latch_bad (
    input a,
    input b,
    input sel,
    output reg y
);
    always @(*) begin
        if (sel)
            y = a;  // sel=0时，y保持原值 → 锁存器！
    end
endmodule

// 错误：不完整的case语句产生锁存器
module case_bad (
    input [1:0] sel,
    input a, b, c,
    output reg y
);
    always @(*) begin
        case (sel)
            2'b00: y = a;
            2'b01: y = b;
            // 2'b10和2'b11未覆盖 → 锁存器！
        endcase
    end
endmodule
```

✅ **After（正确做法）**
```verilog
// 正确：完整的if语句
module latch_good (
    input a,
    input b,
    input sel,
    output reg y
);
    always @(*) begin
        if (sel)
            y = a;
        else
            y = b;  // 覆盖所有条件，无锁存器
    end
endmodule

// 正确：完整的case语句
module case_good (
    input [1:0] sel,
    input a, b, c, d,
    output reg y
);
    always @(*) begin
        case (sel)
            2'b00: y = a;
            2'b01: y = b;
            2'b10: y = c;
            2'b11: y = d;
            default: y = a;  // 保险起见，加default
        endcase
    end
endmodule

// 正确：明确使用寄存器（时序逻辑）
module reg_good (
    input clk,
    input a,
    input sel,
    output reg y
);
    always @(posedge clk) begin
        if (sel)
            y <= a;
        // 时序逻辑中，未覆盖条件保持原值（寄存器特性，非锁存器）
    end
endmodule
```

**原因**：组合逻辑中，未覆盖的条件意味着输出需要保持原值，综合工具会推断锁存器。锁存器是电平敏感器件，时序分析复杂，容易引起竞争条件和毛刺。时序逻辑中的保持是寄存器的正常行为，不会产生锁存器。

## Gotcha 3：关键路径过长导致时序不满足

**问题**：组合逻辑级数过多，关键路径延迟超过时钟周期，时序不满足。

❌ **Before（错误做法）**
```verilog
// 错误：长组合逻辑链
module long_path_bad (
    input clk,
    input [31:0] a, b, c, d, e,
    output reg [31:0] result
);
    always @(posedge clk) begin
        // 一个周期内完成5级运算，逻辑级数过多
        result <= (a * b) + (c * d) - e;
    end
endmodule
```

✅ **After（正确做法）**
```verilog
// 正确：流水线设计，每级一个周期
module pipeline_good (
    input clk,
    input [31:0] a, b, c, d, e,
    output reg [31:0] result
);
    reg [63:0] mult1, mult2;
    reg [63:0] add;
    
    // 第1级：乘法
    always @(posedge clk) begin
        mult1 <= a * b;
        mult2 <= c * d;
    end
    
    // 第2级：加法
    always @(posedge clk) begin
        add <= mult1 + mult2;
    end
    
    // 第3级：减法
    always @(posedge clk) begin
        result <= add - e;
    end
endmodule
```

**原因**：组合逻辑延迟与逻辑级数成正比。长组合逻辑链会导致关键路径延迟超过时钟周期，Setup Time不满足。流水线设计将长逻辑链拆分为多个短级，每级在一个时钟周期内完成，提高时钟频率。

## Gotcha 4：混合使用异步和同步复位

**问题**：设计中部分模块使用异步复位，部分使用同步复位，导致复位释放时亚稳态。

❌ **Before（错误做法）**
```verilog
// 错误：混合复位策略
module mix_reset_bad (
    input clk,
    input rst_n,
    input a,
    output reg b,
    output reg c
);
    // 模块1：异步复位
    always @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            b <= 0;
        else
            b <= a;
    end
    
    // 模块2：同步复位
    always @(posedge clk) begin
        if (!rst_n)
            c <= 0;
        else
            c <= a;
    end
endmodule
```

✅ **After（正确做法）**
```verilog
// 正确：统一的异步复位同步释放
module reset_sync_good (
    input clk,
    input rst_n,
    input a,
    output reg b
);
    reg rst_sync1, rst_sync2;
    wire rst_sync_n;
    
    // 异步复位同步释放
    always @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            rst_sync1 <= 0;
            rst_sync2 <= 0;
        end else begin
            rst_sync1 <= 1;
            rst_sync2 <= rst_sync1;
        end
    end
    
    assign rst_sync_n = rst_sync2;
    
    // 所有模块使用同步后的复位
    always @(posedge clk) begin
        if (!rst_sync_n)
            b <= 0;
        else
            b <= a;
    end
endmodule
```

**原因**：异步复位直接作用于触发器，复位释放时如果与时钟沿接近，会导致亚稳态。同步释放确保复位信号在时钟沿稳定后释放，避免亚稳态。统一复位策略避免不同模块复位时间不一致。

## Gotcha 5：使用不可综合的Verilog语法

**问题**：在RTL代码中使用不可综合的语法（如延时、文件操作、initial块用于综合），导致综合失败。

❌ **Before（错误做法）**
```verilog
// 错误：不可综合的代码
module unsynth_bad (
    input a,
    output b
);
    assign #10 b = a;  // 错误！延时不可综合
    
    initial begin
        $display("Hello");  // 错误！系统任务不可综合
        $dumpfile("wave.vcd");  // 错误！仅仿真可用
    end
    
    always @(*) begin
        if (a)
            b = 1;
        else
            b = 0;
        #5;  // 错误！延时不可综合
    end
endmodule
```

✅ **After（正确做法）**
```verilog
// 正确：可综合的代码
module synth_good (
    input clk,
    input a,
    output reg b
);
    // 时序逻辑用时钟，不用延时
    always @(posedge clk) begin
        b <= a;  // 一个时钟周期延迟
    end
endmodule

// 仿真测试平台（不可综合，仅用于仿真）
module tb;
    reg clk, a;
    wire b;
    
    // 实例化被测模块
    synth_good uut (.clk(clk), .a(a), .b(b));
    
    // 时钟生成（仅仿真）
    initial begin
        clk = 0;
        forever #5 clk = ~clk;  // 100MHz时钟
    end
    
    // 测试激励（仅仿真）
    initial begin
        $dumpfile("wave.vcd");
        $dumpvars(0, tb);
        
        a = 0;
        #20 a = 1;
        #20 a = 0;
        #20 $finish;
    end
endmodule
```

**原因**：综合工具只能将部分Verilog语法转换为硬件电路。延时、文件操作、系统任务等是仿真特有的语法，不可综合。RTL代码必须严格使用可综合子集。
