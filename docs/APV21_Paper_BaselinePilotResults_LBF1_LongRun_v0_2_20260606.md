# APV2.1 论文实验章节草案：RepeatMap v0.5、LBF1 与 LongRun pilot results

版本：v0.2

时间：2026-06-06

定位：投稿论文的补充实验/候选结果章节草案。本文整理当前 baseline / controlled pilot candidate 证据，不把它写成最终 benchmark，也不主张 AP 已经全面胜过 LLM/RAG/agent。

## 1. 实验目的

本节汇报三组用于增强外部可检验性的对比实验。

RepeatMap-RealAPI v0.5 fixed 是当前最强的真实 API 多 seed 候选结果，也是 controlled multiseed candidate。它测试未知映射规则下的持续反馈学习：受试者只能看到公开状态和动作 A/B/C/D，训练阶段提交动作后才收到 reward/punishment，holdout、teacher-off 和 package reload 阶段不给反馈，也不写入记忆。该实验重点比较 AP-style/strict_core、固定启发式、真实 no-memory LLM、真实 LLM+public memory/tool 在学习、保持、规则切换再适应、token 成本和可审计性上的差异。

LBF1 四路线同题对比用于观察：在同一批 6 个受控 smoke case 下，AP-Core、公开规则、单轮 LLM、LLM+记忆/工具 agent 在结果、token 成本、依赖结构和可审计性上的差异。

LongRun-UnknownRule-Learning-1 v0.2 用于观察：在 learner 初始不知道隐藏规律的条件下，不同路线能否通过 reward/punishment 形成持续学习、经验包重载保持，以及规则切换后的再适应趋势。

三组实验均采用 teacher-off/no-leakage 约束：runner 输出前不得接触 sealed answer、private examiner、隐藏目标动作或后验评分字段。评分只在 runner 提交后进行。

## 2. RepeatMap v0.5 fixed: 真实 API 多 seed 候选结果

### 2.1 实验设置

RepeatMap v0.5 使用：

1. `seed_count=5`
2. `state_count=12`
3. `train_repeats=4`
4. 单 seed 单阶段准确率粒度 `1/12=0.0833`
5. 跨 seed 汇总为 mean±95% CI

每条真实 API 路线每 seed trial 数：

`pretest 12 + alpha_train 48 + alpha_holdout 12 + reload 12 + beta_train 48 + beta_holdout 12 = 144`

G3/G4 两条真实路线合计上限为 `1440` 次请求。最终 fixed 记录中真实 LLM 调用数为 `1424`，总 token 为 `3930152`。

### 2.2 受试者身份

| 路线 | 身份 | API/token | 记忆与工具 |
| --- | --- | ---: | --- |
| G1A AP-style | `APFeedbackLearner` | 0 calls / 0 tokens | internal action-feedback memory |
| G1B strict_core bridge | `StrictRuntimeBridge + feedback recall policy` | 0 calls / 0 tokens | `DualEnergyStatePool + MemoryStore` |
| G2 固定启发式 | `FixedHeuristic` | 0 calls / 0 tokens | none |
| G3 Claude no-memory | `claude-opus-4-6` via `https://senerapi.com` | 717 calls / 2928528 tokens | none |
| G4 GPT+memory/tool | `gpt-5.5-all` via `https://senerapi.com` | 707 calls / 1001624 tokens | public memory + `tool.repeatmap_public_feedback_vote.v1` |

这组对比不是用弱模型做靶子。G3 使用真实 `claude-opus-4-6`；G4 使用真实 `gpt-5.5-all`，并且给了 public memory/tool 强条件。G4 的结果显著高于 G3，说明该 baseline 并非被故意削弱。

### 2.3 结果摘要

| 路线 | alpha holdout | beta holdout | API calls | tokens | tools | errors |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| G1A AP-style | 1.0000±0.0000 | 1.0000±0.0000 | 0 | 0 | 0 | 0 |
| G1B strict_core bridge | 1.0000±0.0000 | 1.0000±0.0000 | 0 | 0 | 0 | 0 |
| G2 fixed heuristic | 0.2000±0.2400 | 0.2500±0.2191 | 0 | 0 | 0 | 0 |
| G3 Claude no-memory | 0.2167±0.0400 | 0.3000±0.0980 | 717 | 2928528 | 0 | 6 |
| G4 GPT+memory/tool | 0.8333±0.2066 | 0.8500±0.1819 | 707 | 1001624 | 660 | 120 |

观察结果：

