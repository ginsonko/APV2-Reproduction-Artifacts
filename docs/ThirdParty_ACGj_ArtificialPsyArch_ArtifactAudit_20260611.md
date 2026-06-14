# Third-Party Artifact Audit: ACG-j/artificial_psyarch

Date: 2026-06-11

This note records the local inspection of a third-party AP-inspired clean-room implementation artifact provided by the independent reproducer ACG-j. It is intended as an evidence planning record for APV2 paper and FAQ work.

## Audit Scope

Inspected local inputs:

- Repository checkout: `tmp_thirdparty_audit/artificial_psyarch`
- Remote: `https://github.com/ACG-j/artificial_psyarch.git`
- Commit: `ccb68aea6291c7e9ed507d5f576803bd99f65f5d`
- Commit author: `ation_ciger <ation_ciger@sgxi.cn>`
- Commit date: `2026-06-11T00:27:40+08:00`
- Commit subject: `Add relation scene probe runtime`
- Submitted workspace archive: `.ap.zip`
- `.ap.zip` SHA-256: `051589554123405652740729A02D5BD5A2B00EADDFA425AE2007BAC1EEAE7679`
- Extracted audit copy: `tmp_thirdparty_audit/acg_j_ap_zip_20260611/.ap`

Local rerun update:

- A follow-up local Rust rerun was completed after installing Rust and LLVM-MinGW tooling.
- See `docs/ThirdParty_ACGj_LocalRustRerun_Report_20260611.md`.
- Core report commands were locally rerun successfully. One Windows path-separator unit-test assertion remains as a bounded cross-platform test issue.

## Artifact Contents

The `.ap.zip` archive expands to 63 files with a total size of 673,526 bytes:

- 9 JSON files
- 4 `.apbin` skill package files
- 48 SVG media files
- 2 Markdown reports

Key artifact paths:

- `.ap/exports/bundles/ap-learning-bundle.json`
- `.ap/exports/bundles/scaffold-relation-zh-v1-strict-bundle.json`
- `.ap/exports/lessons/scaffold-relation-zh-v1-strict.json`
- `.ap/exports/lessons/scaffold-relation-zh-v1-holdout.json`
- `.ap/exports/media/relation_spatial_zh_strict/*.svg`
- `.ap/exports/media/relation_spatial_zh_holdout/*.svg`
- `.ap/reports/learning/generated_math_training_report.md`
- `.ap/reports/learning/relation-word-report.json`
- `.ap/reports/status/ap_status_report.md`
- `.ap/skills/external/skill.relation.spatial_words.zh.v1.apbin`
- `.ap/skills/interactive/current.apbin`

## Repository Shape

The repository presents itself as a Rust clean-room AP-Core minimal prototype inspired by the APV2.1 paper. The inspected checkout contains:

- `Cargo.toml` package name: `artificial_psyarch`
- Rust edition: 2024
- License: GPL-3.0
- Description: `Clean-room Rust AP-Core minimal prototype inspired by the APV2.1 paper.`
- 142 Rust source/test/bin files in the inspected tree
- 21 Rust files under `tests`
- 10 executable entrypoints under `src/bin`

Important bins:

- `ap_learn.rs`
- `ap_status_report.rs`
- `ap_tui.rs`
- `experiments_local.rs`
- `generated_math_report.rs`
- `language_grounding_report.rs`
- `paper_key_suite.rs`
- `relation_probe.rs`
- `relation_word_report.rs`
- `repeatmap_local.rs`

The README describes a bounded AP-Core experiment bench with prediction, action, feedback, memory, teacher modes, audit, skill package import/export, external JSON learning bridge, scaffold stages, local experiments, and TUI access. It explicitly frames current learning as a white-box auditable engineering loop rather than open-world large-model learning.

## Reported Metrics

### Status Report

Source: `.ap/reports/status/ap_status_report.md`

