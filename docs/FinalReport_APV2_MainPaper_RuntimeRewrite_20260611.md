# APV2 架构/runtime 主文改写最终报告

日期: 2026-06-11

## 1. 目标

本轮目标是把现有长稿保留为 master technical report, 另行抽取一版更短、更清晰、更适合投稿主文使用的 APV2 架构/runtime 草稿。

本轮遵循用户指定流程:

1. 设计;
2. 审查完善;
3. 通过落地;
4. 严谨验收测试;
5. 最终汇总报告。

## 2. 设计

设计冷保存文件:

- `docs/Design_APV2_MainPaper_RuntimeRewrite_20260611.md`

设计中确定:

- 不直接大删 `docs/APV21_PublicPaper_InitialDraft_v1_0n_20260610.md`;
- 将长稿继续保留为 technical report / appendix 来源;
- 新主文聚焦 APV2 当前 architecture/runtime;
- 概念上统一写 APV2, 不在正文中区分 APV2.1 / APV2.2;
- P0/P1 底层循环材料作为主文核心机制证据;
- GL 学习协议、DPP、Skill37 和产品壳展示保持证据分层, 不写成 AP-Core runtime 证明。

## 3. 审查完善

审查准则文件:

- `docs/ReviewRubric_APV2_MainPaper_RuntimeRewrite_20260611.md`

审查重点:

- 主线是否集中在 APV2 architecture/runtime;
- 新读者是否能不依赖 20 万字 technical report 读懂;
- 快系统和慢系统边界是否清楚;
- 短期叙事槽是否写成每 tick 回读入池的叙事性内感受槽;
- 残差式 B 召回是否写成逐轮吸收, 而非普通 top-k;
- successor lag 是否写成下一 tick 波峰、后续急降和远端尾巴;
- 认知感受是否来自过程量, 而不是外界字段;
- 奖惩派生修正态是否写成行动反馈链路的一部分;
- P0/P1 证据是否有精确数值;
- 是否避免概念性版本分裂和过度防御式正文。

人工修订后, 主文增加了:

- 贡献列表;
- APV2 runtime loop 图;
- state pool vs short-term narrative slot 图;
- residual B recall absorption 图;
- successor lag / rhythm 图;
- 默认参数表;
- 代表性 tick trace 摘要。

## 4. 通过落地

新增文件:

- `docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md`
- `docs/Design_APV2_MainPaper_RuntimeRewrite_20260611.md`
- `docs/ReviewRubric_APV2_MainPaper_RuntimeRewrite_20260611.md`
- `scripts/check_apv2_mainpaper_runtime_draft.py`
- `docs/FinalReport_APV2_MainPaper_RuntimeRewrite_20260611.md`

主文当前规模:

- lines: 267
- characters: 14,305 by `Measure-Object`
- script counted chars: 14,683 including read text representation

主文核心结构:

1. 摘要;
2. 引言;
3. APV2 的最小对象;
4. Runtime 架构;
5. 核心机制;
6. P0/P1 机制证据;
7. 与 LLM Agent 和传统认知架构的关系;
8. 证据边界与后续路线;
9. 结论。

## 5. 严谨验收测试

### 5.1 文档结构与污染检查

命令:

```powershell
python scripts\check_apv2_mainpaper_runtime_draft.py
```

结果:

```text
APV2 mainpaper draft check: PASS
checked: H:\AP原型实验第二期\APV2.1版本原型测试\docs\APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md
chars: 14683
```

检查内容包括:

- 必须出现六个 P0/P1 证据名;
- 必须出现关键数值;
- 必须出现主要章节标题;
- 不允许概念性 APV2.1 / APV2.2 版本拆分;
- 对替代学习的危险词只允许在边界说明中出现;
- 检查过度防御式段落。

### 5.2 P0/P1 证据测试

命令:

```powershell
python -m pytest tests\test_apv2_bottom_loop_p0_materials.py tests\test_apv2_p1_hardening_materials.py -q
```

结果:

```text
8 passed, 1 warning in 7.18s
```

warning:

- `legacy_apv2\sensors\hearing_sensor_v1.py` 中 Python `audioop` deprecation warning;
- 与本轮 AP-Core paper material、P0/P1 底层循环证据无关。

### 5.3 证据引用核对

主文已正确纳入:

| 证据 | 主文引用 |
|---|---|
| `APV2-BottomLoop-ParamSensitivity-1` | `16/16 pass` |
| `ShortTermSlot-OrderAblation-1` | full-order margin `18.2466`; without-order margin `9.0539` |
| `LongRun-InterruptionRecovery-1` | interruptions `2`; resumptions `2`; final slot virtual mass `1.3715` |
| `RhythmSuccessor-Replay-1` | lag 1 `1.0`; lag 2 `0.42`; lag 4 `0.172`; rhythm slot row |
| `PersistenceBackend-Reload-1` | SHA-256 `19a0d88ba4ce8eacb01fe488ae72207a427c50f85bd8cc7bf4a30f74a50e60d7`; warm-load loaded `3` |
| `ArtifactFreeze-1` | local pre-public manifest `12 entries` |

## 6. 当前主文支持的判断

本轮主文可以积极支持以下判断:

1. APV2 当前 runtime 已经形成可读的白箱预测-行动闭环。
2. 状态池和短期叙事槽的边界已经可以清楚表达: 前者是无序能量场, 后者是有序、可衰减、可回读的叙事性内感受槽。
3. 残差式 B 召回已经有可审计的逐轮吸收 trace, 支持复杂 query 被多个历史对象共同解释。
4. successor lag 和 rhythm/phase 已经能表达下一 tick 波峰、急降尾巴和节奏相位。
5. 奖惩派生修正态、行动反馈和持久化重载已经能纳入 AP-Core runtime 证据链。
6. P0/P1 证据足以支撑 Paper 1 的 architecture/runtime 主线。

## 7. 当前仍不应过度主张的部分

主文保持以下边界:

- 不把 GL 学习协议结果写成 AP-Core runtime 证明;
- 不把 DPP/Skill37 写成底层循环证明;
- 不把桌面/桌宠 product shell 写成 AP-Core 证明;
- 不把 JSONL persistence 写成 PostgreSQL 或生产级部署证明;
- 不把 P0/P1 机制证据写成完整开放世界语言学习已经完成;
- 不把 APV2 写成完整 AGI 或完整人类心智模型。

## 8. 后续计划

推荐下一步:

1. 将 P1 Mermaid 图转成投稿级静态图;
2. 为主文补正式英文标题、英文摘要和统一引用格式;
3. 把 long technical report 整理为 supplement / appendix;
4. 继续补 AP 侧机制实验: residual depth stress、long-run stability、larger parameter basin、interruption recovery stress;
5. 等 GL 侧 learning protocol / DPP / Skill37 teacher-off/cold retest 稳定后, 另写学习协议或 evidence/audit companion paper;
6. 做 public artifact freeze, 绑定 commit/tag/hash、运行环境和复现脚本。

## 9. 最终结论

本轮 APV2 架构/runtime 主文改写已经完成第一版可验收草稿。它没有继续把长稿机械加长, 而是把 APV2 当前底层循环的核心机制压缩成一条主文级论证链: 状态池、短期叙事槽、残差召回、后继波峰、过程感受、行动反馈、持久化与 P0/P1 证据。

验收结果显示:

- 文档检查 PASS;
- P0/P1 targeted tests PASS;
- 主文未出现概念性 APV2 版本拆分;
- 必备证据与关键数值已纳入;
- GL/Product Shell 边界已保持。

因此, 下一阶段可以进入图表正式化、technical report / supplement 整理和目标 venue 风格压缩。
