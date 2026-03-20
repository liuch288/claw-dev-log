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

## 2026-03-10

### factor_view (fv)
- 提交45个文件到CLQ-29_init_page分支并push
- 提交DataTable.vue和table.css修改，创建PR #1并合并到main
- 提交.gitignore和vite.config.js小修改到main
- 创建Jira CLQ-31: [fv] Add cell marking，创建分支CLQ-31_cell_marking
- 查看git diff：DataTable.vue新增200行单元格标记功能（1-9数字颜色标记）
- 提交单元格标记代码，创建PR #2: "[fv] Add cell marking feature"
- Squash合并PR #2到main，删除分支
- 提交backend/api.py、app.py、data_loader.py、frontend/styles/table.css修改到main
- 创建Jira CLQ-33: [factor_view] Beautify UI，创建分支CLQ-33_beautify_ui
- 提交DataTable.vue和table.css样式增强，push到CLQ-33_beautify_ui分支
- CLQ-31: Add cell marking → 已合并
- CLQ-33: Beautify UI → 待办

### ptracker (pt)
- 检查pt项目状态：main分支，working tree干净（只有1个未跟踪文件snapshot_cron.sh）
- 记录pt简称：更新TOOLS.md和MEMORY.md
- 创建Jira CLQ-32: [ptracker] Support futures positions，创建分支CLQ-32_futures_position
- 备份~/.ptracker到~/ptracker_backup/ptracker_backup_20260310_184953.tar.gz（71K）

### 基础设施
- 记录Jira项目名规则：使用项目全名（factor_view, ptracker），更新MEMORY.md和AGENTS.md
- 更新AGENTS.md：Jira格式"[项目名] 内容"，分支格式"CLQ-<序号>_<描述>"
- 确认fv已push到origin

## 2026-03-11

### rbt
- 创建 Jira CLQ-40: Adjust indicator formatting
- 创建分支 CLQ-40_adjust_indicator_formatting

### factor_store (fs)
- 添加项目结构和核心功能（factorstore/, tests/, examples/, pyproject.toml, setup.py, .gitignore, README.md）
- 提交到 CLQ-35_project_init 分支并 push 到远程
- 合并到 main 并 push
- 创建 PR #1: https://github.com/liuch288/factor_store/pull/1
- 删除本地和远程的 CLQ-35_PR 和 CLQ-35_project_init 分支，仅保留 main 分支
- 优化包配置：
  - pyproject.toml: 使用 dynamic 版本管理 dependencies 和 optional-dependencies
  - setup.py: 排除 tests、tests.*、examples 目录，安装时不包含测试和示例代码
- CLQ-35: Project init → 已完成

---

## 2026-03-12

### rbt
- CLQ-40: Adjust indicator formatting → pending
- 分支: CLQ-40_adjust_indicator_formatting

### factor_store (fs)
- CLQ-35: Project init → 已完成
- 提交代码（2个commit）：
  - a64c7f1 - Add project structure and documentation
  - faca93e - Update package configuration
- 完成项目结构和核心功能开发

---

## 2026-03-13

### rbt (rolled based trading)
- CLQ-46: 创建时间窗口DMU Jira，创建分支 CLQ-46_time_window_dmu
- 改进 TimePeriodDMU 的非交易时段处理（提交 5d69c3f）：
  - 移除冗余的 get_param_str() 方法（由基类处理）
  - 简化时间访问，假设 new_data.name 始终可用
  - 非交易时段返回 'Z' 而不是 None（更明确）
  - 更新测试用例以反映非交易时段的 Z 周期
  - 改进代码可读性和可维护性
- 修改文件：rbt/dmu/time_period_dmu.py（+6/-14 行）
- CLQ-46: Time window DMU → 进行中

---

## 2026-03-14

### 休息日
- 无开发工作

---

## 2026-03-15

### openclaw-control-center (OpenClaw Control Center)
- 环境确认阶段：
  - 确认 Gateway 可达：ws://127.0.0.1:18789（运行中）
  - 确认 OPENCLAW_HOME：~/.openclaw（默认值正确）
  - 检查 CODEX_HOME 和订阅快照（不存在，允许降级）
  - 确认 node/npm 版本：v22.22.0 / 10.9.4
  - 检查仓库完整性：package.json、src/runtime、src/ui 全部存在
- 项目安装阶段：
  - 运行依赖安装（npm install）
