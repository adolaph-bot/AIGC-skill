---
name: scene-breakdown
version: 1.0.0
module: storyboard
stage: foundation
description: 将完整剧本拆成清晰的 Scene 单元，为分镜和素材生产建立结构。
---

# Scene Breakdown

## 目标

把剧本从“故事文本”转换成“制作单元”。

Scene 是地点、时间和连续动作相对稳定的一段剧情。

## 什么时候使用

- 已经有剧本
- 准备开始分镜
- 需要统计地点、人物和素材
- 需要估算项目复杂度

## Scene 切分规则

通常在以下情况建立新 Scene：

- 地点改变
- 时间发生明显跳跃
- 连续动作被打断
- 剧情进入新的事件单元

不要因为一句对白就建立新 Scene。

## Inputs

- script
- target_duration
- character_bibles（如已有）

## Steps

### Step 1 — 找场景边界

标记：

- location change
- time change
- major event transition

### Step 2 — 给每个 Scene 分配 ID

格式：

```text
SCENE_001
SCENE_002
SCENE_003
```

### Step 3 — 提取生产信息

每个 Scene 至少包含：

- location
- time
- characters
- props
- action
- dialogue
- emotional_goal
- story_function

### Step 4 — 估算 Scene 时长

总和应接近目标视频时长。

### Step 5 — 检查生产复杂度

标记：

- NEW_LOCATION
- NEW_CHARACTER
- COSTUME_CHANGE
- CROWD
- COMPLEX_ACTION
- VFX_HEAVY

如果 30–60 秒作品出现过多高复杂度标签，应建议简化。

## Output Schema

```yaml
scenes:
  - scene_id:
    location:
    time:
    estimated_duration:
    characters:
    props:
    action_summary:
    dialogue:
    emotional_goal:
    story_function:
    continuity_from_previous:
    complexity_flags:

project_summary:
  scene_count:
  unique_locations:
  unique_characters:
  difficult_scenes:
```

## Quality Check

- [ ] Scene 边界合理
- [ ] 场景数量不过度碎片化
- [ ] 每个 Scene 有明确剧情功能
- [ ] 时长总和基本合理
- [ ] 人物和地点已经统计
- [ ] 可以直接进入 storyboard-generator

## Learning Mode

先给用户一小段剧本，让用户自己判断：

> “什么时候应该切新场景？”

用户完成后再解释判断依据。

## Next

```text
scene-breakdown
→ storyboard-generator
```
