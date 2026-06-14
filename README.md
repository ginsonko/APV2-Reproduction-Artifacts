# APV2-Reproduction-Artifacts / APV2 实验复现与冻结锚定

本仓库用于锚定 APV2 发布版实验产物、manifest、SHA-256、复跑日志、Word 发布稿和第三方复现材料。读者可以从这里追踪论文结论对应的公开文件、实验输出和复现实验线索。

This repository anchors APV2 release artifacts: frozen experiment outputs, manifests, SHA-256 records, rerun logs, release documents, and third-party reproduction summaries.

## 发布锚点 / Release Anchors

- Official release tag: `apv2-release-20260614-final-cn-pdf`
- Repository manifest: `PUBLIC_STAGING_MANIFEST.json`
- Word release manifest: `paper_artifacts/release_20260614/release_manifest_20260614.json`
- Third-party reference: `https://github.com/ACG-j/artificial_psyarch`

## 内容 / Contents

- `paper_artifacts/release_20260614/`: 发布版论文、新闻稿、仓库说明 Word 文件和 manifest。
- `outputs/`: AP-Core、GL、第三方复现、public freeze、clean-room rerun 的精选输出。
- `docs/`: 复现报告、第三方审计报告、baseline 对照和最终汇总。
- `.ap.zip`: 第三方提供的 `.ap` artifact 压缩包副本。

## 使用方式 / Usage

先阅读 `paper_artifacts/release_20260614/release_manifest_20260614.json` 和 `PUBLIC_STAGING_MANIFEST.json`，再根据各实验报告中的命令复跑目标套件。

## License / 许可证

本仓库按 `APV2 Public Research License v2026-06-14` 发布为 source-available public research preview。允许公开阅读、克隆、本地复验、非商业研究评估和合理引用；商业使用、模型训练或评测数据复用、数据集/技能包再打包、产品部署或声称官方衍生版本需要另行授权。完整条款见 `LICENSE`。

This repository is source-available for public research preview under `APV2 Public Research License v2026-06-14`. Public reading, cloning, local reproduction, non-commercial research evaluation, and citation are permitted; commercial use, model-training/evaluation-data reuse, dataset or skill-package repackaging, product deployment, and official-release claims require separate permission. See `LICENSE`.