- 配置安全首次接入：
  - 复制 .env.example 创建 .env
  - 保持安全默认值：READONLY_MODE=true、LOCAL_TOKEN_AUTH_REQUIRED=true、APPROVAL_ACTIONS_ENABLED=false、IMPORT_MUTATION_ENABLED=false
  - 确认 GATEWAY_URL=ws://127.0.0.1:18789、UI_PORT=4310
  - CODEX_HOME 和 OPENCLAW_SUBSCRIPTION_SNAPSHOT_PATH 保持注释（降级模式）
- 验证安装阶段：
  - npm run build：✅ 成功
  - npm test：✅ 102/102 测试通过
  - npm run smoke:ui：✅ 通过
- 启动控制中心：
  - npm run dev：成功启动，Gateway 连接正常
  - 确认安全配置生效（readonlyMode、approvalActionsEnabled、importMutationEnabled 均为 false）
  - 心跳运行完成（dry-run 模式）

### rbt (rolled based trading)
- 检查 CLQ-46 讨论前的分支状态：master 分支，刚完成 CLQ-40
- 检查当前分支状态：
  - 分支：master
  - 未提交修改：README.md（版本号 0.7 → 0.8）
  - 修改内容：添加 TimePeriodDMU 的 Changelog 和架构说明
- 切换到 CLQ-40_adjust_indicator_formatting 分支进行开发
- CLQ-40: Adjust indicator formatting → 进行中

---

## 2026-03-16

### rbt (rolled based trading)
- 从 CLQ-40_adjust_indicator_formatting 分支切换到 CLQ-28_pnl_peu 分支
- Stash CLQ-40 分支的 README.md 修改
- 从 origin/master rebase 更新代码（2个commits rebase成功）
- 修改 PEU 相关文件（fixed_holding_peu.py, pnl_estimate_unit.py，+2/-2 行）
- Commit 并 push 到 CLQ-28_pnl_peu 分支（d4828ab）
- 创建 PR #9 并用 squash 模式合并
- 切换回 master 分支并 pull 最新代码（679c0d3..7e4b3cd）
- 合并后新增 4 个文件，共 506 行代码：
  - 新增 `rbt/peu/PEU分析文档.md`
  - 新增 `rbt/peu/fixed_holding_peu.py`（153 行）
  - 更新 `rbt/peu/__init__.py`
  - 更新 `rbt/peu/pnl_estimate_unit.py`（+95/-4）
- CLQ-28: 损益分析PEU → 已完成

### ai_intro
- Commit 并推送 ai-ppt 目录（+343 行）
- Commit 并推送 ai-ppt/index.html 修改（+2/-22 行）
- 再次 commit 并推送 ai-ppt/index.html 修改（+95/-276 行）
- 抹掉未提交的修改（git restore ai-ppt/index.html）
- 退回到上次提交（git reset --soft HEAD~1）
- Stash 改动，pull 更新（ae86d10..d0e9abd），不恢复 stash
- 删除 ai-ppt 目录并 commit push（-142 行）

### fq (factor_quote)
- CLQ-23: Develop Factor Quote Strategy → 标记为已完成

### fc (factor_calculator)
- 创建 Jira CLQ-47: 支持制定指标计算保存
- 创建分支 CLQ-47_support_factor_calculation_save
- 创建 Jira 长篇故事（Epic）CLQ-48: Factor Calculator
- 创建新项目 ~/dev/factor_calculator
- 初始化 git 仓库，添加远程 origin
- 创建 README.md 和 .gitignore
- 初始提交并推送到 main（+38 行）

### 基础设施
- 更新 TOOLS.md：新增 fc 项目简称（factor_calculator）

---

## 2026-03-17

