# APV2 主文英文信息、引用格式与审稿改进最终报告

日期: 2026-06-11

## 1. 目标

本轮继续按指定流程推进:

1. 设计;
2. 审查完善;
3. 通过落地;
4. 严谨验收测试;
5. 最终汇总报告。

目标是在 APV2 architecture/runtime 主文中补齐英文题名/摘要/关键词、图注、引用和 References, 并从审稿人角度做一轮严格评审、评分与反向修订。

## 2. 设计

设计文件:

- `docs/Design_APV2_MainPaper_EnglishCitationReview_20260611.md`

设计确定:

- 本轮不绑定具体 venue;
- 输出定位为 venue-neutral hardening draft;
- 保持 AP-Core runtime、GL learning 和 product shell 的证据边界;
- 审稿评分采用 10 分制, 给出接收倾向;
- 审稿意见中可立即修复的部分必须回写主文。

## 3. 审查完善

审查文件:

- `docs/Review_APV2_MainPaper_EnglishCitationReview_20260611.md`

审查要求:

- 英文 title / abstract / keywords 必须存在;
- 5 张图必须有 `Figure N.` 图注;
- References 必须与正文 citation keys 对齐;
- related work 必须覆盖 LLM/agents、Soar/ACT-R、predictive processing 等相邻路线;
- 不把 GL/DPP/Skill37/product shell 写成 AP-Core runtime proof;
- 不把 APV2 写成完整 AGI 或完整人类心智。

## 4. 通过落地

修改主文:

- `docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md`

新增审稿报告:

- `docs/ReviewerReport_APV2_MainPaper_ArchitectureRuntime_20260611.md`

新增最终报告:

- `docs/FinalReport_APV2_MainPaper_EnglishCitationReview_20260611.md`

修改检查脚本:

- `scripts/check_apv2_mainpaper_runtime_draft.py`

主文新增内容:

1. English title: `APV2: A White-Box Predictive-Action Runtime for Continuous Cognition`;
2. English Abstract;
3. English Keywords;
4. F1-F5 的正式 figure captions;
5. 最小形式化定义:

```text
APV2_runtime = <SA, R, M, S, B, C, E, A, F, P>
```

6. `Claim-To-Evidence` 表;
7. 机制探针价值说明;
8. related-work 压缩对照表;
9. public-freeze checklist;
10. `## References`。

## 5. 审稿人式评审与评分

审稿报告文件:

- `docs/ReviewerReport_APV2_MainPaper_ArchitectureRuntime_20260611.md`

评分:

| Criterion | Score |
|---|---:|
| Novelty and positioning | 1.6 / 2.0 |
| Technical clarity | 1.5 / 2.0 |
| Evidence and reproducibility | 1.35 / 2.0 |
| Related work and fairness | 1.1 / 1.5 |
| Writing/readability | 0.8 / 1.0 |
| Boundary honesty | 1.4 / 1.5 |

Total: **7.75 / 10**

Recommendation: **Weak Accept / Borderline-Positive after revision**

审稿判断:

- 论文作为 architecture/runtime 系统稿有清楚的新意和可读主线;
- P0/P1 证据支持 AP-Core runtime 机制, 但仍主要是本地机制探针;
- 投稿前最大缺口是 public artifact freeze、外部复现和更强 related-work 展开;
- 现阶段不应主张完整开放世界对话、完整 AGI 或产品壳能力。

## 6. 根据审稿意见回写的改进

审稿意见中可立即修复的项目已经回写:

| reviewer concern | revision |
|---|---|
| 需要紧凑 runtime formalism | 新增 `APV2_runtime = <SA, R, M, S, B, C, E, A, F, P>` 表 |
| P0/P1 claim 映射不够直接 | 新增 `Claim-To-Evidence` 表 |
| 机制探针可能被认为只是 toy | 新增机制探针价值说明 |
| artifact 状态需要更清楚 | 新增 public-freeze checklist |
| related work 边界压缩 | 新增相邻路线对照表 |

## 7. 严谨验收测试

### 7.1 主文检查

命令:

```powershell
python scripts\check_apv2_mainpaper_runtime_draft.py
```

结果:

```text
APV2 mainpaper draft check: PASS
checked: H:\AP原型实验第二期\APV2.1版本原型测试\docs\APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md
chars: 23996
```

检查脚本现在覆盖:

- 必备证据名;
- 必备章节;
- English title / Abstract / Keywords;
- 5 个 Figure captions;
- References 与正文 citation key 对齐;
- 静态图路径存在;
- 禁止性替代表述是否被边界框住;
- 概念性 APV2.1 / APV2.2 版本拆分。

### 7.2 图表/supplement 与 P0/P1 测试

命令:

```powershell
python -m pytest tests\test_apv2_publication_figures_supplement.py tests\test_apv2_bottom_loop_p0_materials.py tests\test_apv2_p1_hardening_materials.py -q
```

结果:

```text
10 passed, 1 warning in 9.76s
```

warning:

- `legacy_apv2\sensors\hearing_sensor_v1.py` 的 Python `audioop` deprecation warning;
- 与本轮论文主文、图表、引用或 P0/P1 evidence material 无关。

## 8. 当前稿件状态

当前主文已经从内部架构草稿推进到更接近投稿稿的状态:

- 有中英文摘要;
- 有关键词;
- 有 5 张静态图和正式图注;
- 有最小形式化对象表;
- 有 P0/P1 claim-to-evidence 表;
- 有 related-work citation keys 和 References;
- 有 public-freeze checklist;
- 有审稿人式评分和反向修订记录。

当前最合理定位:

> APV2 architecture/runtime paper, venue-neutral hardening draft, reviewer-score estimate 7.75/10, weak-accept/borderline-positive after revision.

## 9. 投稿前剩余关键工作

按优先级:

1. Public artifact freeze: repo/archive, commit/tag/hash, dependency lock, reproduction command;
2. Venue-specific compression: 按目标期刊/会议压缩字数、图数、图注和引用格式;
3. External replication candidate: clean-machine rerun 或第三方复现候选;
4. Related work expansion: 若目标 venue 偏认知架构, 需要更深 Soar/ACT-R/FEP/agent 比较;
5. Experiment hardening: residual depth stress、long-run stability、larger parameter basin;
6. GL learning results: 等 GL 侧 teacher-off/cold retest/no-leakage audit 完成后, 作为 companion/evidence paper 处理。

## 10. 最终结论

本轮完成了英文信息、引用格式、图注、审稿评估和反向修订。当前稿件比上一轮更像一篇能被审稿人阅读的 architecture/runtime 系统论文: 主张更集中, 证据映射更直接, 相关工作更公平, artifact 状态更清楚。

评分为 **7.75 / 10**。我的审稿人式建议是: **Weak Accept / Borderline-Positive after revision**。若完成 public artifact freeze、venue-specific 压缩和至少一个 clean-machine rerun, 这篇主文有机会提升到更稳定的 weak accept / accept 区间。
