# APV2 投稿图表与 Supplement 整理最终报告

日期: 2026-06-11

## 1. 目标

本轮继续推进 APV2 架构/runtime 主文投稿材料, 目标是:

1. 将 Mermaid 草图转成可复现生成的静态 SVG/PNG 图表;
2. 建立主文与 long technical report、P0/P1 evidence artifacts 之间的 supplement 索引;
3. 将静态图接入主文草稿;
4. 通过脚本和测试验收图表、索引、主文引用和 P0/P1 证据稳定性。

本轮仍然只服务 AP-Core architecture/runtime 主文。GL 学习协议、DPP、Skill37 和 product shell 继续保持独立证据线。

## 2. 设计

设计冷保存:

- `docs/Design_APV2_PublicationFiguresSupplement_20260611.md`

设计中确定输出:

- 5 张投稿用静态图;
- 图表 manifest;
- supplement index;
- 图表生成脚本;
- 自动验收测试;
- 主文静态图引用。

## 3. 审查完善

审查准则:

- `docs/Review_APV2_PublicationFiguresSupplement_20260611.md`

审查重点:

- 图表是否服务主文而不是增加噪声;
- F1-F5 是否分别覆盖 runtime loop、state pool vs slot、residual recall、successor/rhythm、evidence layer split;
- supplement 是否是索引, 而不是机械复制 long technical report;
- 是否避免把 GL/DPP/Skill37/product shell 混写为 AP-Core runtime proof;
- 是否避免概念性 APV2 版本拆分。

本轮中途发现并修正了两个问题:

1. supplement/manifest 初版使用绝对路径, 会把历史目录名带入投稿材料。已改为相对路径。
2. F1/F4 初版箭头略显拥挤。已调整 F1 的 slot 回灌箭头, 并将 F4 的 rhythm phase 影响改为弱连接说明。

## 4. 通过落地

新增/修改文件:

- `scripts/build_apv2_publication_figures_supplement.py`
- `tests/test_apv2_publication_figures_supplement.py`
- `docs/APV2_MainPaper_Supplement_Index_20260611.md`
- `docs/Design_APV2_PublicationFiguresSupplement_20260611.md`
- `docs/Review_APV2_PublicationFiguresSupplement_20260611.md`
- `docs/FinalReport_APV2_PublicationFiguresSupplement_20260611.md`
- `docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md`
- `scripts/check_apv2_mainpaper_runtime_draft.py`

最终图表包:

- `outputs/apv2_publication_figures_supplement_20260611_002510/`

图表 manifest:

- `outputs/apv2_publication_figures_supplement_20260611_002510/figure_manifest.json`

图表清单:

| id | title | svg | png |
|---|---|---|---|
| F1 | APV2 runtime loop | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f1_apv2_runtime_loop.svg` | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f1_apv2_runtime_loop.png` |
| F2 | State pool vs short-term narrative slot | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f2_state_pool_vs_short-term_narrative_slot.svg` | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f2_state_pool_vs_short-term_narrative_slot.png` |
| F3 | Residual B recall absorption | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f3_residual_b_recall_absorption.svg` | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f3_residual_b_recall_absorption.png` |
| F4 | Successor lag and rhythm replay | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f4_successor_lag_and_rhythm_replay.svg` | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f4_successor_lag_and_rhythm_replay.png` |
| F5 | Evidence layer split | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f5_evidence_layer_split.svg` | `outputs/apv2_publication_figures_supplement_20260611_002510/figures/f5_evidence_layer_split.png` |

## 5. 严谨验收测试

### 5.1 图表与 supplement 测试

命令:

```powershell
python -m pytest tests\test_apv2_publication_figures_supplement.py -q
```

结果:

```text
2 passed in 9.84s
```

检查内容:

- 生成 5 张 SVG;
- 生成 5 张 PNG;
- manifest 存在且 figure_count = 5;
- 每张图有非空 sha256 和非零文件大小;
- supplement index 覆盖 P0/P1 六个关键证据;
- supplement 明确 DPP/Skill37/product shell 是 adjacent evidence lines, not AP-Core proof;
- supplement 和 SVG 不出现概念性 APV2.1 / APV2.2 版本拆分。

### 5.2 主文检查

命令:

```powershell
python scripts\check_apv2_mainpaper_runtime_draft.py
```

结果:

```text
APV2 mainpaper draft check: PASS
checked: H:\AP原型实验第二期\APV2.1版本原型测试\docs\APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md
chars: 14788
```

本轮已增强该检查脚本: 现在会同时检查主文中引用的 SVG/PNG 静态图是否实际存在。

### 5.3 P0/P1 targeted tests

命令:

```powershell
python -m pytest tests\test_apv2_bottom_loop_p0_materials.py tests\test_apv2_p1_hardening_materials.py -q
```

结果:

```text
8 passed, 1 warning in 3.92s
```

warning:

- `legacy_apv2\sensors\hearing_sensor_v1.py` 的 Python `audioop` deprecation warning;
- 与本轮 AP-Core 主文图表、supplement 或 P0/P1 evidence material 无关。

### 5.4 联合验收

命令:

```powershell
python -m pytest tests\test_apv2_publication_figures_supplement.py tests\test_apv2_bottom_loop_p0_materials.py tests\test_apv2_p1_hardening_materials.py -q
```

结果:

```text
10 passed, 1 warning in 11.67s
```

## 6. 当前支持的判断

本轮材料支持以下投稿准备判断:

1. APV2 architecture/runtime 主文已经有 5 张可复现生成的静态图。
2. 图表不再依赖 Mermaid 渲染环境, 可直接以 SVG/PNG 进入论文或 appendix。
3. 主文已经接入静态图路径, 且检查脚本验证图文件存在。
4. supplement index 已经把主文、long technical report、P0/P1 artifact 和边界说明连接起来。
5. AP-Core runtime、AP-Core task、GL learning 和 product shell 的证据分层在 F5 和 supplement 中都有显式表达。

## 7. 边界

本轮不声称:

- GL 学习协议已经完成投稿级证明;
- DPP/Skill37 是 AP-Core runtime 证明;
- product shell 或桌宠展示是 AP-Core proof;
- JSONL persistence 等于生产级数据库部署;
- 当前图表已经满足某个具体 venue 的版式规范。

本轮明确避免:

- 关键词硬门;
- regex route;
- answer table;
- student-side LLM;
- hidden solver;
- full-sentence macro;
- 外界字段直接冒充 AP-native cognitive feeling。

## 8. 后续建议

下一步推荐:

1. 为主文补英文标题、英文摘要和统一 citation style;
2. 按目标 venue 的模板重新排版图尺寸、字体和图注;
3. 将 long technical report 冷冻成 supplement / appendix 初稿, 添加稳定章节锚点;
4. 准备 public artifact freeze: commit/tag/hash、环境说明、运行脚本、输出 manifest;
5. 等 GL 侧学习证据稳定后, 再开 learning protocol / evidence-audit companion paper。

## 9. 最终结论

本轮“投稿级静态图 + supplement index”已完成并通过验收。APV2 主文现在不再只有文字和 Mermaid 草图, 而是有可复现生成的 SVG/PNG 图表包、图表 manifest、supplement 索引和自动检查脚本。当前材料已经可以支撑下一阶段的正式排版、英文摘要、引用统一和 venue-specific 压缩。
