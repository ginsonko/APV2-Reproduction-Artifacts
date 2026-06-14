# ACG-j/artificial_psyarch Local Rust Rerun Report

Date: 2026-06-11

This report records the local rerun of the third-party `ACG-j/artificial_psyarch` Rust implementation and the accompanying `.ap` artifact.

## Result

Local rerun succeeded for the core evidence commands.

Evidence status after this pass:

> The ACG-j clean-room Rust implementation is no longer only an inspected third-party artifact. Its core reports were locally rebuilt and rerun from the cited commit on this machine, with bounded caveats noted below.

This supports using it as external clean-room AP-inspired bounded-mechanism reproduction evidence in supplement/evidence-matrix material. It should still be described as a bounded AP-style reproduction, not as APV2 full-runtime reproduction or open-world dialogue proof.

## Source And Artifact

- Repository: `https://github.com/ACG-j/artificial_psyarch.git`
- Local audit checkout: `tmp_thirdparty_audit/artificial_psyarch`
- Rerun source copy: `C:\Users\ADMINI~1\AppData\Local\Temp\ap_acgj_rerun_20260611\artificial_psyarch`
- Clean-source rerun copy: `C:\Users\ADMINI~1\AppData\Local\Temp\ap_acgj_clean_rerun_20260611\artificial_psyarch`
- Commit: `ccb68aea6291c7e9ed507d5f576803bd99f65f5d`
- Submitted artifact: `.ap.zip`
- Submitted artifact SHA-256: `051589554123405652740729A02D5BD5A2B00EADDFA425AE2007BAC1EEAE7679`

The `.ap` artifact was extracted into the rerun source copy for the relation-word report, because that report depends on external relation curriculum/media files under `.ap/exports`.

## Environment

Rust was installed locally for this rerun.

- `rustup`: `rustup 1.29.0 (28d1352db 2026-03-05)`
- `rustc`: `rustc 1.96.0 (ac68faa20 2026-05-25)`
- `cargo`: `cargo 1.96.0 (30a34c682 2026-05-25)`
- Default host: `x86_64-pc-windows-gnu`
- Additional toolchain: `MartinStorsjo.LLVM-MinGW.MSVCRT 22.1.7-20260602`

Implementation note:

- The initial build failed under the Chinese workspace path because Windows GNU linker tooling did not reliably handle the non-ASCII target path.
- The successful rerun used a pure ASCII temp path.
- The successful rerun also used Rust's self-contained GNU linker with LLVM-MinGW binutils/tools available in `PATH`.

This is an environment requirement, not an AP mechanism issue.

## Commands And Outcomes

### Source Quality / Build

- `cargo check`: PASS
- `cargo fmt --check`: PASS
- `cargo clippy --all-targets --all-features -- -D warnings`: PASS
- `cargo test --lib`: PASS, 84/84 library tests passed

### Full Test Caveat

`cargo test` compiled the project and ran the test suite, but one bin-unit test failed on Windows:

- Failing test: `src/bin/relation_word_report.rs::tests::args_default_to_workspace_paths`
- Failure type: path separator mismatch
- Actual: `.ap\exports/lessons\scaffold-relation-zh-v1-strict.json`
- Expected: `.ap/exports/lessons/scaffold-relation-zh-v1-strict.json`

This is a cross-platform path formatting assertion. It does not affect the library tests or the report commands below.

### Report Commands With Submitted `.ap` Artifact

All core report commands completed with exit code 0:

- `cargo run --bin generated_math_report`: PASS
- `cargo run --bin relation_word_report`: PASS
- `cargo run --bin paper_key_suite`: PASS
- `cargo run --bin ap_status_report`: PASS

Generated logs and command summaries are stored under:

- `outputs/thirdparty_acgj_rerun_20260611/`

Machine-readable rerun summary:

- `outputs/thirdparty_acgj_rerun_20260611/rerun_summary.json`

## Clean-Source Rerun

A separate clean source copy was created without the submitted `.ap` directory.

Outcomes:

- `cargo run --bin generated_math_report`: PASS
- `cargo run --bin paper_key_suite`: PASS
- `cargo run --bin ap_status_report`: PASS
- `cargo run --bin relation_word_report`: expected failure because relation curriculum/media files were absent

