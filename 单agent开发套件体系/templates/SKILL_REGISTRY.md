# Skill 注册表

> 版本：v2.0
> 日期：2026-05-09
> 说明：全量 Skill 清单，定义各层级技能的触发条件与核心功能
> 配套文件：编程思维模型精选清单.md（思维层）、角色类智能体清单.md（角色层）

---

## L1 - 思维层

> 职责：提供决策框架，指导如何分析问题
> 触发条件：复杂问题、架构决策、风险评估、长期规划

### 1.1 通用思维模型（A-G组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **A. 底层认知基础** | 因果思维 (Causal Thinking)、归纳思维 (Inductive Thinking)、演绎思维 (Deductive Thinking)、溯因思维 (Abductive Thinking)、类比思维 (Analogical Thinking)、比较思维 (Comparative Thinking)、抽象思维 (Abstract Thinking)、模型思维 (Model Thinking)、还原论思维 (Reductionism)、整体论思维 (Holism)、辩证思维 (Dialectical Thinking)、批判性思维 (Critical Thinking)、创造性思维 (Creative Thinking)、叙事思维 (Narrative Thinking)、量化思维 (Quantitative Thinking)、时间思维 (Temporal Thinking)、规模思维 (Scale Thinking)、模式识别思维 (Pattern Recognition Thinking)、算法思维 (Algorithmic Thinking)、元思维 (Meta-Thinking) | 问题本质分析、逻辑推理、知识迁移 |
| **B. 决策与判断** | 沉没成本谬误 (Sunk Cost Fallacy)、损失厌恶 (Loss Aversion)、确认偏误 (Confirmation Bias)、可得性偏差 (Availability Bias)、锚定效应 (Anchoring Effect)、后见之明偏误 (Hindsight Bias)、达克效应 (Dunning-Kruger Effect)、决策树 (Decision Tree)、概率思维 (Probabilistic Thinking)、贝叶斯更新 (Bayesian Updating)、机会成本思维 (Opportunity Cost)、逆向思维 (Inverse Thinking)、二阶思维 (Second-Order Thinking)、能力圈思维 (Circle of Competence) | 风险评估、方案对比、决策优化 |
| **C. 系统与复杂性** | 熵增定律 (Entropy)、正负反馈回路 (Feedback Loops)、临界点/引爆点 (Critical Mass / Tipping Point)、蝴蝶效应 (Butterfly Effect)、涌现 (Emergence)、反脆弱 (Antifragility)、系统思维 (System Thinking)、冗余思维 (Redundancy Thinking)、复利思维 (Compound Thinking) | 全局分析、系统动态、复杂性管理 |
| **D. 学习与认知** | 费曼学习法 (Feynman Technique)、成长型思维 (Growth Mindset)、思维模型格栅 (Mental Models Latticework)、地图不是疆域 (Map is Not the Territory)、汉隆剃刀 (Hanlon's Razor)、关注圈与影响圈 (Circle of Influence vs Concern)、均值回归 (Mean Reversion)、第一性原理 (First Principles)、悖论思维 (Paradox Thinking) | 知识获取、认知升级、持续学习 |
| **E. 创新与问题解决** | 水平思考 (Lateral Thinking)、设计思维 (Design Thinking)、TRIZ、六顶思考帽 (Six Thinking Hats)、连续追问5个为什么 (5 Whys)、分治思维 (Divide and Conquer)、约束思维 (Constraint Thinking)、极简思维 (Minimalism Thinking)、奥卡姆剃刀 (Occam's Razor) | 创新突破、问题拆解、方案生成 |
| **F. 心理学与行为** | 基本归因错误 (Fundamental Attribution Error)、光环效应 (Halo Effect)、幸存者偏差 (Survivorship Bias)、现状偏误 (Status Quo Bias)、边界思维 (Boundary Thinking) | 认知偏差防御、行为理解、边界管理 |
| **G. 风险与不确定性** | 预防原则 (Precautionary Principle)、不对称风险收益 (Asymmetric Risk/Reward) | 风险预防、不确定性管理 |

### 1.2 编程相关思维模型（H组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **H1. 设计原则与哲学** | 防腐思维 (Anti-Corrosion Thinking)、契约思维 (Contract Thinking)、DRY原则 (Don't Repeat Yourself)、关注点分离 (Separation of Concerns)、组合优于继承 (Composition over Inheritance)、快速失败 (Fail Fast)、防御性编程 (Defensive Programming) | 代码设计、质量保障 |
| **H2. SOLID原则** | 单一职责原则 (Single Responsibility Principle)、开闭原则 (Open/Closed Principle)、里氏替换原则 (Liskov Substitution Principle)、接口隔离原则 (Interface Segregation Principle)、依赖倒置原则 (Dependency Inversion Principle) | 面向对象设计 |
| **H3. 编程范式与模式** | 解耦思维 (Decoupling Thinking)、封装思维 (Encapsulation Thinking)、抽象分层思维 (Abstraction Layering)、事件驱动思维 (Event-Driven Thinking)、不可变思维 (Immutability Thinking)、并发思维 (Concurrency Thinking)、工具化思维 (Tooling Thinking)、产品思维（开发者版）(Product Thinking for Devs) | 编程范式、设计模式 |
| **H4. 工程实践** | 版本控制思维 (Version Control Thinking)、持续集成/持续交付思维 (CI/CD Thinking)、可观测性思维 (Observability Thinking)、渐进增强与优雅降级 (Progressive Enhancement & Graceful Degradation) | 工程流程、团队协作 |
| **H5. 调试与算法** | 调试思维 (Debugging Thinking)、递归思维 (Recursive Thinking) | 调试策略、算法设计 |
| **H6. 编程范式思维** | 命令式vs声明式思维 (Imperative vs Declarative)、面向对象思维 (Object-Oriented Thinking)、函数式编程思维 (Functional Programming Thinking)、响应式编程思维 (Reactive Programming Thinking)、范式灵活切换思维 (Paradigm Flexibility)、代码即沟通思维 (Code as Communication) | 编程范式选择 |

### 1.3 架构与设计思维模型（I组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **I. 软件架构设计** | 领域驱动设计 (Domain-Driven Design)、康威定律 (Conway's Law)、命令查询职责分离 (CQRS)、事件溯源 (Event Sourcing)、六边形架构 (Hexagonal Architecture)、API优先思维 (API-First Thinking)、演进式架构 (Evolutionary Architecture)、限界上下文思维 (Bounded Context)、权衡思维 (Trade-Off Thinking) | 系统设计、架构决策 |

### 1.4 产品设计与用户体验（J组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **J1. 用户研究** | 以用户为中心的设计 (User-Centered Design)、共情地图思维 (Empathy Mapping)、用户旅程地图 (User Journey Mapping)、JTBD思维 (Jobs to Be Done)、用户画像思维 (Persona Thinking) | 用户研究、需求分析 |
| **J2. 信息架构与交互** | 信息架构思维 (Information Architecture)、渐进式展示 (Progressive Disclosure)、可供性/示能思维 (Affordance)、心智模型对齐 (Mental Model Alignment) | 信息架构、交互设计 |
| **J3. 视觉设计** | 视觉层次思维 (Visual Hierarchy)、留白思维 (White Space / Negative Space)、一致性思维 (Consistency Thinking)、无障碍设计思维 (Accessibility Thinking) | 视觉设计、UI规范 |

### 1.5 AI与LLM思维模型（K组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **K. LLM与AI推理** | 思维链推理 (Chain-of-Thought)、思维树推理 (Tree-of-Thought)、思维图推理 (Graph-of-Thought)、少样本类比推理 (Few-Shot Analogical Reasoning)、自我反思与批判 (Self-Reflection / Self-Critique)、推理+行动框架 (ReAct)、结构化思维（系统提示）(Structured Thinking via System Prompt) | AI推理、Prompt工程 |

### 1.6 数据科学与机器学习（AW组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **AW. 数据科学与机器学习** | 偏差-方差权衡 (Bias-Variance Tradeoff)、特征工程思维 (Feature Engineering Thinking)、维度灾难思维 (Curse of Dimensionality)、交叉验证思维 (Cross-Validation Thinking)、A/B测试思维 (A/B Testing Thinking)、集成思维 (Ensemble Thinking)、GIGO思维 (Garbage In Garbage Out)、辛普森悖论 (Simpson's Paradox)、没有免费午餐定理 (No Free Lunch Theorem) | 数据科学、ML建模 |

### 1.7 创业与商业创新（Y组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **Y. 创业与商业创新** | 精益创业思维 (Lean Startup)、最小可行产品 (Minimum Viable Product)、商业模式画布 (Business Model Canvas)、产品市场匹配 (Product-Market Fit)、增长黑客思维 (Growth Hacking)、跨越鸿沟 (Crossing the Chasm)、颠覆式创新 (Disruptive Innovation)、平台思维 (Platform Thinking)、单元经济思维 (Unit Economics) | 创业策略、商业创新 |

### 1.8 安全与可靠性工程（AC组）

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **AC. 安全与可靠性工程** | 瑞士奶酪模型 (Swiss Cheese Model)、海因里希法则 (Heinrich's Law)、纵深防御思维 (Defense in Depth)、失效模式与影响分析 (FMEA)、高可靠性组织思维 (High Reliability Organization)、红蓝对抗思维 (Red Team / Blue Team) | 安全架构、风险防御 |

### 1.9 其他专业思维模型

| 分组 | 思维模型 | 核心功能 |
|------|---------|---------|
| **T. 数学与统计学** | 幂律分布思维 (Power Law Distribution)、正态分布思维 (Normal Distribution)、大数定律 (Law of Large Numbers)、排列组合思维 (Permutations & Combinations)、乘零效应 (Multiply by Zero Effect)、随机性思维 (Randomness & Stochastic Processes)、样本量思维 (Sample Size Thinking) | 数学基础、统计分析 |
| **M. 战略与管理** | 黄金圈法则 (Golden Circle)、SWOT分析 (SWOT Analysis)、PDCA循环 (PDCA Cycle)、安全边际 (Margin of Safety)、多模型交叉验证 (Multi-Model Cross-Validation)、迭代思维 (Iteration Thinking) | 战略决策、管理实践 |
| **Q. 时间与精力管理** | 艾森豪威尔矩阵 (Eisenhower Matrix)、精力管理思维 (Energy Management) | 时间管理、效率提升 |

---

## L2 - 角色层

> 职责：执行具体开发任务
> 触发条件：编码、调试、测试、设计、产品分析、运维

### L0 战略层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **产品经理** | Product Manager | 需求分析、优先级排序、用户故事、产品路线图 | 需求拆解、竞品分析、版本规划 |
| **Sprint排序员** | Sprint Prioritizer | Sprint规划、任务优先级、资源分配 | 迭代规划、任务分配 |
| **趋势研究员** | Trend Researcher | 技术趋势、市场趋势、竞品动态 | 技术预研、市场洞察 |
| **反馈综合师** | Feedback Synthesizer | 用户反馈收集、分析、优先级排序 | 用户研究、反馈处理 |
| **行为助推引擎** | Behavioral Nudge Engine | 用户行为分析、增长策略、转化优化 | 增长实验、行为设计 |
| **创业顾问** | Startup Advisor | 商业模式、定价策略、增长策略、一人公司运营 | 商业分析、融资策略 |
| **增长黑客** | Growth Hacker | 增长实验、病毒传播、渠道优化 | 用户增长、获客优化 |
| **内容创作者** | Content Creator | 技术内容、营销内容、社区内容 | 内容营销、技术布道 |
| **数据分析师** | Data Analyst | 数据分析、指标设计、报表制作 | 数据驱动决策 |
| **财务追踪员** | Financial Tracker | 财务监控、现金流管理、预算跟踪 | 财务管理 |
| **ASO优化师** | ASO Specialist | 应用商店优化、关键词优化、转化率优化 | 应用推广 |
| **财务预测分析师** | Financial Forecast Analyst | 财务建模、预测分析、场景规划 | 财务规划 |
| **供应商评估专家** | Vendor Evaluation Specialist | 供应商筛选、评估、谈判 | 供应链管理 |
| **动态定价策略师** | Dynamic Pricing Strategist | 定价模型、价格优化、竞争定价 | 定价策略 |
| **财务会计与报税师** | Accountant & Tax Filer | 会计核算、税务申报、合规管理 | 财务合规 |
| **税务筹划师** | Tax Planner | 税务优化、筹划策略、合规节税 | 税务优化 |
| **文案策划师** | Copywriter & Content Strategist | 文案创作、内容策略、品牌传播 | 品牌文案 |
| **技术负责人** | Tech Lead | 技术选型、架构评审、技术债务管理 | 技术决策、团队管理 |
| **制片人** | Studio Producer | 多项目统筹、战略对齐、资源分配 | 项目组合管理 |

### L1 设计层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **UX研究员** | UX Researcher | 用户研究、可用性测试、用户画像 | 用户洞察 |
| **UX架构师** | UX Architect | 信息架构、用户流程、交互设计 | 体验设计 |
| **UI设计师** | UI Designer | 界面设计、视觉设计、组件设计 | UI设计、设计系统 |
| **品牌守护者** | Brand Guardian | 品牌规范、视觉识别、品牌一致性 | 品牌管理 |
| **图像提示词工程师** | Image Prompt Engineer | AI图像生成、提示词优化、视觉创作 | AI视觉设计 |
| **动效/交互设计师** | Motion & Interaction Designer | 动效设计、微交互、原型动画 | 交互动效 |
| **视频制作人** | Video Producer | 视频策划、拍摄、剪辑、后期 | 视频内容 |
| **3D/AR设计师** | 3D/AR Designer | 3D建模、AR体验、空间设计 | 3D/AR设计 |
| **数据架构师** | Data Architect | 数据模型、数据流、数据治理 | 数据架构 |

### L2 前端层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **前端架构师** | Frontend Architect | 前端架构、组件体系、性能优化 | 前端架构设计 |
| **移动端工程师** | Mobile Engineer | 移动端开发、跨平台适配、原生集成 | App开发 |
| **小程序工程师** | Mini Program Engineer | 小程序开发、微信生态、轻应用 | 小程序开发 |
| **快速原型师** | Rapid Prototyper | 快速原型、MVP开发、概念验证 | 原型开发 |
| **微信生态开发者** | WeChat Ecosystem Developer | 微信公众号、小程序、支付集成 | 微信开发 |
| **国际化(i18n)工程师** | i18n Engineer | 多语言、本地化、全球化适配 | 国际化开发 |

### L3 后端层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **后端架构师** | Backend Architect | 后端架构、服务设计、系统优化 | 后端架构设计 |
| **API设计师** | API Designer | API设计、接口规范、文档编写 | API开发 |
| **数据库管理员(DBA)** | Database Administrator | 数据库管理、性能优化、备份恢复 | 数据库运维 |
| **软件架构师** | Software Architect | 系统架构、技术选型、架构评审 | 系统架构 |
| **数据工程师** | Data Engineer | 数据管道、ETL、数据仓库 | 数据工程 |
| **数据治理师** | Data Governance Specialist | 数据质量、数据标准、合规管理 | 数据治理 |
| **数据可视化工程师** | Data Visualization Engineer | 数据可视化、报表开发、BI工具 | 数据可视化 |

### L4 AI层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **AI架构师** | AI Architect | AI系统架构、模型选型、技术战略 | AI架构设计 |
| **AI集成工程师** | AI Integration Engineer | AI/ML功能集成、LLM接入、智能自动化 | AI集成开发 |
| **Prompt工程师** | Prompt Engineer | 提示词设计、Prompt优化、输出控制 | Prompt工程 |
| **AI Agent工程师** | AI Agent Engineer | Agent设计、多Agent协作、工具集成 | Agent开发 |
| **ML工程师** | ML Engineer | 模型训练、模型部署、MLOps | 机器学习工程 |
| **AI安全与评估工程师** | AI Safety & Evaluation Engineer | AI安全、模型评估、风险管控 | AI安全评估 |
| **AI治理与伦理审查师** | AI Governance & Ethics Reviewer | AI伦理、合规审查、偏见检测 | AI治理 |
| **数据标注与质量经理** | Data Annotation & Quality Manager | 数据标注、质量控制、标注团队管理 | 数据标注 |
| **语音AI工程师** | Voice AI Engineer | 语音识别、语音合成、语音交互 | 语音AI开发 |
| **计算机视觉工程师** | Computer Vision Engineer | 图像识别、目标检测、视觉分析 | CV开发 |

### L5 测试层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **QA工程师** | QA Engineer | 测试策略、质量保障、测试自动化 | 质量保障 |
| **API测试工程师** | API Test Engineer | API测试、契约测试、自动化测试 | API测试 |
| **安全工程师** | Security Engineer | 安全测试、漏洞扫描、安全审计 | 安全测试 |
| **性能优化师** | Performance Expert | 性能测试、性能分析、性能优化 | 性能优化 |
| **代码审查员** | Code Reviewer | 代码审查、规范检查、质量把关 | 代码审查 |
| **现实检验员** | Reality Checker | 假设验证、事实核查、逻辑检验 | 验证检验 |
| **实验追踪员** | Experiment Tracker | A/B测试、实验设计、结果分析 | 实验管理 |
| **嵌入式测试工程师** | Embedded Test Engineer | 嵌入式测试、硬件测试、固件测试 | 嵌入式测试 |
| **无障碍审核员** | Accessibility Auditor | 无障碍测试、WCAG合规、包容性设计 | 无障碍测试 |
| **网络安全工程师** | Network Security Engineer | 网络安全、渗透测试、安全加固 | 网络安全 |

### L6 运维层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **DevOps工程师** | DevOps Engineer | CI/CD、自动化部署、基础设施 | DevOps实践 |
| **SRE** | Site Reliability Engineer | 可靠性工程、SLO/SLI、故障响应 | 站点可靠性 |
| **云架构师** | Cloud Architect | 云架构设计、云服务选型、成本优化 | 云架构 |
| **工作流优化师** | Workflow Optimizer | 流程优化、自动化、效率提升 | 流程优化 |
| **故障响应指挥官** | Incident Response Commander | 故障响应、危机管理、事后复盘 | 故障管理 |
| **CI/CD流水线架构师** | CI/CD Pipeline Architect | 流水线设计、构建优化、发布管理 | CI/CD架构 |

### L7 硬件层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **硬件架构师** | Hardware Architect | 硬件架构、系统设计、器件选型 | 硬件架构 |
| **PCB设计师** | PCB Designer | PCB设计、信号完整性、EMC设计 | PCB开发 |
| **嵌入式/MCU工程师** | Embedded/MCU Engineer | 嵌入式开发、固件开发、驱动开发 | 嵌入式开发 |
| **IoT架构师** | IoT Architect | IoT架构、协议设计、边缘计算 | IoT架构 |
| **传感器工程师** | Sensor Engineer | 传感器选型、信号处理、校准 | 传感器开发 |
| **控制工程师** | Control Engineer | 控制算法、电机驱动、运动控制 | 控制系统 |
| **嵌入式Linux驱动工程师** | Embedded Linux Driver Engineer | Linux驱动、内核开发、设备树 | 驱动开发 |
| **FPGA数字设计工程师** | FPGA Digital Design Engineer | FPGA设计、数字逻辑、时序优化 | FPGA开发 |

### L8 合规层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **合规审查员** | Compliance Checker | 法律文件审查、隐私政策、法规合规 | 合规审查 |
| **知识产权顾问** | IP Consultant | 专利、商标、著作权、知识产权策略 | 知识产权 |
| **隐私合规专员** | Privacy Compliance Specialist | GDPR/CCPA/PIPL、隐私评估、合规审计 | 隐私合规 |
| **合同审查专家** | Contract Review Specialist | 合同审查、风险评估、条款谈判 | 合同审查 |
| **制度文件撰写专家** | Policy Document Writer | 制度编写、流程文档、合规手册 | 制度编写 |
| **数据出境合规专家** | Data Export Compliance Expert | 数据出境、跨境合规、安全评估 | 数据出境 |
| **劳动法顾问** | Labor Law Consultant | 劳动法规、用工合规、争议处理 | 劳动合规 |
| **安全合规审计师** | Security Compliance Auditor (SOC2/ISO27001) | 安全审计、认证合规、风险评估 | 安全合规 |
| **AI治理与伦理审查师** | AI Governance & Ethics Reviewer | AI伦理、算法审计、偏见检测 | AI伦理 |
| **ESG合规顾问** | ESG Compliance Consultant | ESG报告、可持续发展、社会责任 | ESG合规 |

### L9 文档层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **技术文档工程师** | Technical Writer | 技术文档、用户手册、API文档 | 技术写作 |
| **API文档专员** | API Documentation Specialist | API文档、SDK文档、开发者门户 | API文档 |
| **用户教育专员** | User Education Specialist | 教程编写、培训材料、知识库 | 用户教育 |
| **技术文档翻译专家** | Technical Translator | 技术翻译、本地化、术语管理 | 文档翻译 |

### L10 专项层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **Agent编排师** | Agents Orchestrator | 多Agent协作、工作流管理、任务分发 | Agent编排 |
| **代码考古学家** | Code Archaeologist | 遗留代码分析、代码库理解、迁移规划 | 代码考古 |
| **工具评估师** | Tool Evaluator | 技术评估、工具选型、PoC验证 | 工具评估 |
| **MCP构建师** | MCP Builder | MCP协议开发、工具集成、Server构建 | MCP开发 |
| **Git工作流大师** | Git Workflow Master | 分支策略、提交规范、协作流程 | Git管理 |
| **开发者布道师** | Developer Advocate | 社区建设、技术内容、开发者体验 | 开发者关系 |
| **自动化治理架构师** | Automation Governance Architect | 工作流自动化、业务流程自动化 | 自动化治理 |
| **工作流架构师** | Workflow Architect | 工作流设计、用户旅程、交互流程 | 工作流设计 |
| **项目经理/Scrum Master** | Project Manager / Scrum Master | 项目管理、敏捷实践、风险管理 | 项目管理 |
| **供应链与采购经理** | Supply Chain & Procurement Manager | 供应商管理、采购谈判、库存管理 | 供应链管理 |
| **运营总监/COO** | Chief Operating Officer | 企业运营、流程优化、KPI体系 | 运营管理 |

### L11 增长层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **小红书运营** | Xiaohongshu Operator | 种草笔记、达人合作、爆款内容 | 小红书运营 |
| **抖音策略师** | Douyin Strategist | 短视频策划、算法优化、直播带货 | 抖音运营 |
| **微信公众号运营** | WeChat Operator | 公众号内容、社群运营、裂变增长 | 微信运营 |
| **B站内容策略师** | Bilibili Strategist | UP主运营、弹幕文化、中长视频 | B站运营 |
| **私域流量运营师** | Private Domain Operator | 企微SCRM、社群运营、用户生命周期 | 私域运营 |
| **知识付费策划师** | Knowledge Commerce Strategist | 课程设计、内容定价、平台运营 | 知识付费 |
| **百度SEO专家** | Baidu SEO Specialist | 百度优化、百科/知道/贴吧生态 | 百度SEO |
| **Google SEO策略师** | Google SEO Strategist | Google搜索优化、技术SEO、国际内容 | Google SEO |
| **播客策略师** | Podcast Strategist | 小宇宙/喜马拉雅、音频制作、商业化 | 播客运营 |
| **短视频剪辑指导师** | Short Video Editing Coach | 剪映/PR/达芬奇、调色、音频、特效 | 视频剪辑 |
| **微信视频号运营** | WeChat Channels Operator | 视频号内容、直播运营、微信生态联动 | 视频号运营 |
| **知乎运营策略师** | Zhihu Strategist | 知乎问答、专栏写作、知乎好物 | 知乎运营 |
| **直播电商运营** | Live Commerce Operator | 直播策划、主播培养、选品排品 | 直播电商 |
| **智能搜索优化师** | Agentic Search Optimizer | WebMCP就绪度、AI Agent任务完成率 | AI搜索优化 |
| **AI引文策略师** | AI Citation Strategist | AEO/GEO、品牌在AI平台的可见性 | AI引文优化 |
| **海外社交媒体策略师** | Global Social Media Strategist | Twitter/X、LinkedIn、Reddit、Product Hunt | 海外社媒 |
| **微博/快手运营** | Weibo & Kuaishou Operator | 微博话题、快手短视频、热点营销 | 微博快手 |
| **淘宝/天猫/拼多多运营** | Taobao/Tmall/Pinduoduo Operator | 店铺运营、搜索排名、活动报名 | 电商运营 |

### L12 销售层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **客户拓展策略师** | Account Strategist | 大客户拓展、ABM策略、干系人关系 | 客户拓展 |
| **赢单策略师** | Deal Strategist | MEDDPICC资质审查、竞争定位、赢单规划 | 赢单策略 |
| **售前工程师** | Sales Engineer | 技术Discovery、Demo设计、POC执行 | 售前支持 |
| **Outbound策略师** | Outbound Strategist | 基于信号的Outbound、多渠道触达 | 外拓销售 |
| **Pipeline分析师** | Pipeline Analyst | Pipeline健康诊断、单子速度分析 | 销售分析 |
| **投标策略师** | Proposal Strategist | RFP解读、投标方案撰写、赢标叙事 | 投标管理 |
| **销售教练** | Sales Coach | 销售辅导、Pipeline Review、通话辅导 | 销售培训 |
| **Discovery教练** | Discovery Coach | 高阶Discovery技巧、问题设计、现状诊断 | 需求挖掘 |

### L13 投放层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **付费媒体审计师** | Paid Media Auditor | 广告账户审计、预算优化、效果诊断 | 媒体审计 |
| **广告创意策略师** | Creative Strategist | 广告文案、RSA优化、素材组设计 | 创意策略 |
| **社交广告策略师** | Paid Social Strategist | Meta/TikTok/LinkedIn/微信广告投放 | 社交广告 |
| **PPC竞价策略师** | PPC Strategist | 搜索竞价、关键词管理、Google Ads | PPC管理 |
| **程序化广告采买专家** | Programmatic Buyer | DSP、RTB、程序化展示广告 | 程序化购买 |
| **搜索词分析师** | Search Query Analyst | 搜索词挖掘、否定关键词、查询意图 | 搜索分析 |
| **追踪与归因专家** | Tracking & Attribution Specialist | 转化追踪、归因模型、数据整合 | 归因分析 |

### L14 人力层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **招聘专家** | Recruitment Specialist | 人才招聘、面试评估、雇主品牌 | 招聘管理 |
| **绩效管理专家** | Performance Management Specialist | 绩效考核、目标设定、反馈辅导 | 绩效管理 |
| **薪酬与福利设计顾问** | Compensation & Benefits Consultant | 薪酬体系、福利设计、激励机制 | 薪酬设计 |

### L15 学术层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **人类学家** | Anthropologist | 文化研究、用户洞察、社会行为 | 人类学研究 |
| **心理学家** | Psychologist | 心理分析、行为研究、认知科学 | 心理学应用 |
| **叙事学家** | Narratologist | 叙事分析、故事结构、内容策略 | 叙事研究 |
| **地理学家** | Geographer | 空间分析、地理数据、区域研究 | 地理分析 |
| **学习规划师** | Learning Planner | 学习路径、课程设计、能力发展 | 学习规划 |
| **文化智能顾问** | Cultural Intelligence Consultant | 跨文化沟通、文化适应、全球业务 | 文化智能 |

### L16 行业层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **医疗客服专家** | Healthcare Customer Service Expert | 医疗咨询、患者服务、医疗合规 | 医疗客服 |
| **医疗营销合规师** | Healthcare Marketing Compliance Specialist | 医疗广告合规、内容审核、风险管控 | 医疗营销 |
| **健康数据隐私专家** | Health Data Privacy Expert | 健康数据保护、HIPAA合规、隐私评估 | 健康数据 |
| **政务数字化售前顾问** | Government Digitalization Consultant | 政务方案、数字政府、售前支持 | 政务咨询 |
| **企业培训设计师** | Corporate Training Designer | 培训体系、课程开发、学习效果 | 企业培训 |
| **跨境电商运营专家** | Cross-border E-commerce Specialist | 跨境运营、海外仓储、国际物流 | 跨境电商 |
| **律师计费与工时专家** | Legal Billing & Timekeeping Expert | 律师计费、工时管理、费用优化 | 法律计费 |
| **律所客户接案专家** | Law Firm Client Intake Specialist | 客户接案、案件评估、客户关系 | 律所运营 |
| **法律文书审查专家** | Legal Document Review Specialist | 法律文书、合同审查、合规检查 | 法律文书 |

### L17 客户成功层

| 角色 | 英文名 | 核心功能 | 典型场景 |
|------|--------|---------|---------|
| **客户成功经理** | Customer Success Manager | 客户成功、续约管理、价值实现 | 客户成功 |
| **技术支持工程师** | Technical Support Engineer | 技术支持、问题解决、客户满意度 | 技术支持 |
| **危机公关顾问** | Crisis PR Consultant | 危机管理、公关策略、声誉修复 | 危机公关 |

---

## L3 - 工具层

> 职责：提供专用工具能力
> 触发条件：MCP开发、Web构建、演示创作、通讯、浏览器自动化、文档处理、数据可视化

### 3.1 文档处理 (document)

| 技能 | 英文名 | 功能 | 触发关键词 |
|------|--------|------|-----------|
| **docx** | Word Document | Word文档创建、编辑、转换 | Word doc、.docx、报告、备忘录 |
| **pdf** | PDF Processing | PDF处理（合并、拆分、OCR、表单填充） | .pdf、提取文本、合并PDF |
| **pptx** | PowerPoint | PPT创建、编辑、提取 | deck、slides、presentation、.pptx |
| **collab** | Document Collaboration | 文档协作编写 | 写文档、提案、技术规格、决策文档 |

### 3.2 数据处理 (data)

| 技能 | 英文名 | 功能 | 触发关键词 |
|------|--------|------|-----------|
| **visualization** | Data Visualization | 视觉设计、海报生成、PNG/PDF输出 | 海报、设计、视觉、canvas |
| **art** | Algorithmic Art | 算法艺术生成（p5.js） | 生成艺术、算法艺术、flow fields |
| **compress** | Text Compression | 文本压缩/解压（节省token） | caveman mode、less tokens、be brief |

### 3.3 开发工具 (devtool)

| 技能 | 英文名 | 功能 | 触发关键词 |
|------|--------|------|-----------|
| **mcp-dev** | MCP Development | MCP服务开发、技能创建 | MCP server、Model Context Protocol |
| **web-build** | Web Building | Web组件开发、前端设计 | web components、前端界面、React/Vue |
| **commit-msg** | Commit Message | 极简提交信息生成 | commit message、提交信息 |
| **code-review** | Code Review | 极简代码审查 | code review、审查代码 |

### 3.4 通讯协作 (comms)

| 技能 | 英文名 | 功能 | 触发关键词 |
|------|--------|------|-----------|
| **internal** | Internal Communication | 内部通讯、公告编写 | 内部通讯、状态报告、领导力更新、FAQ |
| **caveman** | Caveman Mode | 极简沟通模式（节省75% token） | caveman mode、talk like caveman |

### 3.5 浏览器 (browser)

| 技能 | 英文名 | 功能 | 触发关键词 |
|------|--------|------|-----------|
| **browser** | Browser Automation | 真实浏览器QA、截图、验证、数据抓取 | 打开网页、截图、抓取数据、测试网站 |

### 3.6 安全 (security)

| 技能 | 英文名 | 功能 | 触发关键词 |
|------|--------|------|-----------|
| **security** | Security Scanning | 安全扫描、敏感信息检测 | 安全扫描、检查漏洞、敏感信息 |

### 3.7 品牌 (brand)

| 技能 | 英文名 | 功能 | 触发关键词 |
|------|--------|------|-----------|
| **guidelines** | Brand Guidelines | 70+公司设计规范参考 | brand colors、设计规范、品牌标准 |

---

## 场景→技能链映射

| 场景类型 | 关键词特征 | 推荐技能链 | 说明 |
|---------|-----------|-----------|------|
| 新功能开发 | 创建、实现、开发、添加、做一个 | L1思维层 → L2角色层 → L3工具层 | 先分析再执行 |
| 问题修复 | 修复、bug、报错、异常、错误 | L1思维层 → L2角色层 | 先逆向分析再调试 |
| 架构决策 | 选型、方案、对比、设计、架构 | L1思维层 → L2角色层 | 多维度评估 |
| 代码审查 | 审查、review、检查、优化代码 | L1思维层 → L2角色层 | 先建立标准再检查 |
| 性能优化 | 优化、慢、卡顿、性能、提升 | L1思维层 → L2角色层 → L3工具层 | 分析→优化→验证 |
| 文档处理 | 文档、报告、表格、演示、写作 | L3工具层 | 直接路由到工具层 |
| 简单任务 | 改一下、小改动、微调、重命名 | L2角色层 | 跳过思维层，直接执行 |
| 学习研究 | 学习、了解、研究、解释、原理 | L1思维层 → L2角色层 | 先拆解再探索 |
| 信息获取 | 搜索、查询、最新、今天、现在 | L3工具层(browser) | 联网搜索获取实时信息 |

---

## 复杂度评估与路由策略

| 复杂度 | 判断标准 | 路由策略 |
|--------|---------|---------|
| 低 | 单文件修改、明确指令、无风险 | 直接路由到 L2角色层 |
| 中 | 多文件协调、需要设计、有一定风险 | L1思维层（简化）→ L2角色层 |
| 高 | 架构变更、多模块、高风险 | L1思维层（完整）→ L2角色层 → L3工具层 |

---

## 异常处理策略

| 异常类型 | 处理策略 | 降级方案 |
|---------|---------|---------|
| 意图识别失败 | 使用第一性原理拆解需求，询问用户确认 | 提供2-4个选项让用户选择 |
| 技能不存在 | 记录错误，尝试降级方案，告知用户 | 使用同层替代技能 |
| 技能执行失败 | 捕获错误信息，尝试替代技能 | 跳过该技能，继续执行后续 |
| 用户中断 | 保存已执行结果，提供部分输出 | 无 |
| 依赖缺失 | 检查技能依赖树，提示缺失项 | 手动补全依赖后重试 |

---

## 更新说明

- 新增技能：在对应层级表格中添加一行
- 删除技能：标记状态为"已废弃"，保留记录
- 修改触发条件：直接更新表格内容
- 场景映射调整：更新场景映射表
