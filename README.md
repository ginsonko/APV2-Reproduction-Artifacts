# APV2-Reproduction-Artifacts / APV2 实验复现与冻结锚定

        本仓库用于锚定 APV2 发布版实验产物、manifest、SHA-256、复跑日志、Word 发布稿和第三方复现材料。

        This repository anchors APV2 release artifacts: frozen experiment outputs, manifests, SHA-256 records, rerun logs, release documents, and third-party reproduction summaries.

        ## 内容 / Contents

        - `paper_artifacts/release_20260614/`: 发布版论文、新闻稿、仓库说明 Word 文件和 manifest。
        - `outputs/`: AP-Core、GL、第三方复现、public freeze、clean-room rerun 的精选输出。
        - `docs/`: 复现报告、第三方审计报告、baseline 对照和最终汇总。
        - `.ap.zip`: 第三方提供的 `.ap` artifact 压缩包副本。

        ## 使用方式 / Usage

        先阅读 `paper_artifacts/release_20260614/release_manifest_20260614.json` 和 `PUBLIC_STAGING_MANIFEST.json`，再根据各实验报告中的命令复跑目标套件。