Interpretation:

- Generated math and key-suite/status evidence can be regenerated from source.
- Relation-word evidence is intentionally source plus external curriculum/media artifact. It should be cited as a source-plus-artifact rerun, not as source-only.

## Rerun Metrics

### Generated Math

The rerun generated:

- `status: PASS`
- `closed_loop: true`
- `train_accuracy: 1.00`
- `teacher_off_holdout_accuracy: 1.00`
- `teacher_off_generalization_accuracy: 1.00`
- `skill_reload_generalization_accuracy: 1.00`
- `untrained_operator_accuracy: 0.00`
- `taint_audit: PASS`

The rerun showed 114 train tasks / memory rows, while the submitted artifact report showed 89. This difference is expected because the rerun environment had fresh/generated current run state and/or accumulated generated cases. The key accuracy, reload, generalization, and boundary metrics remained aligned.

### Relation Words

The source-plus-artifact rerun generated:

- `steps`: 24
- `image_refs`: 24
- `unique_image_refs`: 24
- Training audit: passed
- Holdout audit: passed
- `teacher_off_accuracy`: 1.0
- `cold_retest_accuracy`: 1.0
- `teacher_off_clean`: true
- `cold_retest_clean`: true
- Reload probe accuracy: 1.0
- Holdout probe accuracy: 1.0
- Control `geometry_only` accuracy: 1.0
- Control `no_geometry` accuracy: 0.0
- Control `shuffled_expected` accuracy: 0.0

This matches the key submitted artifact claims and is the strongest local rerun evidence for the third-party artifact.

### Status Report

The rerun generated:

- `status: PASS`
- `generated_math_train_accuracy`: 1.00
- `generated_math_holdout_accuracy`: 1.00
- `generated_math_generalization_accuracy`: 1.00
- `teacher_off_taint_audit`: PASS
- `holdouts_passed`: true
- `validation_errors`: 0
- `suite_count`: 8
- `passed_suites`: 8
- `claim_count`: 8

Experiment/event counts increased relative to the submitted `.ap` status report because the local rerun wrote additional events. This is expected and does not weaken the pass/fail or clean/probe conclusions.

## Claim Boundary

Positive claim now supported:

> A third-party clean-room Rust implementation of AP-inspired mechanisms was locally rerun from the cited commit. The rerun reproduced bounded learning-loop evidence including teacher-off/cold-retest behavior, generated math generalization with reload and untrained-boundary behavior, relation-word learning from geometry features, relation skill reload, holdout probes, and no-leakage/control probes.

Boundary:

- This is not APV2 full-runtime reproduction.
- This is not open-world dialogue proof.
- Relation-word reproduction is source plus `.ap` curriculum/media artifact, not source-only.
- One Windows-only path separator test failure remains in a bin argument-default test; core library tests and report commands passed.

## Recommended Paper Usage

Use in supplement/evidence matrix now:

> We also inspected and locally reran an independent clean-room Rust AP-inspired implementation by ACG-j. On Windows with a Rust GNU toolchain and LLVM-MinGW binutils, the third-party implementation rebuilt successfully and reproduced its bounded report-level results for generated arithmetic and visual relation-word learning. The relation-word artifact includes teacher-off and cold-retest cleanliness, skill reload, independent holdout, and control probes separating geometry features from path/label leakage. We treat this as bounded third-party AP-principle reproduction evidence, not as APV2 full-runtime or open-world dialogue proof.

Main paper usage should remain concise unless the venue welcomes reproduction artifacts.

## Logs

Important local logs:

- `outputs/thirdparty_acgj_rerun_20260611/environment.txt`
- `outputs/thirdparty_acgj_rerun_20260611/toolchain_paths_after_llvm_mingw.txt`
- `outputs/thirdparty_acgj_rerun_20260611/self_linker_llvm_tools_env.txt`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_test_self_linker_llvm_tools.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_test_lib.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_check.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_fmt_check_after_component.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_clippy_all.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_run_generated_math_report.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_run_relation_word_report.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_run_paper_key_suite.log`
- `outputs/thirdparty_acgj_rerun_20260611/cargo_run_ap_status_report.log`
- `outputs/thirdparty_acgj_rerun_20260611/rerun_summary.json`
