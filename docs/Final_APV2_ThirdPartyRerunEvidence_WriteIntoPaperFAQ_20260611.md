# APV2 Third-Party Rerun Evidence Write-In Final Summary

Date: 2026-06-11

## 1. Design

Goal: write the ACG-j third-party reproduction into the APV2 paper and FAQ as positive evidence.

Design choice:

- Use ACG-j as third-party AP-style bounded-mechanism reproduction evidence.
- State what it supports: cross-implementation portability of teacher-off/cold-retest, feedback learning, skill reload, generated math generalization, relation-word geometry learning, and no-leakage/control probes.
- Keep AP-Core runtime proof, GL learning evidence, product-shell evidence, and third-party bounded reproduction as distinct evidence layers.
- Avoid presenting ACG-j as full APV2 runtime reproduction or open-world dialogue proof.

Primary evidence facts:

- Repo: `ACG-j/artificial_psyarch`
- Commit: `ccb68aea6291c7e9ed507d5f576803bd99f65f5d`
- `.ap.zip` SHA-256: `051589554123405652740729A02D5BD5A2B00EADDFA425AE2007BAC1EEAE7679`
- `cargo check`: PASS
- `cargo fmt --check`: PASS
- `cargo clippy --all-targets --all-features -- -D warnings`: PASS
- `cargo test --lib`: 84/84 PASS
- Core reports: `generated_math_report`, `relation_word_report`, `paper_key_suite`, `ap_status_report` PASS

## 2. Review

Review decision: approved for write-in.

Main review constraint:

- Phrase this as a strong third-party mechanism reproduction layer.
- Do not over-integrate it into AP-Core runtime proof.
- Do not write a defensive list of everything it does not prove.
- Put public tag/release/archive and optional second clean-machine rerun into next steps.

Design and review records:

- `docs/Design_APV2_ThirdPartyRerunEvidence_WriteIntoPaperFAQ_20260611.md`
- `docs/Review_APV2_ThirdPartyRerunEvidence_WriteIntoPaperFAQ_20260611.md`

## 3. Landing

Updated files:

- `docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md`
- `docs/APV2_MainPaper_Supplement_Index_20260611.md`
- `docs/APV21_VideoFAQ_PublicInitialDraft_v1_0n_20260610.md`
- `docs/APV21_PublicPaper_InitialDraft_v1_0n_20260610.md`

Main paper changes:

- Added ACG-j third-party Rust rerun to the Chinese and English abstracts.
- Added Section 5.4: third-party Rust rerun as cross-implementation AP-style mechanism evidence.
- Added claim map row `ThirdParty-Replication-ACGj-1`.
- Rephrased evidence scope table away from defensive "does not prove" wording.
- Updated future work and reproducibility status to reflect completed local ACG-j rerun and remaining public release binding.

Supplement changes:

- Added ACG-j audit report, Rust rerun report, and summary JSON to the source relationship table.
- Added `ACGj-RustRerun-1`, `ACGj-GeneratedMath-1`, and `ACGj-RelationWord-1` to the evidence map.
- Added third-party clean-room implementation boundary note.

FAQ changes:

- Replaced "third-party candidate" wording with "ACG-j authorized and locally rerun".
- Added compact metrics for 84/84 library tests, generated math, relation-word learning, and control probes.
- Added ACG-j to "AP 当前已经能说明什么".
- Updated next steps to public tag/release/archive binding.

Long technical report changes:

- Updated the opening status note from "third-party reproduction candidate information" to "ACG-j third-party Rust rerun evidence".
- Rewrote Section 9.1 third-party reproduction from candidate status to authorized local rerun evidence.
- Updated submission blockers and future evidence route tables.

## 4. Validation

Validation commands:

```powershell
rg -n "ACG-j|artificial_psyarch|ThirdParty|第三方|84/84|geometry_only|shuffled_expected|051589|ccb68|generated_math|relation-word|relation_word|cold-retest" docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md docs/APV2_MainPaper_Supplement_Index_20260611.md docs/APV21_VideoFAQ_PublicInitialDraft_v1_0n_20260610.md docs/APV21_PublicPaper_InitialDraft_v1_0n_20260610.md
rg -n "暂时还没公开|等 ACG-j|候选在推进|待公开仓库|待独立报告|第三方复现公开|第三方复现候选信息|ThirdParty-Replication-Candidate-1|pending candidate / 待公开仓库|公开第三方复现仍需要|不等同于公开 DOI artifact、独立机器复现或第三方复现|完整开放世界智能已经完成" docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md docs/APV2_MainPaper_Supplement_Index_20260611.md docs/APV21_VideoFAQ_PublicInitialDraft_v1_0n_20260610.md docs/APV21_PublicPaper_InitialDraft_v1_0n_20260610.md
python scripts/check_apv2_mainpaper_runtime_draft.py
```

Validation result:

- ACG-j key terms, commit, artifact hash, 84/84, generated math metrics, relation-word metrics, and control probes are present in target documents.
- Stale ACG-j candidate wording was removed from target paper/FAQ files. The only remaining matched phrase is the new next-step heading "第三方复现公开", which is correct because it now refers to public tag/release/archive binding.
- `python scripts/check_apv2_mainpaper_runtime_draft.py`: PASS.

## 5. Result

This write-in upgrades the evidence chain from "candidate third-party reproduction" to "authorized and locally rerun third-party Rust AP-style bounded-mechanism reproduction".

The positive paper claim is:

ACG-j independently reconstructs several AP-style mechanisms outside the original codebase and locally rerun evidence supports their cross-implementation portability: teacher-off/cold-retest evaluation, feedback memory, skill reload, generated math generalization, relation-word geometry learning, and control probes that separate geometry use from label/path leakage.

## 6. Next Work

Most useful remaining work:

1. Ask or help ACG-j create a stable public tag/release/archive for the exact reviewed commit.
2. Attach original rerun logs and environment notes to the public artifact.
3. Optionally repeat the ACG-j rerun on a second clean machine or VM.
4. Keep GL OpenWorld/Foundation evidence separate as learning-protocol evidence.
5. Keep product-shell/desktop-pet evidence separate as integration and application evidence.
