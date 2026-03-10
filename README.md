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

---

## 2026-03-07

### ptracker
- 切换到 CLQ-26_note_display 分支
- 从远程 main 分支 rebase 更新代码
- 修改 query.py 和 trade.py，添加 note 显示功能（新增 format_note 函数，支持 --fullnote 参数）
- 提交代码并 push 到 origin
- 创建 PR #11: "CLQ-26: Add note display feature"
- 合并 PR 并删除远程分支
- CLQ-26: Add note display → 已完成

### rbt
- 查询仓库 PR 列表（5个已 merged）
- 查询未完成的 Jira：CLQ-22, CLQ-20, CLQ-19, CLQ-18, CLQ-4
- 查看当前分支：master
- 构建 rbt-0.7 whl 并安装到 quantdev conda 环境

### fq (factor_quote)
- 检查分支状态：main
- 软撤销 FuturesMdEngine commit（保留代码改动）
- CLQ-23: Develop Factor Quote Strategy → 进行中

---

## 2026-03-08

### fq (factor_quote)
- 检查分支状态：当前在 `CLQ-23_factor_quote_strategy`
- 提交并push现有修改：41个文件，2873行新增（local_rbt2/目录下的多个DMU和IC文件）
- CLQ-23: Develop Factor Quote Strategy → 进行中

### rbt
- 查询分支状态：当前在 `master`
- 创建 Jira issue: CLQ-27 - 增加更多DMU和IC
- 创建并切换到新分支：`CLQ-27_add_more_dmu_ic`
- CLQ-22: RBT save data in binary format → 已完成
- 查看本地修改（后应用户要求恢复）：mos_recover_ic.py（优化器改为CLARABEL）、constants.py（新增AG白银期货配置）

### 基础设施
- 处理 GLM-5 配额限制，切换到 MiniMax-M2.5 模型


---

## 2026-03-10

### factor_view (fv)
- 04:16 - 提交45个文件到CLQ-29_init_page分支并push
- 04:57 - 提交DataTable.vue和table.css修改，创建PR #1并合并到main
- 05:06 - 提交.gitignore和vite.config.js小修改到main
- 11:07 - 创建Jira CLQ-31: [fv] Add cell marking，创建分支CLQ-31_cell_marking
- 11:19 - 查看git diff：DataTable.vue新增200行单元格标记功能（1-9数字颜色标记）
- 13:35 - 提交单元格标记代码，创建PR #2: "[fv] Add cell marking feature"
- 13:36 - Squash合并PR #2到main，删除分支
- 14:28 - 提交backend/api.py、app.py、data_loader.py、frontend/styles/table.css修改到main
- 14:37 - 创建Jira CLQ-33: [factor_view] Beautify UI
- CLQ-31: Add cell marking → 已合并
- CLQ-33: Beautify UI → 待办

### ptracker (pt)
- 13:04 - 检查pt项目状态：main分支，working tree干净（只有1个未跟踪文件snapshot_cron.sh）
- 13:06 - 记录pt简称：更新TOOLS.md和MEMORY.md
- 13:06 - 创建Jira CLQ-32: [ptracker] Support futures positions，创建分支CLQ-32_futures_position

### 基础设施
- 13:38 - 记录Jira项目名规则：使用项目全名（factor_view, ptracker），更新MEMORY.md和AGENTS.md
- 更新AGENTS.md：Jira格式"[项目名] 内容"，分支格式"CLQ-<序号>_<描述>"
- 14:31 - 确认fv已push到origin（commit cde9c2c）

---

## 2026-03-09

### rbt
- 检查分支状态：CLQ-28_pnl_peu
- CLQ-28: 创建损益分析PEU Jira，创建分支 CLQ-28_pnl_peu
- 提交PEU分析文档（PEU分析文档.md）和pnl_estimate_unit.py完善（+353行）
- 创建FixedHoldingPEU（固定持有期限PEU），提交并推送到 origin
- CLQ-30: 创建PassThroughDMU Jira，创建分支 CLQ-30_passthrough_dmu
- 提交PassThroughDMU模块（pass_through_dmu.py + README.md + __init__.py），创建PR #6
- CLQ-28: 损益分析PEU → 进行中
- CLQ-30: PassThroughDMU → 已创建PR

### fq (factor_quote)
- 分支 CLQ-23_factor_quote_strategy
- 添加 .gitignore（忽略 __pycache__/、local_rbt2/、*.png 等）
- 取消跟踪 local_rbt/__pycache__/
- 提交并推送到远程

### factor_view (fv)
- 新建项目 ~/dev/factor_view
- 初始化仓库并推送到 GitHub: https://github.com/liuch288/factor_view
- CLQ-29: 创建初始化页面Jira，创建分支 CLQ-29_init_page
