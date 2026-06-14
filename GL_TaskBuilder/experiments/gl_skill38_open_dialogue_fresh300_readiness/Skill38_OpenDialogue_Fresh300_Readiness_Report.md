# Skill38 开放对话 Fresh300 Readiness 报告

## 本轮结论

第二批更嘈杂开放对话微领域 readiness gate 已完成。它不是 Fresh300 本身，而是为冻结 Codex Fresh300 题库做前置验收。

- passed: `True`
- domain_pass: `6/6`
- cold_retest_pass: `6/6`
- ablation_degradation_observed: `6/6`
- stage_order_pass: `6/6`
- fresh300_readiness_gate_passed: `True`
- live_fresh300_run: `False`

## 领域结果

### 多意图下最新焦点优先

- domain_id: `multi_intent_latest_focus`
- teacher-off: `reply_family::ack_latest_focus`
- cold: `reply_family::ack_latest_focus`
- ablation: `reply_family::old_focus_pollution`
- conclusion: 旧奖励焦点存在时，当前输入仍能取得优先权；去掉 current_focus_support 后旧焦点污染。

### 话题切换后的延迟 episode 回忆

- domain_id: `delayed_episode_topic_shift`
- teacher-off: `reply_family::delayed_subject_recall`
- cold: `reply_family::delayed_subject_recall`
- ablation: `reply_family::topic_shift_lost_subject`
- conclusion: 插入天气、午饭和消息提醒后仍能回到风铃主体；去掉短期槽后主体丢失。

### 主观体验边界

- domain_id: `subjective_experience_boundary`
- teacher-off: `reply_family::no_subjective_experience_claim`
- cold: `reply_family::no_subjective_experience_claim`
- ablation: `reply_family::fabricated_personal_experience`
- conclusion: 主观体验边界能压住编造倾向；去掉 experience_gap 后会出现伪体验。

### 时间语言短间隔 grounding

- domain_id: `time_language_short_interval`
- teacher-off: `reply_family::time_grounded_ack`
- cold: `reply_family::time_grounded_ack`
- ablation: `reply_family::unsafe_time_literal_guess`
- conclusion: 时间词通过 timefelt 和短期槽进入过程，而不是 regex 回复规则。

### 近期记忆干扰后的修订回退

- domain_id: `repair_after_recent_memory_interference`
- teacher-off: `reply_family::self_repair_current_answer`
- cold: `reply_family::self_repair_current_answer`
- ablation: `reply_family::polluted_old_memory_commit`
- conclusion: 被旧蓝纸鹤污染时能回读、擦除并改回小纸船；去掉 dissonance 后旧记忆提交。

### 陪伴情绪到明确任务的切换

- domain_id: `affective_companion_task_switch`
- teacher-off: `reply_family::gentle_task_switch`
- cold: `reply_family::gentle_task_switch`
- ablation: `reply_family::emotion_overrides_task_request`
- conclusion: 情绪慢量调节语气，但不会命令最终回复；明确任务出现后能温和切换。

## Fresh300 计划

下一步是冻结 Codex Fresh300 题库：300 题，目标阈值 >=290/300，Codex 只做外部出题和事后评分，学生侧保持 student_side_llm=false。