1. G1A/G1B 在该受控未知映射任务中达到 alpha/beta holdout 1.0000±0.0000，且不调用 LLM、不消耗 token、不使用外部工具。
2. G2 固定启发式接近公开规则/随机基线，没有学习增益。
3. G3 真实 `claude-opus-4-6` 在 no-memory/no-tool 独立调用条件下没有跨轮学习载体，结果接近 G2。
4. G4 真实 `gpt-5.5-all` + public memory/tool 表现明显更强，说明强 LLM-agent 路线有效；但它需要真实 API、token 成本、外部记忆和工具调用。
5. G4 的高分不削弱 AP 价值，反而说明对照不是稻草人。该实验展示的是内生反馈记忆与外部 LLM-agent harness 的机制、成本和审计差异。

### 2.4 Provenance 与异常

首次 full run 中，G4 因执行时使用错误/截断 key 出现 `401 Invalid token`。该失败已保留为 badkey artifact，不作为模型能力证据。最终 fixed 结果采用 corrected G4 full rerun，并用 merge policy 合并：

`G1A/G1B/G2/G3 are copied from base full run; G4 is copied from the corrected G4 fixed run. No successful route is re-scored or hand-edited.`

最终 records sha256：

`0bfc62535a43b8fb4b7c254e5587c529036cc14291c93474335789b9ef40ec7a`

该部分的论文表述必须保留这一 provenance，避免给人挑结果或隐藏失败的印象。

### 2.5 可支持与不可支持的结论

可以支持：

1. 在 RepeatMap v0.5 受控未知映射任务中，AP-style/strict_core bridge 展示了低成本反馈学习、保持与规则切换再学习能力。
2. no-memory/no-tool LLM 条件缺少跨轮学习载体，难以在该任务中自然提高。
3. LLM+memory/tool agent 是强路线，但机制、成本和审计结构不同于 AP-style 内部反馈记忆。

不可支持：

1. AP 已经全面胜过 LLM/RAG/agent。
2. G1B 是 full APV2.1 runtime。
3. RepeatMap v0.5 是最终 benchmark。
4. G4 badkey run 是模型能力失败。
5. 该任务能代表所有开放自然语言、开放视觉或真实桌面任务。

换言之，G1B 是 strict_core bridge，不是 full APV2.1 runtime；RepeatMap v0.5 fixed 是 controlled multiseed candidate，不是最终 benchmark。

## 3. LBF1 四路线同题对比

### 3.1 受试者身份

| 路线 | 身份 | API/token | 记忆与工具 |
| --- | --- | ---: | --- |
| G1 AP-Core 原生闭环 | `g1_apcore_same_case_runner_v0_1` | 0 calls / 0 tokens | AP-Core action-outcome memory、feature-contribution memory、registered AP-Core math process skills；无外部 LLM/API |
| G2 公开规则基线 | `g2_rule_runner_v0_1_public_rules` | 0 calls / 0 tokens | exact lookup、nearest lookup、public feature rules；非 AP 主体 |
| G3 单轮 LLM 基线 | `claude-opus-4-6` via `https://senerapi.com` | 6 calls / 3912 tokens | 无持久记忆、无工具 |
| G4 LLM+记忆/工具 agent | `gpt-5.5-all` via `https://senerapi.com` | 6 calls / 6375 tokens | `external_logged_memory` + `tool.action_recommendation_from_logged_memory.v1`；`api_key_saved=false` |

这组对比不是用弱模型做靶子。G3 使用真实 `claude-opus-4-6`，G4 使用真实 `gpt-5.5-all` 加公开日志记忆和行动推荐工具。G4 达到 6/6 后验匹配，说明本对照不是刻意削弱的 baseline。

### 3.2 结果摘要

| 路线 | 后验匹配 | 候选分 | API/tokens | 工具 |
| --- | ---: | ---: | ---: | ---: |
| G1 AP-Core 原生闭环 | 6/6 | 90/96 | 0/0 | 0 |
| G2 公开规则基线 | 5/6 | 70/96 | 0/0 | 0 |
| G3 单轮 LLM 基线 | 5/6 | 41/96 | 6/3912 | 0 |
| G4 LLM+记忆/工具 agent | 6/6 | 70/96 | 6/6375 | 8 |

评分为 pilot candidate score，每题最高 16 分，由 task success、feedback learning、persistence、process transparency、dependency clarity、leakage resistance、data efficiency、adaptation 八个维度组成。

本结果可以支持的谨慎表述是：在这批受控同题 smoke case 中，AP-Core 路线以 0 token、0 外部 API 获得较高候选分；G4 真实强模型 agent 也达到 6/6，但依赖真实 LLM API、公开日志记忆和行动推荐工具。该结果展示的是机制、成本和审计结构差异，而非 AP 对所有 LLM/agent 的普遍胜出。

## 4. LongRun v0.2 no-API 多 seed pilot

### 4.1 受试者身份

