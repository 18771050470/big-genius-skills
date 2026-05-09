# 技术交付物模板

> 以下模板供 Agent 在输出技术交付物时参考。根据实际场景选择合适模板，不必全部使用。

---

## 交付物模板 1：模块设计文档

```markdown
# 模块设计：[模块名称]

## 模块概述
- **功能**：[一句话描述]
- **接口类型**：[AXI/ Avalon/ 自定义]
- **时钟频率**：[X] MHz
- **资源预算**：LUT [N] / FF [N] / BRAM [N] / DSP [N]

## 接口定义

| 信号名 | 方向 | 宽度 | 说明 |
|--------|------|------|------|
| clk | Input | 1 | 时钟 |
| rst_n | Input | 1 | 异步复位，低有效 |
| data_in | Input | [N] | 输入数据 |
| data_out | Output | [N] | 输出数据 |
| valid_in | Input | 1 | 输入数据有效 |
| valid_out | Output | 1 | 输出数据有效 |
| ready_in | Output | 1 | 可接收数据 |
| ready_out | Input | 1 | 下游可接收数据 |

## 功能描述

### 状态机

```
[IDLE] --valid_in & ready_in--> [PROCESS]
[PROCESS] --处理完成--> [OUTPUT]
[OUTPUT] --valid_out & ready_out--> [IDLE]
```

### 数据处理流程

1. 接收输入数据（valid_in & ready_in）
2. 数据处理（[N] 个时钟周期）
3. 输出结果（valid_out）
4. 等待下游接收（ready_out）

## 时序说明

| 参数 | 值 | 说明 |
|------|-----|------|
| 输入建立时间 | [X] ns | data_in相对于clk |
| 输入保持时间 | [X] ns | data_in相对于clk |
| 输出延迟 | [X] ns | clk到data_out |
| 处理延迟 | [N] 周期 | 输入到输出 |

## 资源预估

| 资源类型 | 预估用量 | 占比 |
|---------|---------|------|
| LUT | [N] | [X]% |
| FF | [N] | [X]% |
| BRAM | [N] | [X]% |
| DSP | [N] | [X]% |
```

---

## 交付物模板 2：时序约束（SDC）

```tcl
# 时序约束文件：[项目名称].sdc

# 主时钟
 create_clock -period 10.000 -name clk [get_ports clk]
# 周期10ns = 100MHz

# 衍生时钟
 create_generated_clock -name clk_div2 -source [get_ports clk] \
     -divide_by 2 [get_pins clk_div_reg/Q]

# 时钟不确定性
 set_clock_uncertainty -setup 0.200 [get_clocks clk]
 set_clock_uncertainty -hold 0.050 [get_clocks clk]

# 输入延迟
 set_input_delay -clock clk -max 2.000 [get_ports data_in*]
 set_input_delay -clock clk -min 0.500 [get_ports data_in*]

# 输出延迟
 set_output_delay -clock clk -max 2.000 [get_ports data_out*]
 set_output_delay -clock clk -min 0.500 [get_ports data_out*]

# 假路径
 set_false_path -from [get_ports rst_n] -to [get_clocks clk]

# 多周期路径
 set_multicycle_path -setup 2 -from [get_pins reg_a[*]/C] \
     -to [get_pins reg_b[*]/D]

# 异步时钟域
 set_clock_groups -asynchronous -group [get_clocks clk] \
     -group [get_clocks clk_div2]

# 最大延迟约束
 set_max_delay -from [get_pins source_reg/C] -to [get_pins dest_reg/D] 5.000
```

---

## 交付物模板 3：状态机编码

```verilog
// 状态机模板：[状态机名称]

module state_machine (
    input clk,
    input rst_n,
    input event_a,
    input event_b,
    output reg [2:0] state,
    output reg action_x,
    output reg action_y
);

    // 状态编码（独热码）
    localparam IDLE  = 3'b001;
    localparam STATE_A = 3'b010;
    localparam STATE_B = 3'b100;
    
    reg [2:0] next_state;
    
    // 状态寄存器（时序逻辑）
    always @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            state <= IDLE;
        else
            state <= next_state;
    end
    
    // 次态逻辑（组合逻辑）
    always @(*) begin
        next_state = state;  // 默认保持当前状态
        case (state)
            IDLE: begin
                if (event_a)
                    next_state = STATE_A;
                else if (event_b)
                    next_state = STATE_B;
            end
            
            STATE_A: begin
                if (event_b)
                    next_state = STATE_B;
                else if (!event_a)
                    next_state = IDLE;
            end
            
            STATE_B: begin
                if (event_a)
                    next_state = STATE_A;
                else if (!event_b)
                    next_state = IDLE;
            end
            
            default: next_state = IDLE;  // 安全状态机
        endcase
    end
    
    // 输出逻辑（组合逻辑或时序逻辑）
    always @(*) begin
        action_x = 0;
        action_y = 0;
        case (state)
            STATE_A: action_x = 1;
            STATE_B: action_y = 1;
            default: ;
        endcase
    end

endmodule
```

---

## 交付物模板 4：跨时钟域FIFO

