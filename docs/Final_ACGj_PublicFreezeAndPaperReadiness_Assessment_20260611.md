# ACG-j Public-Freeze-Ready Evidence And Paper Readiness Final Report

Date: 2026-06-11

## 1. Design

Goal: harden the ACG-j third-party reproduction evidence beyond "local rerun" into a release-ready evidence bundle.

Design decision:

- Generate a source snapshot archive from the exact reviewed commit.
- Bind the submitted `.ap.zip` artifact by SHA-256.
- Re-run the core Rust evidence commands from a clean ASCII staging path.
- Store command logs, manifest, source archive, artifact copy, and a report in one output directory.
- Keep the wording precise: this is a local public-freeze-ready bundle, awaiting owner-side GitHub tag/release/archive.

Key fixed inputs:

- repo: `https://github.com/ACG-j/artificial_psyarch.git`
- commit: `ccb68aea6291c7e9ed507d5f576803bd99f65f5d`
- submitted `.ap.zip` SHA-256: `051589554123405652740729A02D5BD5A2B00EADDFA425AE2007BAC1EEAE7679`

Design doc:

- `docs/Design_ACGj_PublicFreezeAndCleanRerun_20260611.md`

## 2. Review

Review decision: approved.

Approved positive claim:

> A third-party Rust implementation reconstructed AP-style bounded mechanisms outside the original codebase, and the reviewed commit plus submitted `.ap` artifact can be packaged and rerun from a clean source snapshot with teacher-off/cold-retest, feedback learning, skill reload, generated math generalization, relation-word geometry learning, and control-probe evidence intact.

Boundary locked:

- not an owner-side GitHub release yet,
- not APV2 full-runtime reproduction,
- not open-world dialogue proof,
- relation-word evidence is source plus submitted `.ap` curriculum/media artifact.

Review doc:

- `docs/Review_ACGj_PublicFreezeAndCleanRerun_20260611.md`

## 3. Landing

Implemented script:

- `scripts/build_acgj_public_freeze_ready.py`

Generated output:

- `outputs/thirdparty_acgj_public_freeze_20260611/acgj_public_freeze_ready_manifest.json`
- `outputs/thirdparty_acgj_public_freeze_20260611/acgj_public_freeze_ready_report.md`
- `outputs/thirdparty_acgj_public_freeze_20260611/archives/artificial_psyarch_ccb68aea6291_source.zip`
- `outputs/thirdparty_acgj_public_freeze_20260611/archives/acgj_submitted_ap_20260611.zip`
- `outputs/thirdparty_acgj_public_freeze_20260611/logs/*.log`

Archive hashes:

- source archive SHA-256: `F2C229584EB80F55B0C8791F741816129593A1D7F2235658F5807AD378481EC5`
- `.ap.zip` SHA-256: `051589554123405652740729A02D5BD5A2B00EADDFA425AE2007BAC1EEAE7679`

Clean-copy rerun result:

- 8/8 command PASS
- `cargo check`: PASS
- `cargo fmt --check`: PASS
- `cargo clippy --all-targets --all-features -- -D warnings`: PASS
- `cargo test --lib`: PASS, 84/84
- `generated_math_report`: PASS
- `relation_word_report`: PASS
- `paper_key_suite`: PASS
- `ap_status_report`: PASS

Documents updated:

- `docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md`
- `docs/APV2_MainPaper_Supplement_Index_20260611.md`
- `docs/APV21_VideoFAQ_PublicInitialDraft_v1_0n_20260610.md`
- `docs/APV21_PublicPaper_InitialDraft_v1_0n_20260610.md`

## 4. Validation

Validation commands:

```powershell
python scripts\check_apv2_mainpaper_runtime_draft.py
rg -n "public-freeze-ready|F2C229584EB80F55B0C8791F741816129593A1D7F2235658F5807AD378481EC5|8/8 command|8/8 核心|owner-side|thirdparty_acgj_public_freeze_20260611|acgj_public_freeze_ready" docs/APV2_MainPaper_ArchitectureRuntime_Draft_20260611.md docs/APV2_MainPaper_Supplement_Index_20260611.md docs/APV21_VideoFAQ_PublicInitialDraft_v1_0n_20260610.md docs/APV21_PublicPaper_InitialDraft_v1_0n_20260610.md outputs/thirdparty_acgj_public_freeze_20260611/acgj_public_freeze_ready_report.md
```

Validation result:

