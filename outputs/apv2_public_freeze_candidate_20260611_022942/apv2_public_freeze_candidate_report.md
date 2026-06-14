# APV2 Public Freeze Candidate Report

Generated: `2026-06-10T18:29:44.425608+00:00`

## Scope

- scope: `AP-Core architecture/runtime main-paper reproducibility candidate`
- not_scope: `GL learning proof / DPP / Skill37 / desktop-pet product-shell proof`
- repository_status: `not_git_repository`

## Summary

- file_count: `163`
- total_bytes: `3484270`
- zip_path: `H:\AP原型实验第二期\APV2.1版本原型测试\outputs\apv2_public_freeze_candidate_20260611_022942\apv2_public_freeze_candidate.zip`
- zip_bytes: `1116294`
- zip_sha256: `f14b78e982410e8e997bdcd3912e1512b3d3b419d5b17ad1744a1634bd19caed`
- secret_like_finding_count: `0`
- missing_requested_inputs: `[]`

## Category Summary

| category | files | bytes |
|---|---:|---:|
| AP-Core paper experiment | 3 | 81164 |
| AP-Core paper test | 5 | 18216 |
| AP-Core runtime dependency | 98 | 2009185 |
| Frozen paper evidence output | 25 | 1037594 |
| Other included file | 4 | 91959 |
| Package metadata | 1 | 411 |
| Paper documentation | 16 | 108866 |
| Paper reproducibility script | 4 | 45325 |
| Runtime support dependency | 7 | 91550 |

## Required Rerun Commands

- `python scripts\check_apv2_mainpaper_runtime_draft.py`
- `python -m pytest tests\test_apv2_publication_figures_supplement.py tests\test_apv2_bottom_loop_p0_materials.py tests\test_apv2_p1_hardening_materials.py tests\test_apv2_p2_stress_mechanism_evidence.py tests\test_apv2_public_freeze_clean_room.py -q`

## Boundary

This package strengthens AP-Core runtime traceability. It does not claim GL learning proof, DPP/Skill37 open-dialogue proof, product-shell proof, DOI-level release, or independent third-party replication.