- Overall status: PASS
- `generated_math_train_accuracy`: 1.00
- `generated_math_holdout_accuracy`: 1.00
- `generated_math_generalization_accuracy`: 1.00
- `teacher_off_taint_audit`: PASS
- `experiment_count`: 13
- `event_count`: 1000
- `holdouts_passed`: true
- `validation_errors`: 0
- `suite_count`: 8
- `passed_suites`: 8
- `claim_count`: 8

The status report also states the current scope positively as completed AP-Core slices, teacher modes, local experiments, skill package reload, external JSON learning bridge, TUI learning commands, and generated math generalization. It bounds the current implementation away from open-ended conversation, live LLM provider calls, rich image/audio generation, and broad mathematics beyond the implemented expression parser.

### Generated Math Report

Source: `.ap/reports/learning/generated_math_training_report.md`

- Overall status: PASS
- `closed_loop`: true
- `train_tasks`: 89
- `memory_rows`: 89
- `train_accuracy`: 1.00
- `teacher_off_holdout_accuracy`: 1.00
- `teacher_off_generalization_accuracy`: 1.00
- `skill_reload_generalization_accuracy`: 1.00
- `untrained_operator_accuracy`: 0.00
- `taint_audit`: PASS

Generalization probes:

- `9 + 4 -> 13`
- `9 - 7 -> 2`
- `9 * 2 -> 18`
- `8 / 2 -> 4`
- `2 + 3 * 4 -> 14`
- `(2 + 3) * 4 -> 20`

Reload probes:

- `11 + 4 -> 15`
- `11 - 8 -> 3`
- `7 * 3 -> 21`
- `12 / 3 -> 4`
- `2 + 3 * 5 -> 17`
- `(2 + 3) * 5 -> 25`

Boundary probe:

- Untrained division-expression behavior returned `ObserveText`, matching the report's expected boundary behavior.

Interpretation:

- This is useful bounded evidence for a generated arithmetic learning loop with rewarded operators, teacher-off holdout, unseen expression generalization, skill persistence/reload, and a negative boundary for untrained operators.
- It should not be described as unrestricted mathematical reasoning.

### Relation Word Report

Source: `.ap/reports/learning/relation-word-report.json`

Task:

- Skill id: `skill.relation.spatial_words.zh.v1`
- Domain: `relation_words`
- Steps: 24
- Image refs: 24
- Unique image refs: 24
- Actions: 4 examples each for `RelationWordAbove`, `RelationWordBelow`, `RelationWordLeft`, `RelationWordParallel`, `RelationWordPerpendicular`, `RelationWordRight`
- Scenarios: `point_point`, `line_line`, `shape_shape`

Audit:

- Training audit: passed
- Holdout audit: passed

Scaffold metrics:

- `teacher_off_accuracy`: 1.0
- `cold_retest_accuracy`: 1.0
- `teacher_off_clean`: true
- `cold_retest_clean`: true
- `mastery_estimate`: 0.99999994
- `mastery_success_steps`: 96
- `mastery_failure_steps`: 0

Reload and holdout probes:

- Reload probe: accuracy 1.0, clean true, 24 attempts
- Holdout probe: accuracy 1.0, clean true, 24 attempts

Control probes:

- `geometry_only`: accuracy 1.0, clean true
- `no_geometry`: accuracy 0.0, clean true
- `shuffled_expected`: accuracy 0.0, clean true

Interpretation:

- This is the strongest artifact-side evidence in the submitted `.ap` archive because it combines teacher-off/cold-retest accuracy with holdout, reload, and controls that distinguish geometry-feature use from label/path/expected-answer leakage.
- It is still bounded to a relation-word skill slice and should not be treated as open-world visual-language understanding.

## Static Source Evidence

The source code contains explicit relation-word audit logic in `src/learning/relation_words.rs`:

