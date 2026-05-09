# 防腐思维 - 常见陷阱

## 陷阱 1: 防腐层本身成了新腐化源

**问题**：翻译逻辑堆积过多，防腐层内部乱成一团。

❌ **Before**: ERPAdapter类500行，各种if-else判断老旧ERP的不同版本兼容
✅ **After**: 按ERP版本拆分为V1Adapter和V2Adapter，共用Translation接口，各自独立维护

**原因**：防腐层不是垃圾桶——它也需要设计。防腐层内部同样遵循高内聚低耦合。

---

## 陷阱 2: 过度防

**问题**：对接一个设计良好的RESTful API也建防腐层。

❌ **Before**: 对接GitHub API时，花了3天建了完整的GitHubACL层，但GitHub API设计已经非常干净
✅ **After**: 直接调用GitHub API，只在"GitHub特有的概念（如Pull Request）→内部概念（如Code Review）"处做轻量映射

**原因**：防腐层的成本（翻译+维护）是真实的。如果外部系统本身设计良好且与内部模型兼容，不需要隔离层。
