# APV2 Release Notes 2026-06-14

本仓库是 APV2 发布包的一部分，角色是：冻结 artifact、manifest、SHA-256、复跑日志、Word/PDF 发布稿和第三方复现整理。

This repository is one part of the APV2 public release package. Its role is: 冻结 artifact、manifest、SHA-256、复跑日志、Word/PDF 发布稿和第三方复现整理.

## Release Tag

`apv2-release-20260614-final-longreport`

## Evidence Included

- 发布版 Word/PDF、release manifest、journal-style figures 和 trace excerpt。
- ACG-j Rust AP-inspired implementation 本地复跑整理: 84/84 library tests, generated math, relation-word geometry, reload, holdout 和 no-leakage/control probes。
- AP-Core、GL、baseline、STP-v2、online vector 和第三方复现的精选 public artifacts。

## Reproduction Anchors

- Repository manifest: `PUBLIC_STAGING_MANIFEST.json`
- Cross-repository zip summary: `release_repos_20260614/PUBLIC_REPO_STAGING_SUMMARY.json`
- Paper artifact manifest: `paper_artifacts/release_20260614/release_manifest_20260614.json`
- Main AP-Core repository: `https://github.com/ginsonko/Artificial-PsyArch-V2`
- GL repository: `https://github.com/ginsonko/APV2-GL-OpenWorld-Chinese`
- Artifact repository: `https://github.com/ginsonko/APV2-Reproduction-Artifacts`
- Third-party reference implementation: `https://github.com/ACG-j/artificial_psyarch`

## Suggested Quick Checks

- `python - <<'PY'
import json, hashlib
from pathlib import Path
m=json.loads(Path('PUBLIC_STAGING_MANIFEST.json').read_text(encoding='utf-8'))
print(m['repo_id'], m['file_count'], m['total_bytes'])
PY`

## Evidence Layering

AP-Core、GL、第三方复现和 Product/Canvas/Desktop 证据线在发布材料中分层呈现。AP-Core 负责底层机制验证；GL 负责学习协议和开放中文对话验证；artifact 仓库负责冻结证据与复现锚点；Product/Canvas/Desktop 证据线展示受控应用接口和外部效度。