| 路线 | 身份 | API/token | 记忆与工具 |
| --- | --- | ---: | --- |
| G1-LR AP-style 持续学习 | `APStyleLearner` | 0 calls / 0 tokens | internal feature/action-feedback weights + internal memory rows |
| G2-LR 固定公开启发式 | `StaticRuleBaseline` | 0 calls / 0 tokens | fixed public hash-like heuristic；无学习 |
| G3-LR 无记忆单轮启发式 | `StatelessNoMemoryBaseline` | 0 calls / 0 tokens | current visible state only；无持久记忆 |
| G4-LR 外部记忆/工具 agent | `ExternalMemoryToolBaseline` | 0 calls / 0 tokens | external logged action-feedback memory + `tool.longrun_external_memory_vote.v1` |

LongRun v0.2 是 no-API 多 seed pilot。G4-LR 是外部 memory/tool harness 强基线，不是真实 LLM+RAG API 的最终表现；它用于给 AP-style 内生学习路线提供较强、透明且可审计的外部工具对照。

### 4.2 结果摘要

默认 9 seeds，每个 seed 四条路线，共 36 seed-run。CI 为描述性 95% 半宽，不是正式显著性检验。

| 路线 | 稳定首窗 | 稳定末窗 | 学习增益 | 重载保持 | 切换首窗 | 切换末窗 | 再适应增益 | 平均 tools |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| G1-LR AP-style 持续学习 | 0.3978 | 0.6310 | +0.2332 | 0.6379 | 0.2346 | 0.4760 | +0.2414 | 0 |
| G2-LR 固定公开启发式 | 0.2222 | 0.2222 | +0.0000 | 0.2222 | 0.2222 | 0.2222 | +0.0000 | 0 |
| G3-LR 无记忆单轮启发式 | 0.1975 | 0.1975 | +0.0000 | 0.1975 | 0.2716 | 0.2716 | +0.0000 | 0 |
| G4-LR 外部记忆/工具 agent | 0.3663 | 0.6337 | +0.2675 | 0.6543 | 0.3416 | 0.6241 | +0.2826 | 1215 |

观察结果：

1. G1-LR 在 0 token、0 外部工具下出现稳定阶段学习增益、经验包重载保持和规则切换后的再适应趋势。
2. G2-LR 与 G3-LR 不具备持久学习机制，均未出现跨轮学习增益。
3. G4-LR 在本轮均值中表现最强，说明外部 memory/tool harness 是强路线；这并不削弱 AP-style 结果，反而使对比更公平。
4. G1-LR 与 G4-LR 的差异应解释为“内生闭环 vs 外部 agent harness”的机制差异，而不是简单胜负。

## 5. 与 AP 论文主张的关系

这三组实验适合放在论文的 controlled pilot evidence 或 supplementary experiments 中，用于支撑以下有限主张：

1. AP-style/strict_core 路线可以在小规模、受控、可审计任务中展示低 token 成本的实时反馈学习现象。
2. AP-Core/AP-style 路线和 LLM/agent harness 路线不是同一种机制：前者强调内部状态、行动、反馈和记忆的闭环固化；后者强调外部模型、外部记忆和工具调度。
3. 强 G4/G4-LR baseline 的存在使证据更可信，因为它避免了只与弱 baseline 比较。
4. RepeatMap v0.5 fixed 比 v0.4 更适合作为当前主候选结果，因为它使用更多 state、更多 seed、真实强模型身份、原始 request/response 与 provenance。

当前不应写入的结论：

1. AP 已经全面胜过 LLM/RAG/agent。
2. LLM 无法持续学习。
3. LBF1、LongRun v0.2 或 RepeatMap v0.5 已是最终论文 benchmark。
4. LongRun G4-LR 等同真实 LLM+RAG API 最终表现。
5. G1-LR 或 G1B 等同完整 APV2.1 runtime。

## 6. 证据路径

RepeatMap v0.5 fixed 展示：

`outputs/repeatmap_realapi_v05_full_real_fixed_20260606/repeatmap_v05_explained_showcase_zh.html`

`outputs/repeatmap_realapi_v05_full_real_fixed_20260606/repeatmap_realapi_v05_records.json`

`outputs/repeatmap_realapi_v05_full_real_fixed_20260606/repeatmap_v05_explained_artifact_manifest.json`

LBF1 展示：

`outputs/llm_baseline_fair1_g4_memory_tool_runner_20260606/lbf1_four_route_bar_showcase_zh.html`

`outputs/llm_baseline_fair1_g4_memory_tool_runner_20260606/lbf1_four_route_bar_showcase_summary.json`

LongRun v0.2 展示：

`outputs/longrun_unknown_rule_learning1_v02_20260606/longrun_unknown_rule_learning1_v02_showcase_zh.html`

`outputs/longrun_unknown_rule_learning1_v02_20260606/longrun_unknown_rule_learning1_v02_records.json`
