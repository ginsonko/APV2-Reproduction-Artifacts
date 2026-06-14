# ACG-j Public-Freeze-Ready Local Evidence Bundle

Date: 2026-06-11T15:17:20

## Result

Status: `PASS`

This bundle packages the reviewed ACG-j Rust source snapshot and submitted `.ap` artifact into a local public-freeze-ready evidence set. It is ready to be attached to an owner-side public tag/release/archive once the third-party maintainer chooses to publish that release.

## Source And Artifact

- repository: `https://github.com/ACG-j/artificial_psyarch.git`
- commit: `ccb68aea6291c7e9ed507d5f576803bd99f65f5d`
- source archive: `H:\AP原型实验第二期\APV2.1版本原型测试\outputs\thirdparty_acgj_public_freeze_20260611\archives\artificial_psyarch_ccb68aea6291_source.zip`
- source archive SHA-256: `F2C229584EB80F55B0C8791F741816129593A1D7F2235658F5807AD378481EC5`
- submitted `.ap.zip` copy: `H:\AP原型实验第二期\APV2.1版本原型测试\outputs\thirdparty_acgj_public_freeze_20260611\archives\acgj_submitted_ap_20260611.zip`
- submitted `.ap.zip` SHA-256: `051589554123405652740729A02D5BD5A2B00EADDFA425AE2007BAC1EEAE7679`

## Environment

- platform: `Windows-10-10.0.19045-SP0`
- rustup: `rustup 1.29.0 (28d1352db 2026-03-05)`
- rustc: `rustc 1.96.0 (ac68faa20 2026-05-25)`
- cargo: `cargo 1.96.0 (30a34c682 2026-05-25)`
- linker: `C:\Users\Administrator\.rustup\toolchains\stable-x86_64-pc-windows-gnu\lib\rustlib\x86_64-pc-windows-gnu\bin\self-contained\x86_64-w64-mingw32-gcc.exe`
- LLVM-MinGW bin: `C:\Users\Administrator\AppData\Local\Microsoft\WinGet\Packages\MartinStorsjo.LLVM-MinGW.MSVCRT_Microsoft.Winget.Source_8wekyb3d8bbwe\llvm-mingw-20260602-msvcrt-x86_64\bin`

## Clean-Copy Rerun

- staging root: `C:\Users\ADMINI~1\AppData\Local\Temp\ap_acgj_public_freeze_20260611\source`
- `.ap` artifact extracted into staging source: `True`
- command count: `8`
- passed: `8`
- failed: `0`

| command | returncode | seconds | passed | log |
|---|---:|---:|---|---|
| `cargo_check` | `0` | `61.779` | `True` | `cargo_check.log` |
| `cargo_fmt_check` | `0` | `1.096` | `True` | `cargo_fmt_check.log` |
| `cargo_clippy_all_targets_all_features_D_warnings` | `0` | `26.262` | `True` | `cargo_clippy_all_targets_all_features_D_warnings.log` |
| `cargo_test_lib` | `0` | `77.067` | `True` | `cargo_test_lib.log` |
| `generated_math_report` | `0` | `36.937` | `True` | `generated_math_report.log` |
| `relation_word_report` | `0` | `8.971` | `True` | `relation_word_report.log` |
| `paper_key_suite` | `0` | `8.218` | `True` | `paper_key_suite.log` |
| `ap_status_report` | `0` | `8.015` | `True` | `ap_status_report.log` |

## Interpretation

Positive paper claim supported:

> The reviewed ACG-j Rust implementation can be packaged from the cited commit and rerun from a clean source snapshot with the submitted `.ap` artifact. The clean-copy rerun preserves the core AP-style bounded-mechanism evidence: source quality checks, 84/84 library tests, generated math reports, relation-word reports, paper key suite, and status report.

## Boundary

- This is a local public-freeze-ready bundle, not an owner-side GitHub release.
- Relation-word evidence is source plus submitted `.ap` curriculum/media artifact.
- The evidence supports third-party AP-style bounded-mechanism reproduction, not APV2 full-runtime reproduction or open-world dialogue completion.

## Next Step For Public Citation

The third-party maintainer can create a public tag/release/archive for commit `ccb68aea6291c7e9ed507d5f576803bd99f65f5d` and attach or cite this source archive, `.ap.zip` hash, logs, and manifest.
