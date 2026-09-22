---
name: character-bible
version: 1.0.0
module: character
stage: foundation
description: 为 AIGC 连续创作建立稳定、可重复引用的角色身份与视觉规则。
---

# Character Bible

## 目标

建立角色的唯一事实来源（Single Source of Truth）。

后续生图、分镜、视频、配音都应该优先读取 Character Bible，而不是每次重新描述角色。

## 什么时候使用

- 一个角色会出现在多个镜头
- 需要保持人物外貌、服装、声音、道具一致
- 准备生成表情组、多角度或角色参考图
- AI 漫剧、连续短片、系列角色

## 什么时候不要使用

- 路人只出现一次且不重要
- 单张概念图
- 用户已经提供完整、可靠且结构化的 Character Bible

## 核心原则

### 1. Stable Traits 与 Variable Traits 分离

**Stable Traits** 默认不能随镜头变化：

- 基础脸部特征
- 发型
- 年龄感
- 身材
- 核心服装
- 标志性配饰
- 身份特征

**Variable Traits** 可以按剧情变化：

- 表情
- 姿势
- 镜头角度
- 光照
- 临时道具
- 污渍、雨水等剧情状态

### 2. 描述必须可见

优先：

> 黑色短发、偏瘦、灰色连帽卫衣

少用：

> 有破碎感、灵魂孤独、命运感很强

抽象人格可以作为表演信息，但不能替代视觉描述。

### 3. 不要每个镜头重新发明角色

后续生成必须引用同一 `character_id`。

## Inputs

必需：

- `character_name`
- `story_role`

可选：

- 用户已有角色图
- 剧本
- 年龄
- 性别表达
- 风格
- 服装
- 标志性道具
- 声音需求

## Steps

### Step 1 — 确定身份

生成稳定 ID：

```text
CHARACTER_<NAME>_<NUMBER>
```

例如：

```text
CHARACTER_LIN_CHUAN_01
```

### Step 2 — 定义 Stable Visual Identity

至少包含：

- age_appearance
- face
- hair
- body
- skin
- default_outfit
- footwear
- signature_accessories
- signature_props

### Step 3 — 定义表演特征

- posture
- habitual_expression
- movement_style
- personality_keywords

### Step 4 — 定义连续性规则

明确：

- MUST_KEEP
- MAY_CHANGE
- NEVER_CHANGE_WITHOUT_STORY_REASON

### Step 5 — 规划 Reference Pack

核心角色建议最终准备：

- front portrait
- 3/4 portrait
- side profile
- full body front
- full body back
- expression sheet
- optional pose sheet

这些是后续视觉 Skill 的任务，本 Skill 只定义需求。

### Step 6 — 声音身份占位

即使现在还未做 TTS，也保留：

- voice_id
- age_feel
- pitch
- speaking_rate
- emotional_baseline
- reference_audio

## Output Schema

```yaml
character_id:
name:
story_role:

stable_visual_identity:
  age_appearance:
  face:
  hair:
  body:
  skin:
  default_outfit:
  footwear:
  signature_accessories:
  signature_props:

performance:
  posture:
  habitual_expression:
  movement_style:
  personality_keywords:

continuity:
  must_keep:
  may_change:
  never_change_without_story_reason:

reference_pack:
  required_views:
  expression_set:
  pose_set:

voice_profile:
  voice_id:
  age_feel:
  pitch:
  speaking_rate:
  emotional_baseline:
  reference_audio:

prompt_anchor:
  canonical_character_description:
```

## Prompt Anchor

必须额外输出一段 **canonical_character_description**。

原则：

- 简短
- 视觉明确
- 每次引用尽量保持原句
- 不塞入当前镜头动作和环境

例如：

```text
22-year-old East Asian man, slim build, short straight black hair,
narrow face, dark eyes, charcoal gray hoodie, black cargo pants,
white sneakers
```

## Quality Check

- [ ] 有唯一 character_id
- [ ] Stable / Variable 已区分
- [ ] 外貌描述足够具体
- [ ] 没有互相冲突的特征
- [ ] 有固定服装
- [ ] 有 canonical character description
- [ ] 有 reference pack 规划
- [ ] 可以直接被 storyboard / image generation 使用

## Learning Mode

用户学习时，不直接替用户决定所有细节。

优先要求用户先确定：

1. 发型
2. 主服装
3. 一个最容易识别的标志特征

然后再帮助补全。

## Next

```text
character-bible
→ scene-breakdown / storyboard-generator
→ 后续 character-consistency / image-generator
```
