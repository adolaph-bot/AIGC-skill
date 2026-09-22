---
name: story-writer
version: 1.0.0
module: story
stage: foundation
description: 将一个创意、题材或一句话设定转化为适合 AIGC 制作的结构化短剧故事与剧本。
---

# Story Writer

## 目标

把模糊创意转成 **可继续拆 Scene、Shot、角色和素材的生产型剧本**。

不是写纯文学小说，而是为后续 AIGC 制作提供清晰输入。

## 什么时候使用

适用于：

- 用户只有一个故事点子
- 用户有主题但没有剧情
- 用户有一段散乱文案，需要改成短剧
- 后续需要进入角色设计、分镜、生图或视频制作

## 什么时候不要使用

不要用于：

- 已经有完整定稿剧本，只需要分镜
- 单纯生成一张图
- 单纯设计角色外观
- 单纯写视频 Prompt

这些任务应交给对应 Skill。

## Inputs

必需：

- `premise`：一句话故事/题材/核心想法

可选：

- `target_duration`：目标时长，如 30s / 60s / 3min
- `genre`：喜剧、悬疑、都市、科幻等
- `tone`：轻松、压抑、热血、克制等
- `audience`
- `platform`：抖音、B站、YouTube Shorts 等
- `constraints`：角色数、场景数、预算、画面限制
- `reference_style`：只允许描述特征，不要求模仿在世艺术家个人风格

## 核心规则

1. **故事必须可视化。**  
   尽量用能够被镜头表现的动作、地点、物件和冲突，不依赖大量内心独白。

2. **短剧必须尽早建立冲突。**  
   短视频开头应尽快出现问题、异常、目标或悬念。

3. **控制角色和地点数量。**  
   初学项目默认：
   - 主要角色 1–3 个
   - 主要场景 1–3 个
   - 避免无必要群演和频繁换景

4. **不要直接写生成模型 Prompt。**  
   Story Writer 负责故事，不负责镜头级生成提示。

5. **保留可修改性。**  
   角色名、地点、时长等应结构化输出。

## Steps

### Step 1 — 明确一句话故事

整理成：

```text
主角 + 目标 + 阻碍 + 特殊设定/代价
```

例如：

```text
一名便利店夜班青年想熬过普通的一晚，
却在门口发现一个失去记忆、会说话的机器人。
```

### Step 2 — 建立故事骨架

默认使用：

```text
Setup
→ Inciting Incident
→ Escalation
→ Turning Point / Climax
→ Resolution
```

对于 30–60 秒短剧，可以压缩为：

```text
Hook
→ Problem
→ Escalation
→ Payoff
```

### Step 3 — 建立角色需求

这里只定义剧情功能，不展开完整视觉设计。

每个主要角色至少写：

- name
- role
- goal
- conflict
- personality_keywords
- story_function

### Step 4 — 写 Production Script

每段剧情使用可拍摄格式：

```text
SCENE
地点 / 时间
角色
可视动作
对白
剧情目的
```

避免长段文学描写。

### Step 5 — 检查 AIGC 可制作性

检查：

- 是否需要太多角色？
- 是否频繁换装？
- 是否有大量难以稳定生成的复杂群体动作？
- 是否一个镜头包含多个连续变形？
- 是否场景数量过多？
- 是否需要无法通过画面表达的大量心理描写？

必要时简化。

## Output Schema

```yaml
title:
logline:
target_duration:
genre:
tone:

characters:
  - name:
    role:
    goal:
    conflict:
    personality_keywords:
    story_function:

story_beats:
  - beat_id:
    type:
    summary:

script:
  - scene_id:
    location:
    time:
    characters:
    action:
    dialogue:
    dramatic_purpose:

production_notes:
  estimated_scenes:
  estimated_characters:
  difficult_elements:
  simplification_suggestions:
```

## Quality Check

合格标准：

- [ ] 一句话能说明故事核心
- [ ] 主角目标明确
- [ ] 有冲突或变化
- [ ] 开头不拖沓
- [ ] 每个 Scene 都有剧情功能
- [ ] 画面可表达
- [ ] 角色和地点数量适合当前项目
- [ ] 可以直接交给 `scene-breakdown`

## Learning Mode

如果用户处于学习阶段：

先让用户自己回答三个问题：

1. 主角是谁？
2. 他/她想得到什么？
3. 什么东西阻止他/她？

只在用户完成后继续扩写。

## Next

通常下一步：

```text
story-writer
→ character-bible
→ scene-breakdown
```
