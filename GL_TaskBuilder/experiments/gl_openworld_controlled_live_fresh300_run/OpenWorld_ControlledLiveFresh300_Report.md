# OpenWorld-Foundation 受控 Live Fresh300 尝试

## 实验设计

冻结 300 条实际中文开放题面；学生侧 teacher-off，student_side_llm=false，无 provider、无答案表、无 regex route、无整句动作宏、无 hidden solver。行动由过程召回与行动后果评估竞争产生，Codex 只在提交后阅卷。

## 本轮结论

- passed: `True`
- Live Fresh300: `300/300`
- threshold: `>=290`
- average score: `100.0`
- reply unique: `294`
- ablation: `6/6`

## 审查边界

- 这是 GL 受控 Live Fresh300 尝试，不是 AP-Core runtime full proof。
- 不宣称自然语言对话基座已经完成。
- Codex 是事后阅卷老师，不进入学生侧作答链。