# PR Review 记录

| 日期 | Jira ID | 项目 | PR | 审核结果 | 严重问题 | 警告 | 建议 | 备注 |
|------|---------|------|-----|----------|----------|------|------|------|
| 2026-04-24 | CLQ-122 | factor_calculator | [CLQ-122: Remove PositionPnldMU from calculation process](https://github.com/liuch288/factor_calculator/pull/9) | ✅ 可合并 | 0 | 1 | 0 | 利用 rbt CLQ-123 新特性（Strategy(position_pnl_dmu_class=None)）移除 position tracking 开销；新增 CHANGELOG.md；version bump 0.1.0→0.1.2（直接跳过了 0.1.1）；警告：版本号跳级幅度较大（0.1.0→0.1.2），且 0.1.1 在 CHANGELOG 中无实际内容，仅标注 version aligned，建议确认版本管理策略 |
| 2026-04-24 | CLQ-123 | rbt | [CLQ-123: Allow Strategy without position PnldMU](https://github.com/liuch288/rbt/pull/44) | ✅ 可合并 | 0 | 0 | 1 | position_pnl_dmu_class 从 PositionPnlDMU 改为 None 默认，None 时跳过 position pnl 相关计算；轻微：strategy.py 中 PositionPnlDMU 的导入语句位置不变，但类已不再是默认参数，后续使用需注意 |
| 2026-04-24 | CLQ-120 | contextum | [CLQ-120: Add event dashboard functionality](https://github.com/liuch288/contextum/pull/10) | ⚠️ 建议修改 | 0 | 2 | 3 | 新增事件看板（/events 列表 + /events/<id> 详情页），卡片式布局支持分类筛选；event_detector 新增美伊战争匹配规则；警告：events_page() 在循环内逐个 event 开 2 个 raw sqlite3 连接查 news（N+1×2 问题），应改为批量查询；raw sqlite3.connect 未用 with/try-finally 保护，异常时连接泄漏；轻微：fiscalRe 正则硬编码前端分类脆弱；_get_event_stats 异常返回值缺 total_events 键可能导致模板错误；import 语句多处在函数体内 |
| 2026-04-23 | CLQ-117 | factor_calculator | [CLQ-117: Support main contract calculation](https://github.com/liuch288/factor_calculator/pull/8) | ✅ 可合并 | 0 | 1 | 2 | re-review：新增 dominant.py 别名解析（TL01→TL品种+01标记）+ expand_to_dominant_dates；core.py 新增 _run_strategy_multi_day_dominant；parse_alias 正则从 {2,4} 改为 {1,4} 支持单字母品种；version bump 0.1.0→0.1.1；警告：calculate() 中 self._dominant_expansion 实例变量在并发调用场景下有 race condition 风险，建议改为参数传递；轻微：calculate() docstring 空白行格式（Args 前有多余空行）；dominant.py 末尾缺少换行符 |
| 2026-04-23 | CLQ-116 | rbt | [CLQ-116: Integrate market-specs package](https://github.com/liuch288/rbt/pull/43) | ⚠️ 建议修改 | 0 | 1 | 1 | 合约信息外部化：删除util/constants.py中600+行instrument_info字典，改为委托market_specs.get_info()；STOCK逻辑保留；新增market-specs为显式依赖；警告：market-specs未发布PyPI，当前直接pip install rbt会失败，需先发布market-specs到PyPI或改用git URL依赖；轻微：util.py股票分支tick_size=0.01是硬编码，digits=3不变，与真实股票精度可能有差异 |
| 2026-04-23 | CLQ-115 | market-specs | [CLQ-115: Initialize market-specs project](https://github.com/liuch288/market-specs/pull/1) | ✅ 可合并 | 0 | 1 | 1 | re-review：dominant.py已移除EXCHANGE_MAP导入；_load_data()新增文件缺失保护（warnings.warn+空字典）；警告：constants.py中EXCHANGE_MAP定义仍在但无任何模块使用/导出（局部死代码，不影响功能）；轻微：CSV数据版权未说明 | 2026-04-22 | CLQ-111 | rbt | [CLQ-111: Accelerate BiquotePEU performance](https://github.com/liuch288/rbt/pull/41) | ✅ 可合并 | 0 | 1 | 1 | 性能优化核心改动：numpy数组替代iterrows、预扫描极值跳过循环、_get_volume_before_from_values直接接收数组减少Series索引开销；MosRecoverIC新增_fallback_result、trade_size==1直接判断避免cvxpy求解；MoSplitDMU新增highest_buy_px/lowest_sell_px供预判；警告：构造函数参数不再有默认值（breaking change已在PR描述说明）；BiquotePEU已优化但BiquoteClosePEU/BiquoteStopClosePEU仍用iterrows未同步优化 |
| 2026-04-22 | CLQ-110 | rbt | [CLQ-110: Add comprehensive contract information](https://github.com/liuch288/rbt/pull/40) | ✅ 可合并 | 0 | 2 | 1 | 合约信息从4个国债期货扩展至87个期货品种，覆盖6大交易所；全项目black格式化；version bump 0.22→0.23；警告：md_dmu.register_contract_info只存hands，tick_size/digits被忽略，与其他unit不一致；instrument_info结构变更（T/TF/TL/TS新增name/exchange字段），需确认调用方是否依赖旧结构 |
| 2026-04-21 | CLQ-108 | factor_calculator | [CLQ-108: Prepare agent usage examples and skill](https://github.com/liuch288/factor_calculator/pull/6) | ✅ 可合并 | 0 | 1 | 3 | 新增 factor_calculator_skill（skill文档+6个示例）；cli.py --db改为可选；删除旧示例文件；pyproject.toml新增包扫描配置 |
| 2026-04-20 | CLQ-105 | contextum | [CLQ-105: Support dynamic refresh time](https://github.com/liuch288/contextum/pull/9) | ✅ 可合并 | 0 | 2 | 3 | Dashboard 新增事件统计面板+一键生成审查建议；动态抓取间隔算法（根据最新两条新闻时间差计算）；_get_event_stats 异常时静默返0可能误导；trigger_review 无并发保护 |
| 2026-04-20 | CLQ-104 | contextum | [CLQ-104: Add news auto assignment event](https://github.com/liuch288/contextum/pull/8) | ⚠️ 建议修改 | 0 | 4 | 2 | 排序字段变更（processed_at→published_at）无说明；N+1 query；批量接受无防重保护；run_full_analysis并发无锁 |
| 2026-04-20 | CLQ-103 | contextum | [CLQ-103: event data correction](https://github.com/liuch288/contextum/pull/7) | ✅ 可合并 | 0 | 3 | 3 | 新增事件审查系统（event_updater.py 485行）；Dashboard `/reviews` 页面支持接受/拒绝/重新分析；EventReview 模型+pending_reviews 机制设计合理；backup.py 新增 events.db 备份；主要警告：run_review limit=0 时先查所有 events 再切片效率可优化；_exec_merge 重复 news_id 场景直接丢弃 link 而非合并内容；approve_review 异常时 session.rollback 后返回 False 但 review.status 已是"pending"（因为未到 commit）；轻微建议：REVIEWS_TEMPLATE 变量名全大写可改为 ReviewsTemplate 驼峰；review 拒绝时未清理 EventReview row（status 变 rejected 但记录残留 |
| 2026-04-17 | CLQ-99 | contextum | [CLQ-99: Add event recognition and classification](https://github.com/liuch288/contextum/pull/5) | ⚠️ 建议修改 | 0 | 2 | 2 | 新增事件识别分类系统（event_detector/analyzer/manager/db/models），独立 events.db；seed events 预定义14个重大事件；支持双轮扫描（首次+重扫 skipped）；parse_json_response 增强截断恢复；timeout 60s→180s，max_tokens 16384→65536；主要警告：parse_json_response unescaped quote 检测有 bug（只检查前一个字符是否为单反斜号，\\\\" 场景漏检）；N+1 query（_fetch_unanalyzed_news/_fetch_skipped_news 每条 news 单独查 tag）；建议：fetch 批量查所有 tags 避免 N+1；风格统一（中英文混用） |
| 2026-04-17 | CLQ-102 | contextum | [CLQ-102: Add one-click start command](https://github.com/liuch288/contextum/pull/6) | ✅ 可合并 | 0 | 0 | 2 | 启动验证机制完善（sleep 1 + kill -0确认进程存活）；优雅关闭（10s超时+SIGKILL）；使用python -m启动更规范；轻微建议：set -e改为set -euo pipefail保持一致；确认python命令在目标环境可用（建议python3） |
| 2026-04-17 | CLQ-102 | contextum | [CLQ-102: Add one-click start command](https://github.com/liuch288/contextum/pull/6) | ⚠️ 建议修改 | 0 | 2 | 2 | start.sh逻辑清晰，支持start/stop；logs/写入.gitignore规范；轻微问题：python未用python3可能Mac兼容性；建议：补充依赖检查（pip install/npm install）、启动后加短暂sleep再检查进程是否存活、frontend依赖backend启动成功才继续 |
| 2026-04-17 | CLQ-96 | factor_calculator | [CLQ-96: Support cross-day unit execution](https://github.com/liuch288/rbt/pull/38) | ✅ 可合并 | 0 | 1 | 1 | 适配RBT v0.22新API，重构干净代码量从77行减至33行；_build_strategy()封装策略构建逻辑清晰；移除_reset_units_end_of_day()由Strategy.run()接管日终重置合理；轻微：List未使用；建议：确认Strategy.run(sym,dates)中每个date是否都调用了prepare_data（多日场景） |
| 2026-04-17 | CLQ-96 | rbt | [CLQ-96: Support cross-day unit execution](https://github.com/liuch288/rbt/pull/38) | ⚠️ 建议修改 | 0 | 1 | 2 | 多日运行+日终重置设计合理；_run_single_day提取干净；_ensure_contract_info缓存避免重复查询；建议：删除未使用的List import；单日run场景下on_end_of_day()行为可确认是否符合预期；prepare_data(sym,date)调用但md_engine可能未实现该方法 |
| 2026-04-17 | CLQ-96 | rbt | [CLQ-96: Support cross-day unit execution](https://github.com/liuch288/rbt/pull/38) | ⚠️ 建议修改 | 0 | 1 | 2 | 代码本身结构规范、逻辑清晰；仅余轻微问题：AtrDMU.make_decision直接访问previous_result["MdDMU_v0__mid"]未做KeyError保护；KlinePatternDMU窗口未填满时返回旧pattern可能误导；PR描述和版本号问题用户表示不重要 |
| 2026-04-17 | CLQ-96 | rbt | [CLQ-96: Support cross-day unit execution](https://github.com/liuch288/rbt/pull/38) | ⚠️ 建议修改 | 0 | 2 | 2 | 多日计算核心逻辑完整，测试覆盖充分（314行）；主要问题：_generate_date_range 包含所有日历日（含周末/假日），非交易日会触发不必要的失败；cli.py 参数验证与 core.py 重复，可提取公共方法；fail_fast + 日终重置逻辑正确 |
| 2026-04-17 | CLQ-96 | rbt | [CLQ-96: Support cross-day unit execution](https://github.com/liuch288/rbt/pull/38) | ✅ 可合并 | 0 | 1 | 1 | Unit 基类新增 on_end_of_day() 钩子，8 个 DMU 子类实现日终重置，设计干净；mo_split_dmu 正确处理 recover_ic 可能为 None 的情况；TrendDMU 重置 last_val=0.0 可能丢失跨日趋势连续性，建议确认是否符合业务预期；version bump 0.21→0.22 + changelog 完整 |
| 2026-04-16 | CLQ-98 | contextum | [CLQ-98: Support real-time news processing](https://github.com/liuch288/contextum/pull/4) | ✅ 可合并 | 0 | 2 | 2 | re-review：backup.py 已改用 with 语句管理连接，中等问题已修复；仅余 process_history*.py import 顺序不规范、processor.py 重试计数偏差两处轻微警告 |
| 2026-04-16 | CLQ-93 | contextum | [CLQ-93: Enhance JSON parsing with Chinese quotes and truncation support](https://github.com/liuch288/contextum/pull/3) | ✅ 可合并 | 0 | 2 | 2 | JSON 解析增强（中文引号+截断恢复）逻辑完整；max_tokens 2048→16384；移除了 OpenAI 兼容 API 和 provider 切换逻辑，代码更简洁；processor.py prompt 更新中文引号说明；仅余轻微警告 |
| 2026-04-15 | CLQ-92 | contextum | [CLQ-92: Add basic processing agent](https://github.com/liuch288/contextum/pull/2) | ⚠️ 建议修改 | 1 | 2 | 4 | Processor 核心功能已实现，但集成代码全部注释未启用；API key 前缀明文日志；.env.example 硬编码 GLM-4.7 模型名；dashboard 新闻数从 20 改为 10 |
| 2026-04-13 | CLQ-91 | contextum | [CLQ-91: Add project framework](https://github.com/liuch288/contextum/pull/1) | ✅ 可合并 | 0 | 1 | 3 | 框架初始化 PR，结构清晰；Source.fetch_interval 字段在 scheduler 中未被使用，建议确认用途或清理；news_fetcher 每条 commit 可考虑批量；.env.example/.gitignore 规范 |
| 2026-04-12 | CLQ-88 | factor_view | [CLQ-88: Fix GuidePage 500 error](https://github.com/liuch288/factor_view/pull/6) | ✅ 可合并 | 0 | 1 | 2 | toFixed+parseFloat 可能丢精度建议改为 toFixed；双下划线分隔符与 CLQ-83 一致；小数精度控制实现完整 |
| 2026-04-11 | CLQ-87 | rbt | [CLQ-87: Adapt PEU subclasses to new framework](https://github.com/liuch288/rbt/pull/36) | ✅ 可合并 | 0 | 1 | 2 | re-review：代码更新后，排单量逻辑改进（多档探测替代硬编码5档）；仅余轻微警告 |
| 2026-04-11 | CLQ-87 | rbt | [CLQ-87: Adapt PEU subclasses to new framework](https://github.com/liuch288/rbt/pull/36) | ⚠️ 建议修改 | 0 | 3 | 1 | Strategy.py pd.concat 列名冲突风险；SimpleBiquotePEU 价格来源语义变化；PR 描述与代码不符（称移除 Order 类但仍使用） |
| 2026-04-10 | CLQ-83 | factor_view | [CLQ-83: Add dynamic product/contract selection in guide page](https://github.com/liuch288/factor_view/pull/5) | ⚠️ 建议修改 | 0 | 1 | 2 | COLUMN_REGEX 从单下划线改为双下划线分隔符，需确认历史数据兼容性；建议：补全 GuidePage 组件的快照测试 |
| 2026-04-10 | CLQ-86 | rbt | [CLQ-86: Pass unit results to PEU estimate method for dependency support](https://github.com/liuch288/rbt/pull/35) | ⚠️ 建议修改 | 0 | 2 | 1 | fixed_holding_peu.py 仍用旧签名 estimate(data, previous_result)；FsResultDB 与 PklResultDB 对 factors=None 行为不一致；严重问题：PEU 子类签名不一致，需同步更新 |
| 2026-04-10 | CLQ-81 | rbt | [CLQ-81: Add dynamic level detection for market order recovery](https://github.com/liuch288/rbt/pull/34) | ✅ 可合并 | 0 | 2 | 1 | MoSplitDMU.md_type 默认值变更可能导致兼容性问题；recover_mo_core_dynamic 未设置求解器参数 |
| 2026-04-09 | CLQ-82 | rbt | [CLQ-82: Extract order splitting module into DMU](https://github.com/liuch288/rbt/pull/33) | ✅ 可合并 | 0 | 2 | 1 | MoIntentionDMU 构造参数变更需确认兼容性；MdEngine 不再自动恢复市价单 |
| 2026-04-09 | CLQ-79 | rbt | [CLQ-79: Optimize biquotepeu](https://github.com/liuch288/rbt/pull/32) | ✅ 可合并 | 0 | 1 | 2 | 文档整理，接口统一；移除了 active_closing_time 参数需确认兼容性 |
| 2026-04-09 | CLQ-77 | factor_calculator | [CLQ-77: Support lrbt](https://github.com/liuch288/factor_calculator/pull/3) | ✅ 可合并 | 0 | 1 | 0 | pkgutil 遍历可考虑加限制条件 |
| 2026-03-31 | CLQ-78 | rbt | [CLQ-78: Add minmax IC](https://github.com/liuch288/rbt/pull/31) | ⚠️ 建议修改 | 0 | 1 | 2 | calculate() 未调用 super()；建议删除注释代码；补充 docstring |
| 2026-03-29 | CLQ-76 | lrbt | [CLQ-76: Add lrbt project framework](https://github.com/liuch288/lrbt/pull/1) | ✅ 可合并 | 0 | 1 | 2 | 建议添加 __main__.py + pyproject.toml |
| 2026-03-29 | - | ptracker | [#12: Add snapshot cron script](https://github.com/liuch288/ptracker/pull/12) | ✅ 可合并 | 0 | 2 | 1 | 硬编码路径；建议用配置文件 + 添加错误处理 |
| 2026-03-27 | CLQ-74 | rbt | [CLQ-74: Fix release issue](https://github.com/liuch288/rbt/pull/29) | ✅ 可合并 | 0 | 0 | 0 | 添加 contents:write 权限，改进版本提取 |
| 2026-03-27 | CLQ-71 | rbt | [CLQ-71: Fix release error](https://github.com/liuch288/rbt/pull/26) | ✅ 可合并 | 0 | 0 | 1 | 动态获取默认分支，正则解析版本 |
| 2026-03-27 | CLQ-70 | rbt | [CLQ-70: Adapt to release](https://github.com/liuch288/rbt/pull/25) | ✅ 可合并 | 0 | 0 | 1 | 建议统一分支名为 master |
| 2026-03-27 | CLQ-73 | rbt | [CLQ-73: Fix pipeline bug](https://github.com/liuch288/rbt/pull/28) | ✅ 可合并 | 0 | 0 | 0 | 修复 action-gh-release v2 参数名 |
| 2026-03-27 | CLQ-72 | rbt | [CLQ-72: Continue fixing pipeline error](https://github.com/liuch288/rbt/pull/27) | ⚠️ 建议修改 | 0 | 1 | 1 | 分支名回退为硬编码；env 变量用途不明 |
| 2026-03-27 | CLQ-69 | rbt | [CLQ-69: Deploy RBT pipeline](https://github.com/liuch288/rbt/pull/23) | ✅ 可合并 | 0 | 1 | 0 | GitHub Actions CI/CD 配置正确 |
| 2026-03-26 | CLQ-65 | factor_calculator | [CLQ-65: Fix previous result and BGM functionality](https://github.com/liuch288/factor_calculator/pull/2) | ✅ 可合并 | 0 | 1 | 0 | docstring 描述与实际用途不一致；CLI 破坏性变更无缓冲期 |
| 2026-03-26 | CLQ-68 | rbt | [CLQ-68: Fix FsResultDB bugs](https://github.com/liuch288/rbt/pull/22) | ⚠️ 建议修改 | 0 | 1 | 0 | 与 #20 改动方向冲突，需统一设计 |
| 2026-03-25 | CLQ-67 | rbt | [CLQ-67: Determine required factors to load in strategy run](https://github.com/liuch288/rbt/pull/21) | ✅ 可合并 | 0 | 1 | 0 | 需确认 get_data 支持 factors 参数 |
| 2026-03-25 | CLQ-66 | rbt | [CLQ-66: Limit read range for existed data in strategy run](https://github.com/liuch288/rbt/pull/20) | ✅ 可合并 | 0 | 1 | 1 | LSP 修复正确，命名更清晰 |
| 2026-03-25 | CLQ-64 | rbt | [CLQ-64: Provide dependency factor information](https://github.com/liuch288/rbt/pull/19) | ✅ 可合并 | 0 | 1 | 0 | 方法重复定义已修复 |
| 2026-03-25 | CLQ-64 | rbt | [CLQ-64: Provide dependency factor information](https://github.com/liuch288/rbt/pull/19) | ❌ 需修复 | 1 | 0 | 0 | 方法重复定义 |
| 2026-03-24 | CLQ-60 | rbt | [CLQ-60: Adjust FuturesMdEngine parameters and Unit auto-naming](https://github.com/liuch288/rbt/pull/17) | ✅ 可合并 | 0 | 1 | 2 | FuturesMdEngine 构造简化，需确认导出 |
| 2026-03-24 | CLQ-63 | rbt | [CLQ-63: Register contract info](https://github.com/liuch288/rbt/pull/18) | ✅ 可合并 | 0 | 0 | 4 | 合约参数统一注入 |
| 2026-03-24 | CLQ-50 | factor_calculator | [CLQ-50: Develop basic version](https://github.com/liuch288/factor_calculator/pull/1) | ✅ 可合并 | 0 | 0 | 5 | 因子计算工具 |
| 2026-03-21 | CLQ-62 | factor_store | [CLQ-62: Remove cast_to_float64 call in save method](https://github.com/liuch288/factor_store/pull/5) | ⚠️ 建议修改 | 0 | 2 | 2 | 有条件通过，需确认历史数据无类型不一致 |
| 2026-03-20 | CLQ-58 | rbt | [CLQ-58: Unit auto naming](https://github.com/liuch288/rbt/pull/15) | ✅ 可合并 | 0 | 0 | 1 | 使用 __init_subclass__ 实现自动单元命名 |
| 2026-03-20 | CLQ-59 | rbt | [CLQ-59: Fix init bug](https://github.com/liuch288/rbt/pull/16) | ✅ 可合并 | 0 | 0 | 0 | 修复 __init__.py 缺失导入 |
| 2026-03-20 | CLQ-55 | factor_view | [CLQ-55: Column filtering feature](https://github.com/liuch288/factor_view/pull/4) | ⚠️ 建议修改 | 1 | 2 | 2 | 需修复 end 变量重复赋值 Bug |
| 2026-03-19 | CLQ-56 | factor_store | [CLQ-56: Standardize date format](https://github.com/liuch288/factor_store/pull/3) | ⚠️ 建议修改 | 0 | 2 | 1 | 需修复 _use_pandas 属性初始化问题 |
| 2026-03-19 | CLQ-57 | factor_store | [CLQ-57: Support skipping existing factors and saving specified factors](https://github.com/liuch288/factor_store/pull/4) | ✅ 可合并 | 0 | 2 | 1 | 列名前缀校验，建议更新 PR 标题 |
| 2026-03-19 | CLQ-54 | rbt | [CLQ-54: Create factor store result db](https://github.com/liuch288/rbt/pull/14) | ⚠️ 建议修改 | 0 | 3 | 3 | 需添加 factor_store 依赖，确认返回类型 |
| 2026-03-18 | CLQ-53 | rbt | [CLQ-53: Extract resultdb base class structure](https://github.com/liuch288/rbt/pull/13) | ✅ 可合并 | 0 | 1 | 4 | 抽象基类设计，建议修复 _get_path 类型注解 |
| 2026-03-17 | CLQ-51 | rbt | [CLQ-51: Add contract information registration](https://github.com/liuch288/rbt/pull/12) | ✅ 可合并 | 0 | 2 | 4 | 合约信息注册机制，建议确认依赖 |
| 2026-03-16 | CLQ-28 | rbt | [CLQ-28: PNL PEU](https://github.com/liuch288/rbt/pull/9) | ✅ 可合并 | 0 | 3 | 3 | 实现 FixedHoldingPEU，建议确认 finish_time |
| 2026-03-16 | CLQ-49 | rbt | [CLQ-49: Add parameter generation function](https://github.com/liuch288/rbt/pull/10) | ✅ 可合并 | 0 | 2 | 2 | 修改收益计算逻辑，添加参数校验 |
| 2026-03-16 | CLQ-49 | rbt | [CLQ-49: Continue parameter generation function](https://github.com/liuch288/rbt/pull/11) | ✅ 可合并 | 0 | 0 | 2 | 新增 get_param_str() 方法 |
| 2026-03-13 | CLQ-46 | rbt | [CLQ-46: Add TimePeriodDMU for time-based trading periods](https://github.com/liuch288/rbt/pull/8) | ✅ 可合并 | 0 | 0 | 4 | 新增时间区间决策单元 |

---

## 审核标准

- ✅ 可合并: 代码质量良好，仅有轻微建议
- ⚠️ 建议修改: 存在一些问题，建议修复后合并
- ❌ 需修复: 存在严重问题，必须修复后才能合并

---

*由 Big Brother 自动生成*
