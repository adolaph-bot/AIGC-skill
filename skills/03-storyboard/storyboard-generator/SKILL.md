---
name: storyboard-generator
version: 1.0.0
module: storyboard
stage: foundation
description: 将 Scene 拆为连续镜头，并为后续关键帧生成建立清晰的视觉分镜结构。
---

# Storyboard Generator

## 目标

把每个 Scene 转换成一系列 **Shot**。

它回答的不是“故事发生什么”，而是：

> 观众具体会看到什么？

## 什么时候使用

- Scene Breakdown 已完成
- 准备画分镜或生成关键帧
- 需要确定镜头数量、镜头顺序和视觉重点

## 核心原则

### 一个 Shot 只承担一个主要视觉任务

避免：

> 人走进房间、坐下、拿起手机、接电话、跑出去、天空爆炸

全部塞在一个 Shot。

应该拆开。

### 每个镜头必须有存在理由

常见功能：

- Establish
- Reveal
- Reaction
- Action
- Detail
- Transition
- Payoff

### 短视频不要过度切镜

30 秒初学项目通常优先控制在约 5–10 个有效镜头，而不是几十个碎镜头。

## Inputs

- scenes
- character_bibles
- target_duration
- aspect_ratio
- visual_style（可选）

## Steps

### Step 1 — 为 Scene 定义视觉目的

一句话回答：

> 这个 Scene 最重要的画面信息是什么？

### Step 2 — 拆 Shot

每个 Shot 记录：

- shot_id
- scene_id
- purpose
- subject
- visible_action
- environment
- emotional_beat

### Step 3 — 初步选择景别

可选基础集合：

- ECU — Extreme Close-Up
- CU — Close-Up
- MCU — Medium Close-Up
- MS — Medium Shot
- MLS — Medium Long Shot
- WS — Wide Shot
- EWS — Extreme Wide Shot

### Step 4 — 定义镜头衔接

考虑：

- Establish → Detail
- Action → Reaction
- Wide → Close
- Question → Reveal

### Step 5 — 分配时长

保证镜头时长之和与 Scene 时长一致。

### Step 6 — 标记关键帧需求

每个 Shot 默认至少需要一个关键帧。

如果镜头存在明显前后状态变化，可标记：

- start_frame
- end_frame

## Output Schema

```yaml
storyboard:
  - shot_id:
    scene_id:
    purpose:
    duration:
    framing:
    subject:
    visible_action:
    environment:
    emotional_beat:
    continuity_notes:
    keyframe_requirement:
      type:
      description:

summary:
  total_shots:
  total_duration:
  high_priority_shots:
```

## 不在本 Skill 做的事情

不要在这里完成：

- 完整视频模型参数
- 最终图像 Prompt
- 最终运动 Prompt
- TTS
- 剪辑

这些交给后续 Skill。

## Quality Check

- [ ] 每个 Shot 只有一个主要视觉任务
- [ ] Shot 顺序能看懂剧情
- [ ] 没有突然出现未定义角色/道具
- [ ] 总时长合理
- [ ] 有建立镜头和重点镜头
- [ ] 每个镜头可以进一步交给 shot-planner

## Learning Mode

先让用户选一个 Scene，自己尝试拆成 3–5 个镜头。

老师只给提示：

- 第一镜观众需要先知道什么？
- 哪一刻值得特写？
- 哪个反应必须被看到？

## Next

```text
storyboard-generator
→ shot-planner
```