- It requires six relation actions and three scenario classes.
- It defines leakage terms including relation labels, answer/action markers, action names, and label-like filename fragments.
- `RelationWordTrainingReport::passed()` requires training audit, holdout audit, teacher-off clean, cold-retest clean, teacher-off accuracy, cold-retest accuracy, reload probe, holdout probe, and control probes.
- `ControlProbeReport::passed()` requires geometry-only success, no-geometry at or below chance, and shuffled-expected failure.
- The audit rejects leakage terms in state items.

The prompt in `docs/relation_word_training_prompt.md` asks an external AI/agent to generate strict no-leakage visual relation curricula and to run the local framework. It requires train and holdout specs, unique images, neutral filenames, teacher-off and cold-retest without state/action/feedback, feedback-only without state/action biases, and control probes.

These source-level checks support the artifact's relevance as a no-leakage-oriented bounded learning reproduction, subject to clean rerun verification.

## Current Evidence Value

This artifact is useful as third-party clean-room AP-inspired bounded-mechanism evidence. After the local Rust rerun, it is stronger than preliminary artifact inspection, but it remains bounded to the mechanisms and reports that were actually rerun.

The strongest fair claim is:

> A third-party clean-room Rust implementation, independent from the local APV2 codebase and inspired by the AP paper principles, reports successful bounded reproductions of AP-style learning loops: teacher-on/off scaffolding, feedback memory, teacher-off holdout, cold retest, skill reload, generated arithmetic generalization, relation-word learning from geometry features, and leakage/control audits. Local artifact and source inspection support its relevance; clean-machine rerun and author confirmation remain pending.

It is appropriate for:

- Evidence planning
- Supplementary material preparation
- A third-party bounded reproduction entry in the evidence matrix
- Drafting a cautious paper/FAQ paragraph about independent implementation interest and locally rerun bounded mechanisms

It is not enough for:

- A claim that APV2 full runtime was independently reproduced
- A claim of open-world dialogue or broad language intelligence
- A claim that relation-word evidence is source-only without the external `.ap` curriculum/media artifact

## What Is Still Needed

To further strengthen this evidence, collect:

1. Reproducer permission to cite the repository, commit, reports, and artifact.
2. A frozen public tag, release archive, or signed commit reference.
3. Confirmation that `.ap.zip` was generated from commit `ccb68aea6291c7e9ed507d5f576803bd99f65f5d`.
4. Exact environment information:
   - OS and version
   - Rust version
   - Cargo version
   - Relevant environment variables, especially `AP_WORKSPACE` if used
5. Raw terminal logs for:
   - `cargo fmt --check`
   - `cargo check`
   - `cargo test`
   - `cargo clippy --all-targets --all-features -- -D warnings`
   - `cargo run --bin generated_math_report`
   - `cargo run --bin relation_word_report`
   - `cargo run --bin paper_key_suite`
6. A no-secret/no-provider/no-student-side-LLM statement for the reported teacher-off tests.
7. Ideally, an additional clean-machine rerun by another independent environment.

## Suggested Local Rerun Plan

When Rust/Cargo is available:

1. Copy or clone `tmp_thirdparty_audit/artificial_psyarch` to a clean temp directory.
2. Extract `.ap.zip` into that temp directory as `.ap`.
3. Run:

```bash
cargo fmt --check
cargo check
cargo test
cargo clippy --all-targets --all-features -- -D warnings
cargo run --bin generated_math_report
cargo run --bin relation_word_report
cargo run --bin paper_key_suite
```

4. Compare generated report metrics against the submitted `.ap` artifact.
5. Save raw logs and hashes under a local `outputs/thirdparty_acgj_audit_YYYYMMDD/` folder.

## Bottom Line

The provided `.ap` archive is enough for a serious artifact audit, especially when paired with the current ACG-j Rust repository checkout and the local rerun report. It meaningfully strengthens the project as an external clean-room AP-principle reproduction evidence line.

It is not enough to call the case fully closed for APV2 as a whole. The evidence should remain scoped to bounded AP-style mechanisms: teacher-off/cold-retest scaffolding, feedback learning, skill reload, generated arithmetic generalization, relation-word geometry learning, and no-leakage/control probes.
