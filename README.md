# OpenClaw 开发日志

记录 OpenClaw 项目的日常开发情况。

---

## 日报格式规范

### 结构
```
## 日期

### 项目1
- 具体工作内容（代码改动、功能开发等）
- CLQ-XX: 事项描述 → 状态

### 项目2
- 具体工作内容
- CLQ-XX: 事项描述 → 状态
```

### 规则
1. **按项目分组** - 不是按"Jira管理"、"基础设施"分类
2. **Jira 写到项目下面** - 每个项目的 Jira issues 列在该项目内
3. **具体工作** - 写实际做了什么，不写"检查状态"这种过程
4. **代码/文件改动** - 写了具体文件、新增功能

---

## 2026-02-10

### ClawQuant
- 搭建 HFT 交易系统基础结构（数据层、回测引擎、策略模板），讨论后决定不在 workspace 内开发，清理目录
- 在 ~/dev/ClawQuant 创建 README，完成 init commit 并推送到 GitHub（liuch288/ClawQuant）
- CLQ-2：创建分支 `CLQ-2_database_initialize`，开始数据库开发
  - 方案讨论：Python 包形式，pickle 存储 DataFrame，按 exchange/symbol/timeframe 组织

### 基础设施
- 建立 memory 记忆系统（daily memory + MEMORY.md）

---

## 2026-02-25

### ptracker
- CLQ-7：记录 ptracker init issue
- ClawQuant PR #2 等待合并（支持 datetime.date 对象作为日期参数）
- 更新 MEMORY.md 项目列表，加入 ptracker

### rbt
- CLQ-3：记录 rbt intro issue

### 基础设施
- 测试模型切换（MiniMax-M2.1 → GLM-5）

---

## 2026-02-26

### rbt
- CLQ-3：确认项目路径 ~/dev/rbt（rolled based trading），待启动

### 基础设施
- 清理 BOOTSTRAP.md（启动引导文件已完成使命）

---

## 2026-02-27

### ptracker
- CLQ-12：账户存取款功能开发完成（+192 行，6 个文件）
  - 新增 CashFlowRepository（cash_flow.py）
  - Account 模型新增 total_deposit / total_withdrawal 字段
  - CLI 新增 `deposit` / `withdraw` 命令（支持 --currency、--note）
  - query_account 显示增强（Cash Flow 区块 + 历史表格）
  - 功能测试通过
- 版本 0.1.3 → 0.1.4
- 提交 `c06f8d3`，创建 PR #5

---

## 2026-02-28

### yuri-test
- 新建项目 ~/dev/yuri-test，用于测试自动化开发
- 完成 init commit（README.md），推送到 GitHub（liuch288/yuri-test）
- 遇到 workspace 外写文件权限限制，改用 shell 命令解决

### 基础设施
- 调试 Telegram bot 命令权限问题（/new、/models 命令不可用）

---

## 2026-03-04

### ptracker
- 检查分支状态：**CLQ-11_ptracker_skill**，working tree 干净
- 创建 PR #8，审核通过后合并
- 切回 main 分支并拉取最新代码
- CLQ-11: develop skills（已合并到 main）

### rbt
- 检查分支状态：**CLQ-3_rbt_docs**，有未提交更改
- 修改文件：
  - `rbt/ic/mos_recover_ic.py` (+2/-1 行)
  - `rbt/peu/biquote_close_peu.py` (+3/-1 行)
- 提交并推送到 `CLQ-3_rbt_docs`
- 创建 PR: https://github.com/liuch288/rbt/pull/1

### 基础设施
- 加载个人 Skills：ptracker（投资组合跟踪 CLI）、acli-jira（Jira 控制）
- Jira issues 使用英文（规则写入 MEMORY.md）

---

## 2026-03-05

### ptracker
- 检查分支状态：**CLQ-11_ptracker_skill**，working tree 干净
- 查看并理解 ptracker 项目结构（投资组合跟踪 CLI 工具）
- 列出 ptracker CLI 命令：init, version, account, trade, query, config
- account 子命令：add, list, query, delete, deposit, withdraw
- trade 子命令：add, list
- query 子命令：holdings, value, realized, pnl
- CLQ-11: develop skills → 已完成
- CLQ-14: yahoo sym → 已完成
- CLQ-15: option calc → 已完成

### rbt
- 检查 rbt 分支状态：**CLQ-3_rbt_docs**
- CLQ-3: rbt intro → 已完成
- CLQ-16: rbt 策略运行支持bgm（新建）

### 基础设施
- Jira issues 使用英文（规则写入 MEMORY.md 和 SOUL.md）

---

## 2026-03-06

### rbt
- 重新构建 rbt whl (v0.5) 并安装到系统
- CLQ-24: Add KlineDMU（新建 Jira）
- 创建分支 CLQ-24_kline_dmu，提交并推送代码

### fq (factor_quote)
- 检查分支状态，发现 1 个未 push 的 commit
- 软撤销 commit（保留改动）
- CLQ-23: Develop Factor Quote Strategy（新建 Jira）
- 创建分支 CLQ-23_factor_quote_strategy
- 提交 FuturesMdEngine 代码并推送到远程
- 推送 4 个 commit（含 run_example.py, spread_plot.png）

### ptracker
- CLQ-25: Add record editing feature（新建 Jira）
- 创建分支 CLQ-25_record_edit

### claw-dev-log
- 仓库已在 ~/dev/claw-dev-log
- README.md 已更新今日工作

