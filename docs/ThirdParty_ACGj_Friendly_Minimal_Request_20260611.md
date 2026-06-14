# ACG-j Third-Party Evidence: Friendly Minimal Request

Date: 2026-06-11

This note records a low-friction way to communicate with the third-party reproducer. The goal is to avoid asking for a long audit checklist directly. We should ask only for consent and provenance first, then do reproduction work ourselves whenever possible.

## Principle

Do not send the reproducer a long reviewer-style checklist.

Use a tiered approach:

1. Ask for permission to cite the public repo and the provided `.ap` artifact.
2. Ask for one provenance confirmation: whether the provided `.ap` artifact corresponds to the cited commit.
3. Ask for one boundary confirmation: whether the reported teacher-off tests avoided student-side LLM, hidden solver, provider calls, or answer-table leakage.
4. Handle rerun logs, environment capture, and evidence formatting ourselves.
5. If the reproducer is interested, offer a one-click script or GitHub Actions workflow as an optional convenience, not as a demand.

## Recommended Short Message

可以直接发这一版：

```text
你好，我们看了你这个 artificial_psyarch 仓库和你发来的 .ap artifact，感觉很有价值，想把它作为“第三方 clean-room AP-inspired 原理复现候选证据”记录到论文补充材料/项目证据表里。

为了避免麻烦你，我先只确认三件很简单的事：

1. 我们可以引用你的 GitHub 仓库和这份 .ap artifact 吗？
2. 这份 .ap artifact 是不是对应当前这个 commit 生成的？
   ccb68aea6291c7e9ed507d5f576803bd99f65f5d
3. 这些 teacher-off / cold-retest / relation-word / math 报告里，学生侧有没有使用 LLM/provider、隐藏 solver、答案表或关键词硬门？

其它复跑、日志整理、环境记录我们可以自己做，不需要你额外整理一大堆材料。之后如果你愿意，我们也可以给你一个一键脚本或 GitHub Actions workflow，自动跑 cargo test 和几个 report，然后自动打包日志。
```

## Even Shorter Message

如果担心上面仍然太正式，可以发这一版：

```text
你的 artificial_psyarch 和 .ap artifact 我们已经初步看过了，挺有价值的。我们想把它作为第三方 clean-room AP-inspired 复现候选证据记录下来。

想先确认一下：我们可以引用你的仓库和这份 artifact 吗？另外这份 .ap 是不是从 commit ccb68aea... 跑出来的？teacher-off 那些报告里学生侧没有用 LLM/provider/隐藏 solver/答案表吧？

其它复跑和日志我们自己处理，不麻烦你整理。
```

## Optional One-Click Follow-Up

Only send this if the reproducer asks how to help or actively wants to provide stronger evidence:

```text
如果你愿意帮忙加强证据，我们可以给你一个一键脚本或 GitHub Actions workflow。你只需要运行/点一下，它会自动执行：

- cargo fmt --check
- cargo check
- cargo test
- cargo run --bin generated_math_report
- cargo run --bin relation_word_report
- cargo run --bin paper_key_suite

然后把日志和报告打包。这个是可选项，不急；我们会尽量自己复跑。
```

## Evidence Levels

### Level 1: Permission + Provenance

Needed from reproducer:

- Permission to cite repo/artifact.
- Confirmation that `.ap` artifact corresponds to the named commit.
- Confirmation of no student-side LLM/provider/hidden solver/answer-table route for teacher-off reports.

Allowed claim:

> A third-party clean-room AP-inspired implementation and artifact have been inspected as a candidate independent reproduction of bounded AP-style mechanisms.

### Level 2: Public Freeze

Needed:

- Public tag/release or stable archive.
- Attached `.ap` artifact or documented generation command.

Allowed claim:

> A frozen third-party clean-room implementation provides reproducible artifact materials for bounded AP-style learning-loop evidence.

### Level 3: Independent Rerun

Needed:

- We or CI rerun the project from source.
- Logs and generated reports match the submitted artifact at the metric level.

Allowed claim:

> A third-party clean-room implementation was independently rerun and reproduced bounded AP-style teacher-off/cold-retest/skill-reload/control-probe results.

## Recommended Route

Use Level 1 now. It is polite, low-friction, and enough to justify keeping the evidence in planning and supplement drafts.

Then perform Level 3 ourselves when Rust/Cargo is available locally or through a clean CI/VM environment.
