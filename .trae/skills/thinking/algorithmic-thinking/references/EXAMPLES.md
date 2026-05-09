# 分析示例

## 示例 1：用户输入密码检测

### 输入
设计一个函数 `is_valid_password(p)`，要求：
- 长度 ≥ 8
- 至少包含一个大写字母、一个小写字母、一个数字
- 返回 True/False

### Step 1：问题定义
- 输入：字符串 p
- 输出：布尔值
- 约束：无特殊字符要求（但需确保输入为字符串）
- 边界：空字符串、None、全部大写等

### Step 2：分解与模式匹配
子问题：
1. 检查长度
2. 检查是否包含大写
3. 检查是否包含小写
4. 检查是否包含数字
模式：线性扫描、布尔聚合

### Step 3：抽象与模型
- 数据结构：整数计数器或布尔 flag
- 伪代码：
```
def is_valid_password(p):
    if not isinstance(p, str) or len(p) < 8:
        return False
    has_upper = has_lower = has_digit = False
    for ch in p:
        if 'A' <= ch <= 'Z': has_upper = True
        elif 'a' <= ch <= 'z': has_lower = True
        elif '0' <= ch <= '9': has_digit = True
    return has_upper and has_lower and has_digit
```

### Step 4：步进设计
1. 检查输入是否为字符串，否则返回 False
2. 若长度 < 8 → False
3. 初始化三个布尔变量为 False
4. 遍历每个字符，更新对应标志
5. 返回三个标志的与

### Step 5：正确性验证
- 输入："Abc123!" → 长度≥8，遍历得到所有标志为 True → 返回 True ✅
- 输入："abc123!" → 无大写 → 返回 False ✅
- 输入："" → 长度 < 8 → False ✅
- 输入：None → 先判断类型 → False ✅

### Step 6：效率分析
- 时间复杂度：O(n)，n 为字符串长度
- 空间复杂度：O(1)，仅三个布尔变量

### Step 7：实现与测试（略）

### 最终输出
明确的函数步骤，无歧义，满足所有边界。

---

## 示例 2：实现贪心算法找零（硬币无限供应）

### 输入
给定硬币面额 [25, 10, 5, 1] 和金额 amount，用最少数量的硬币找零。

### Step 1：问题定义
- 输入：整数 amount（>=0），整数数组 coins（正数，降序）
- 输出：最少硬币数，或 -1 如果无法找零（假设所有金额都能用 1 找零，所以总能找到）
- 边界：amount=0 → 0 枚

### Step 2：分解与模式匹配
子问题：重复选择最大面额不超过剩余金额 → 贪心模式（对于 canonical coin system 有效）

### Step 3：抽象
- 数据结构：计数器 count
- 伪代码：
```
def min_coins(coins, amount):
    count = 0
    for coin in coins:
        count += amount // coin
        amount %= coin
    return count
```

### Step 4：步进设计
1. 初始化 count=0
2. 遍历 coins（已按降序）
3.  当前硬币可用数量 = amount // coin
4.  count += 可用数量
5.  amount %= coin
6. 返回 count

### Step 5：正确性验证
- coins=[25,10,5,1], amount=99 → 25*3 + 10*2 + 5*0 + 1*4 = 3+2+0+4=9 ✅
- amount=0 → 循环中 amount%coin 一直为0，count=0 ✅
- coins=[25,10,1], amount=30 → 25*1 + 10*0 + 1*5 = 6，最优解也是6（因10*3需3枚，贪心得到25+5个1，共6枚，验证可行）

### Step 6：效率
- 时间复杂度 O(m)，m 为硬币种类数
- 空间复杂度 O(1)

### Step 7：实现

### 最终输出
清晰的贪心算法步骤。

---

## 示例 3：不该触发此 Skill 的反例

### 输入
“设计一个好看的网页配色方案。”

### 分析
- 这个问题没有明确的输入格式（是给定品牌色？指向任意？）
- 输出“好看的”具有主观性，无法用确定性步骤衡量
- 没有明确的成功标准（除了主观审美）
- 算法思维要求精确、可重复，但配色方案设计更适合创意思维或启发式美学规则

### 结论
不调用算法思维。应调用“设计思维”或“审美直觉”来处理，而非步骤化算法。