- main paper checker: PASS
- manifest summary: `8/8` commands PASS
- source archive hash and `.ap.zip` hash verified in manifest and paper/FAQ docs
- docs explicitly say owner-side public release/tag/archive remains the next step
- no target paper/FAQ text claims owner-side GitHub release is already completed

## 5. Paper Evidence Strength After This Step

This step materially strengthens the APV2 paper.

Before this step, ACG-j evidence was:

- authorized,
- locally rerun,
- tied to commit and `.ap.zip` hash.

After this step, it is:

- source-archived from the reviewed commit,
- bound to a source archive SHA-256,
- bound to the submitted `.ap.zip` SHA-256,
- rerun from a clean source snapshot,
- accompanied by logs and manifest,
- integrated into the main paper, supplement index, FAQ, and long report.

This is close to the strongest artifact practice available before the third-party owner publishes an official release.

## 6. If Open-World Daily Chinese Dialogue Base Also Succeeds

If GL/OpenWorld later demonstrates a stable daily Chinese dialogue base under teacher-off/cold-retest/no-leakage conditions, the AP paper evidence chain becomes unusually strong for an independent prototype project:

1. AP-Core mechanism evidence: state pool, short-term slot, residual B recall, successor lag, feedback revision, persistence, parameter sensitivity, ablation.
2. AP-Core task evidence: KeySuite, RepeatMap, SPAD, STP-v2, representation ablation.
3. Third-party reproduction evidence: ACG-j Rust source-plus-artifact clean-copy rerun, 8/8 commands, 84/84 library tests.
4. Learning-protocol evidence: GL staged learning, teacher-off/cold-retest, no answer table, no regex route, no student-side LLM.
5. Open-world foundation evidence: if completed, reasonable responses to unknown/ambiguous/noisy daily inputs, honest uncertainty, clarification, learning from teacher demonstration, and cold retention.

At that point, the paper can credibly argue that AP is not only a theory or a single local demo, but a layered research program with mechanism, learning, reproduction, and early open-world evidence.

## 7. Is This The Highest Standard A Prototype Can Reach?

For a personal or small-team prototype, this is very near the highest realistic standard:

- white-box implementation,
- frozen artifacts,
- manifest/hash binding,
- local reruns,
- third-party independent implementation,
- ablations and controls,
- no-leakage audits,
- planned open-world foundation evaluation,
- clear separation between AP-Core, GL, and product shell.

The few standards above this are mostly resource-intensive rather than conceptually different:

- independent lab replication on their own machines,
- public benchmark comparison at larger scale,
- multi-month longitudinal deployment logs,
- formally packaged Docker/Nix/CI reproduction,
- peer-reviewed external adversarial audit.

Those would make the evidence even stronger, but they are not normally expected from an early independent architecture prototype.

## 8. Can Reviewers Still Give A Low Score?

Yes. Even strong evidence does not prevent low scores. Likely critique points:

- scope mismatch: reviewer expects AGI/open-world chatbot proof rather than architecture/runtime proof;
- paper length: the system is broad, and a long technical report can feel hard to evaluate;
- baseline pressure: reviewers may request stronger LLM-agent baselines or more tasks;
- novelty framing: some may see AP as a combination of memory, symbolic state, RL-like feedback, and cognitive architecture ideas unless the unique synthesis is stated crisply;
- scale: reviewers may want larger curriculum, more domains, or more users;
- engineering maturity: Python/Rust/local artifacts may be viewed as prototype-grade rather than production-grade;
- theory taste: endogenous cognitivism may be attractive to some reviewers and alien to others.

The right mitigation is not defensive wording. The right mitigation is:

- define the paper as a system architecture plus evidence paper,
- keep the claims positive and scoped,
- put detailed traces and long tables in appendix,
- show ablation/control results up front,
- present ACG-j as cross-implementation evidence,
- present GL/OpenWorld as learning evidence only after it passes,
- make the artifact easy to rerun.

## 9. Overall Assessment

Current paper strength after ACG-j public-freeze-ready evidence:

- Mechanism evidence: strong.
- Artifact discipline: strong locally, still needs public owner-side release.
- Third-party reproduction: strong for bounded AP-style mechanisms.
- Open-world language base: still pending GL/OpenWorld evidence.
- Submission readiness: much better, but still benefits from compression, public artifact release, and a final venue-specific positioning pass.

If the open-world daily Chinese dialogue base succeeds with honest unknown handling, teacher-off/cold-retest, and no hidden solver, then AP will have enough evidence for a serious architecture paper and possibly a companion learning-protocol paper. It would not be immune to reviewer disagreement, but it would no longer be easy to dismiss as only a speculative theory or one-off local demo.