### rbt (rolled based trading)
- CLQ-51: Add contract information registration (#12)
- 新增合约信息注册功能，版本升级 0.7 → 0.8
- 修改 4 个文件，新增 87 行代码：
  - 新增 `rbt/md/futures_md_engine.py`（45 行）- 合约信息注册模块
  - 更新 `rbt/strategy.py`（+24 行）- 策略合约注册支持
  - 更新 `rbt/unit.py`（+17 行）- 单元合约配置支持
  - 更新 `README.md`（版本号更新）
- 创建 PR #12 并合并
- CLQ-51: Add contract information registration → 已完成

### fc (factor_calculator)
- CLQ-50: Add basic factor calculator structure
- 完成因子计算器基础架构开发
- 修改 11 个文件，新增 2059 行代码：
  - 新增 `factor_calculator/core.py`（403 行）- 核心因子计算引擎
  - 新增 `factor_calculator/factory.py`（372 行）- 因子工厂模式实现
  - 新增 `factor_calculator/cli.py`（171 行）- 命令行接口
  - 新增 `examples/example_usage.py`（222 行）- Python 使用示例
  - 新增 `examples/example_usage.ipynb`（246 行）- Jupyter 使用示例
  - 新增 `tests/test_core.py`（211 行）- 核心功能测试
  - 新增 `tests/test_factory.py`（216 行）- 工厂模式测试
  - 更新 `factor_calculator/__init__.py`（+32 行）
  - 更新 `pyproject.toml`（+22 行）- 依赖配置
- CLQ-50: Add basic factor calculator structure → 已完成

---

## 2026-03-18

### rbt (rolled based trading)
- CLQ-51: Add contract information registration
- 解决本地 merge conflicts：README.md 中英文冲突，保留中文版本
- CLQ-51, CLQ-53 任务状态更新为"已完成"
- 清理 GitHub 分支：删除 CLQ-51_add_contract_information_registration 和 CLQ-53_resultdb-base-class 的远程和本地分支
- CLQ-54: Create factor store result db
  - 创建 Jira issue，parent 为 CLQ-4 (RBT)
  - 创建并切换到分支 CLQ-54_factor-store-result-db
  - 实现 FactorStoreResultDB（rbt/result_db/fs_result_db.py，202 行）
  - 提交并推送到远程（commit 9d5dfc7）
- CLQ-51: Add contract information registration → 已完成
- CLQ-53: Extract resultdb base class → 已完成
- CLQ-54: Create factor store result db → 进行中

### factor_view (fv)
- CLQ-55: Add column filtering functionality
  - 创建 Jira issue，parent 为 CLQ-39 (factorview)
  - 切换到 main 分支并 pull 最新代码
  - 创建并切换到分支 CLQ-55_column-filtering
  - 清理文件：删除 AI_Model_Timeline_2026.md
- CLQ-55: Add column filtering functionality → 待办

### 基础设施
- **PR 合并规则强化**：特别强调 PR 合并必须使用 squash merge 扁平化方式
- 更新以下核心文件：
  - SOUL.md：添加醒目的 "🚨 PR 合并规则" 部分，包含正确和错误的命令对比
  - MEMORY.md：在工作流程总结中强化规则
  - AGENTS.md：在 Git/Jira 操作部分添加规则
- 规则内容：`gh pr merge <PR_NUMBER> --squash`（正确）vs `gh pr merge <PR_NUMBER> --merge`（错误）

---

## 2026-03-19

### rbt (rolled based trading)
- CLQ-54: Create factor store result db (#14)
- 合并 PR #14 到 master，新增 FactorStoreResultDB 模块
- 修改 5 个文件，新增 182 行代码：
  - 新增 `rbt/result_db/fs_result_db.py`（176 行）- FactorStoreResultDB 实现
  - 更新 `rbt/result_db/__init__.py`（+3/-1 行）
  - 更新 `.gitignore`（忽略所有 ipynb 文件）
- CLQ-54: Create factor store result db → 已完成

### fc (factor_calculator)
- 更新 core 和 tests 以适配 FsResultDB
- 修改 2 个文件，新增 108 行代码：
  - `factor_calculator/core.py`（+63/-18 行）
    - 参数 `db_directory` 改为 `root_path`（向后兼容保留 alias）
    - 新增 `frequency` 参数（默认 "tick"）
    - 默认使用 FsResultDB 而不是旧的 ResultDB
    - 支持从本地 rbt 开发版本导入 FsResultDB
  - `tests/test_core.py`（+85/-22 行）
    - 更新测试以使用 FactorStore 格式保存和读取
    - 修复 get_existing_factors 返回格式（factor 名称而非列名）
- 状态：进行中（适配 FsResultDB）

---

## 2026-03-20

### factor_view (fv)
- CLQ-55: Column filtering feature（3次提交）
- 创建 PR #4（待合并）
- 修复暗色模式样式

### factor_calculator (fc)
- CLQ-50: develop basic version
- 更新示例文档（新增因子单元，API 变更：db_directory→root_path）
- Commit + Push（未创建 PR）
