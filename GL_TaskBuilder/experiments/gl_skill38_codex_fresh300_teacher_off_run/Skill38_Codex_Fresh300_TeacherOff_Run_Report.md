# Skill38 Codex Fresh300 Teacher-Off 结果报告

## 本轮结论

本轮完成冻结题库 teacher-off 作答与 Codex 事后阅卷，结果为 `300/300`，目标阈值 `>=290/300`，Fresh300 teacher-off gate: `True`。

结论边界：这是 GL 冻结题库 teacher-off harness 的结果，不是 AP-Core runtime proof，也不证明广域开放世界中文对话成熟。

## 关键指标

- case_count: `300`
- pass_count: `300`
- failure_count: `0`
- bank_sha256: `c55e39e307092295568e417e01f17978aaf297748054674d9b7b03bc6ab35f5e`
- no_leakage_pass: `300/300`
- repair_trace_count: `60`

## 类别分数

- `affective_companion_task_switch` / 陪伴情绪到任务切换: `50/50` avg `100.0`
- `delayed_episode_topic_shift` / 延迟 episode 话题切换: `50/50` avg `100.0`
- `multi_intent_latest_focus` / 多意图最新焦点: `50/50` avg `100.0`
- `repair_after_recent_memory_interference` / 近期记忆干扰修订: `60/60` avg `100.0`
- `subjective_experience_boundary` / 主观体验边界: `45/45` avg `100.0`
- `time_language_short_interval` / 时间语言短间隔: `45/45` avg `100.0`

## 审查边界

`student_side_llm=false`；学生侧只接收 student_visible.turns；Codex judge 在 commit_reply 之后运行；无 answer table、regex answer route、关键词硬门、整句动作宏或 hidden solver。
