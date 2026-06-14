# APV2 P1 Hardening Materials Final Report

Date: 2026-06-11

## 1. Goal

This round followed the required cycle:

1. design;
2. review and refinement;
3. implementation;
4. rigorous acceptance testing;
5. final report.

The goal was to continue AP-Core paper-material hardening after the P0 bottom-loop package, with emphasis on:

- formal figures;
- long-run interruption recovery;
- rhythm successor replay;
- real local persistence reload;
- artifact freeze.

Scope remains AP-Core runtime evidence only. This report does not claim GL learning-stage success, DPP/Skill37 dialogue generalization, or desktop-pet product capability.

## 2. Design

Design cold-save:

- `docs/Design_APV2_P1HardeningMaterials_20260610.md`

The design used the same boundary style as the P0 material package:

- define each experiment;
- explain why the mechanism matters;
- list observable evidence;
- state counterexamples / forbidden interpretations;
- give a concrete example.

## 3. Review And Refinement

The initial P1 script exposed two useful issues.

First, the real JSONL persistence boundary failed on non-JSON-native payload fields such as sets. This was a valid persistence-boundary failure, not a test artifact. The JSONL adapter was refined with recursive JSON cleaning so MemoryStore can persist the authoritative payload shape across a real local file boundary.

Second, the rhythm successor experiment initially failed because `ShortTermSlotPacketBuilder` recognized older rhythm traces using `dominant_peak`, while the current `RhythmChannel` exposes rhythm evidence through `family` and `channels`. This was a real integration gap between the rhythm channel and the short-term narrative slot. The slot builder was extended to accept the current `family/channels` rhythm trace shape and generate `short_term_slot::rhythm` from phase expectation, period, and groove.

## 4. Implementation

New files:

- `memory/persistence/jsonl_store.py`
- `experiments/apv2_p1_hardening_materials.py`
- `tests/test_apv2_p1_hardening_materials.py`
- `docs/Design_APV2_P1HardeningMaterials_20260610.md`
- `docs/FinalReport_APV2_P1HardeningMaterials_20260611.md`

Modified files:

- `memory/persistence/__init__.py`
- `memory/short_term/slot_packet.py`

Generated latest output:

- `outputs/apv2_p1_hardening_materials_20260611_000013/apv2_p1_hardening_materials.json`
- `outputs/apv2_p1_hardening_materials_20260611_000013/apv2_p1_hardening_materials_report.md`
- `outputs/apv2_p1_hardening_materials_20260611_000013/artifact_freeze_manifest.json`
- `outputs/apv2_p1_hardening_materials_20260611_000013/jsonl_persistence/apv2_memory.jsonl`

Generated figures:

- `outputs/apv2_p1_hardening_materials_20260611_000013/figures/apv2_runtime_loop.mmd`
- `outputs/apv2_p1_hardening_materials_20260611_000013/figures/state_pool_vs_short_term_slot.mmd`
- `outputs/apv2_p1_hardening_materials_20260611_000013/figures/residual_b_recall_absorption.mmd`
- `outputs/apv2_p1_hardening_materials_20260611_000013/figures/successor_lag_rhythm_replay.mmd`
- `outputs/apv2_p1_hardening_materials_20260611_000013/figures/evidence_layer_split.mmd`

## 5. Acceptance Results

P1 script:

- command: `python experiments\apv2_p1_hardening_materials.py`
- result: `4 pass / 0 partial / 0 fail`

P1 targeted tests:

- command: `python -m pytest tests\test_apv2_p1_hardening_materials.py -q`
- result: `4 passed in 1.30s`

P0 + P1 + existing bottom-loop regression:

- command: `python -m pytest tests\test_apv22_core_loop_acceptance.py tests\test_apv22_apcore_dynamics.py tests\test_apv2_bottom_loop_p0_materials.py tests\test_apv2_p1_hardening_materials.py -q`
- result: `19 passed, 1 warning in 11.19s`

The warning is the known Python `audioop` deprecation warning from `legacy_apv2\sensors\hearing_sensor_v1.py`. It does not affect this AP-Core material package.

## 6. What The Evidence Supports

`LongRun-InterruptionRecovery-1` supports the claim that AP-Core short-term narrative machinery can record interruption and resumption traces, keep positive slot virtual mass, and recover the earlier narrative in controlled focus-packet probes.

`RhythmSuccessor-Replay-1` supports the claim that AP-Core rhythm evidence can produce phase expectation, be carried into the short-term narrative slot, and coexist with successor lag shaping where lag 1 is the peak, lag 2 drops sharply, and later lags form a tail.

`PersistenceBackend-Reload-1` supports the claim that MemoryStore can cross a real local file persistence boundary through the same adapter contract: write snapshots to JSONL, instantiate a fresh store, warm-load, then recover state B recall, C successor prediction, and short-term-slot recall.

`ArtifactFreeze-1` supports local pre-public traceability: source files, tests, designs, and figures are recorded with size and SHA-256 hashes.

## 7. Boundaries

This package does not prove:

- GL learning protocol stages;
- DPP/Skill37 open-dialogue learning;
- product-shell / desktop-pet capability;
- music performance;
- PostgreSQL production deployment;
- public DOI-level release freeze.

It also does not use or introduce:

- keyword hard gates;
- regex routes;
- answer tables;
- student-side LLM;
- hidden solvers;
- full-sentence action macros.

## 8. Paper Use

These materials can now support a stronger APV2 paper structure:

- Mechanisms section: use the runtime, state-pool/slot, residual recall, and rhythm/successor figures.
- Evidence section: cite P0 and P1 bottom-loop material reports.
- Methods appendix: include default parameter table from P0 and persistence/reload details from P1.
- Boundary section: keep GL and product-shell claims separate from AP-Core evidence.

Recommended next paper step:

1. prepare a concise APV2 architecture/runtime main-paper draft;
2. keep the current long paper as the technical report;
3. move long schema, FAQ, and failure-boundary details into appendix/report;
4. wait for GL-side learning results before writing the separate learning-protocol evidence paper.

