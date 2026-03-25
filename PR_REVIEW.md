# PR Review 记录

记录每次 Code Review 的结果。

| 日期 | Jira ID | 项目 | PR | 审核结果 | 严重问题 | 警告 | 建议 | 备注 |
|------|---------|------|-----|----------|----------|------|------|------|
| 2026-03-20 | CLQ-55 | factor_view | [CLQ-55: Column filtering feature](https://github.com/liuch288/factor_view/pull/4) | ⚠️ 建议修改 | 1 | 2 | 2 | 需修复 end 变量重复赋值 Bug |
| 2026-03-25 | CLQ-64 | rbt | [CLQ-64: Provide dependency factor information](https://github.com/liuch288/rbt/pull/19) | ✅ 可合并 | 0 | 1 | 0 | 方法重复定义已修复 |
| 2026-03-25 | CLQ-64 | rbt | [CLQ-64: Provide dependency factor information](https://github.com/liuch288/rbt/pull/19) | ❌ 需修复 | 1 | 0 | 0 | 方法重复定义 |
| 2026-03-24 | CLQ-60 | rbt | [CLQ-60: Adjust FuturesMdEngine parameters and Unit auto-naming](https://github.com/liuch288/rbt/pull/17) | ✅ 可合并 | 0 | 1 | 2 | FuturesMdEngine 构造简化，需确认导出 |
| 2026-03-24 | CLQ-63 | rbt | [CLQ-63: Register contract info](https://github.com/liuch288/rbt/pull/18) | ✅ 可合并 | 0 | 0 | 4 | 合约参数统一注入 |
| 2026-03-24 | CLQ-50 | factor_calculator | [CLQ-50: Develop basic version](https://github.com/liuch288/factor_calculator/pull/1) | ✅ 可合并 | 0 | 0 | 5 | 因子计算工具 |
| 2026-03-21 | CLQ-62 | factor_store | [CLQ-62: Remove cast_to_float64 call in save method](https://github.com/liuch288/factor_store/pull/5) | ⚠️ 建议修改 | 0 | 2 | 2 | 有条件通过，需确认历史数据无类型不一致 |

---

## 审核标准

- ✅ 可合并: 代码质量良好，仅有轻微建议
- ⚠️ 建议修改: 存在一些问题，建议修复后合并
- ❌ 需修复: 存在严重问题，必须修复后才能合并

---

*由 Big Brother 自动生成*
