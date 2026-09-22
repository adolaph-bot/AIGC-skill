# Skills Index

本目录存放可被人、AI、Codex、Agent 直接读取和执行的 AIGC Skills。

## 使用原则

每个 Skill 都必须明确：

- 什么时候使用
- 什么时候不要使用
- 输入
- 执行步骤
- 输出
- 质量检查
- 与下一 Skill 的衔接

AI 不应跳过必要的中间产物直接进入后续生成。

## 第一批基础 Skills

```text
story-writer
    ↓
character-bible
    ↓
scene-breakdown
    ↓
storyboard-generator
    ↓
shot-planner
```

### 01 Story

- `01-story/story-writer/SKILL.md`  
  把创意或题材整理成可制作的故事与短剧剧本。

### 02 Character

- `02-character/character-bible/SKILL.md`  
  为核心人物建立稳定、可重复引用的角色圣经。

### 03 Storyboard

- `03-storyboard/scene-breakdown/SKILL.md`  
  把剧本拆成 Scene。

- `03-storyboard/storyboard-generator/SKILL.md`  
  把 Scene 转换为可视化分镜。

- `03-storyboard/shot-planner/SKILL.md`  
  为单个 Shot 补齐景别、机位、运动、时长、声音和生成提示。

## 两种工作模式

### Learning Mode

用户正在学习时：

1. 不一次替用户完成全部工作。
2. 先解释当前步骤为什么存在。
3. 给一个小任务让用户自己完成。
4. 检查后再进入下一阶段。
5. 每一阶段都留下可复用成果。

### Production Mode

用户明确要求直接制作时：

1. 可以连续执行多个 Skill。
2. 仍必须保留结构化中间结果。
3. 对角色定稿、重大视觉方向等不可逆节点，优先让用户确认。
4. 不得为了速度跳过角色一致性、分镜或质量检查。

## 当前边界

第一批 Skills 只解决：

> 创意 → 剧本 → 角色 → 场景 → 分镜 → 镜头计划

暂时不负责真正生图、生视频、配音和剪辑。后续模块会在这一基础上继续建立。
