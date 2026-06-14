# APV2 Same-Machine Clean-Room Rerun Report

Generated: `2026-06-10T18:30:14.350027+00:00`

## Scope

- scope: `AP-Core architecture/runtime main-paper reproducibility candidate`
- rerun_level: `same_machine_clean_room_staging_copy`
- source_package: `outputs\apv2_public_freeze_candidate_20260611_022942\package`
- staging_root: `H:\AP原型实验第二期\APV2.1版本原型测试\outputs\apv2_clean_room_rerun_20260611_022953\stage`
- all_passed: `True`

## Commands

| command | returncode | seconds | passed |
|---|---:|---:|---|
| `python scripts\check_apv2_mainpaper_runtime_draft.py` | 0 | 0.185 | True |
| `python -m pytest tests\test_apv2_publication_figures_supplement.py tests\test_apv2_bottom_loop_p0_materials.py tests\test_apv2_p1_hardening_materials.py tests\test_apv2_p2_stress_mechanism_evidence.py tests\test_apv2_public_freeze_clean_room.py -q` | 0 | 19.903 | True |

## Boundary

This is a same-machine clean-room rerun from a copied freeze package. It is stronger than running in the original workspace, but weaker than an independent clean-machine or third-party reproduction.
