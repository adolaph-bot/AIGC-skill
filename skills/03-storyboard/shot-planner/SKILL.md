---
name: shot-planner
version: 1.0.0
module: storyboard
stage: foundation
description: 把单个分镜补全为可直接交给图像、视频、声音和剪辑模块的镜头计划。
---

# Shot Planner

## 目标

将一个基础 Shot 转成完整的“生产镜头卡”。

这是 Storyboard 与真正生成媒体之间的桥梁。

## Inputs

必需：

- storyboard shot
- character bible（涉及核心角色时）

可选：

- visual style
- aspect ratio
- target platform
- dialogue
- reference images

## 镜头设计字段

### Framing

- ECU
- CU
- MCU
- MS
- MLS
- WS
- EWS

### Angle

- eye level
- high angle
- low angle
- bird's-eye
- worm's-eye
- dutch angle
- over-the-shoulder

### Camera Movement

优先使用真实摄影中可理解的运动：

- static
- pan
- tilt
- dolly in
- dolly out
- truck left/right
- pedestal
- crane
- orbit
- handheld
- rack focus（光学/焦点变化）

避免一条镜头同时给多个互相冲突的运动。

### Lighting

写具体光源与方向，例如：

- soft window light
- cold fluorescent ceiling light
- warm sunset backlight
- neon rim lighting

少写空泛的：

- beautiful lighting
- masterpiece lighting

## Steps

### Step 1 — 明确 Shot Intent

一句话：

> 这个镜头希望观众注意什么、感受什么？

### Step 2 — 选择景别和角度

根据叙事目的选择。

例：

- 情绪 → CU / MCU
- 环境 → WS / EWS
- 强势人物 → low angle
- 脆弱 / 被压迫 → high angle（视剧情）

### Step 3 — 设计镜头运动

默认优先：

> 能静态就不要无意义运动。

运动必须服务情绪或信息。

### Step 4 — 补齐环境与光线

描述真实可见信息。

### Step 5 — 锁定角色连续性

从 Character Bible 引用：

`canonical_character_description`

不得擅自改变稳定外观。

### Step 6 — 生成 Image Prompt Draft

推荐结构：

```text
[framing + angle]
+ [canonical character]
+ [visible action]
+ [environment]
+ [lighting]
+ [composition / lens]
+ [visual style]
```

### Step 7 — 生成 Video Prompt Draft

推荐结构：

```text
[subject motion]
+ [camera motion]
+ [environment motion]
+ [timing / intensity]
+ [continuity constraints]
```

视频 Prompt 不要重复堆砌静态画质词。

### Step 8 — 声音与剪辑占位

记录：

- dialogue
- ambience
- sfx
- music_cue
- transition_in
- transition_out

这里只规划，不生成。

## Output Schema

```yaml
shot_id:
scene_id:
duration:

intent:
framing:
angle:
camera_movement:
lens:
composition:
lighting:

characters:
  - character_id:
    canonical_description:
    action:
    expression:

environment:
foreground:
background:

image_prompt_draft:
video_prompt_draft:

audio_plan:
  dialogue:
  ambience:
  sfx:
  music_cue:

edit_plan:
  transition_in:
  transition_out:

continuity_constraints:
risk_flags:
```

## Risk Flags

遇到以下情况标记：

- TOO_MANY_ACTIONS
- CONFLICTING_CAMERA_MOVES
- IDENTITY_RISK
- COSTUME_CONTINUITY_RISK
- COMPLEX_HAND_INTERACTION
- CROWD_COMPLEXITY
- TRANSFORMATION_HEAVY
- TEXT_IN_IMAGE

## Quality Check

- [ ] 镜头目的明确
- [ ] 景别和角度服务剧情
- [ ] 镜头运动不冲突
- [ ] 角色描述来自 Character Bible
- [ ] Image Prompt 与 Video Prompt 职责分开
- [ ] 视频 Prompt 明确“什么在动”
- [ ] 有时长
- [ ] 有声音/剪辑占位
- [ ] 风险已标记

## Learning Mode

用户学习时，每次只训练一个维度。

建议顺序：

1. 景别
2. 机位
3. 镜头运动
4. 光线
5. 图像 Prompt
6. 视频 Motion Prompt

不要一次把全部摄影术语灌给初学者。

## Next

后续应连接：

```text
shot-planner
→ image-generator
→ image-to-video / text-to-video
→ audio
→ editing
```