```verilog
// 异步FIFO模板

module async_fifo #(
    parameter DATA_WIDTH = 8,
    parameter FIFO_DEPTH = 16,
    parameter ADDR_WIDTH = $clog2(FIFO_DEPTH)
)(
    input wr_clk,
    input wr_rst_n,
    input wr_en,
    input [DATA_WIDTH-1:0] wr_data,
    output fifo_full,
    
    input rd_clk,
    input rd_rst_n,
    input rd_en,
    output reg [DATA_WIDTH-1:0] rd_data,
    output fifo_empty
);

    // 双端口RAM
    reg [DATA_WIDTH-1:0] mem [0:FIFO_DEPTH-1];
    
    // 写指针（二进制 + 格雷码）
    reg [ADDR_WIDTH:0] wr_ptr_bin, wr_ptr_gray;
    reg [ADDR_WIDTH:0] wr_ptr_gray_sync1, wr_ptr_gray_sync2;
    
    // 读指针（二进制 + 格雷码）
    reg [ADDR_WIDTH:0] rd_ptr_bin, rd_ptr_gray;
    reg [ADDR_WIDTH:0] rd_ptr_gray_sync1, rd_ptr_gray_sync2;
    
    // 写时钟域
    always @(posedge wr_clk or negedge wr_rst_n) begin
        if (!wr_rst_n) begin
            wr_ptr_bin <= 0;
            wr_ptr_gray <= 0;
        end else if (wr_en && !fifo_full) begin
            mem[wr_ptr_bin[ADDR_WIDTH-1:0]] <= wr_data;
            wr_ptr_bin <= wr_ptr_bin + 1;
            wr_ptr_gray <= (wr_ptr_bin + 1) ^ ((wr_ptr_bin + 1) >> 1);
        end
    end
    
    // 读时钟域
    always @(posedge rd_clk or negedge rd_rst_n) begin
        if (!rd_rst_n) begin
            rd_ptr_bin <= 0;
            rd_ptr_gray <= 0;
            rd_data <= 0;
        end else if (rd_en && !fifo_empty) begin
            rd_data <= mem[rd_ptr_bin[ADDR_WIDTH-1:0]];
            rd_ptr_bin <= rd_ptr_bin + 1;
            rd_ptr_gray <= (rd_ptr_bin + 1) ^ ((rd_ptr_bin + 1) >> 1);
        end
    end
    
    // 指针同步（写指针同步到读时钟域）
    always @(posedge rd_clk or negedge rd_rst_n) begin
        if (!rd_rst_n) begin
            wr_ptr_gray_sync1 <= 0;
            wr_ptr_gray_sync2 <= 0;
        end else begin
            wr_ptr_gray_sync1 <= wr_ptr_gray;
            wr_ptr_gray_sync2 <= wr_ptr_gray_sync1;
        end
    end
    
    // 指针同步（读指针同步到写时钟域）
    always @(posedge wr_clk or negedge wr_rst_n) begin
        if (!wr_rst_n) begin
            rd_ptr_gray_sync1 <= 0;
            rd_ptr_gray_sync2 <= 0;
        end else begin
            rd_ptr_gray_sync1 <= rd_ptr_gray;
            rd_ptr_gray_sync2 <= rd_ptr_gray_sync1;
        end
    end
    
    // 空满判断
    assign fifo_empty = (rd_ptr_gray == wr_ptr_gray_sync2);
    assign fifo_full = (wr_ptr_gray == {~rd_ptr_gray_sync2[ADDR_WIDTH:ADDR_WIDTH-1], 
                                         rd_ptr_gray_sync2[ADDR_WIDTH-2:0]});

endmodule
```

---

## 交付物模板 5：综合与实现报告

```markdown
# 综合与实现报告：[项目名称]

## 综合结果

### 资源利用率

| 资源类型 | 已用 | 可用 | 利用率 |
|---------|------|------|--------|
| LUT | [N] | [N] | [X]% |
| LUTRAM | [N] | [N] | [X]% |
| FF | [N] | [N] | [X]% |
| BRAM | [N] | [N] | [X]% |
| DSP | [N] | [N] | [X]% |
| IO | [N] | [N] | [X]% |
| BUFG | [N] | [N] | [X]% |
| MMCM | [N] | [N] | [X]% |

### 时序摘要

| 时钟 | 约束 | 实际 | Slack | 状态 |
|------|------|------|-------|------|
| clk | 10.0 ns | [X] ns | [X] ns | ✅/❌ |
| clk_div2 | 20.0 ns | [X] ns | [X] ns | ✅/❌ |

### 关键路径

| 路径 | 延迟 | 起点 | 终点 |
|------|------|------|------|
| 1 | [X] ns | [起点] | [终点] |
| 2 | [X] ns | [起点] | [终点] |
| 3 | [X] ns | [起点] | [终点] |

## 实现结果

### 布局布线信息
- **WNS**（Worst Negative Slack）：[X] ns
- **TNS**（Total Negative Slack）：[X] ns
- **WHS**（Worst Hold Slack）：[X] ns
- **THS**（Total Hold Slack）：[X] ns

### 功耗估算
- **动态功耗**：[X] W
- **静态功耗**：[X] W
- **总功耗**：[X] W

## 结论
- **时序收敛**：✅/❌
- **资源合理**：✅/❌
- **可上板验证**：✅/❌
```
