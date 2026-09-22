# AIGC-skill

> 面向 AI 漫剧 / AI 短视频 / 生成式媒体创作的系统化学习与生产仓库。  
> 本仓库不是“工具收藏夹”，而是一套可被人和 AI 共同读取、调用、扩展的 **AIGC 能力系统**。

## 一句话目标

把完整 AIGC 流程跑通：

```text
创意/故事
→ 剧本
→ 角色设定
→ 场景设定
→ 分镜
→ 关键帧
→ 角色一致性
→ 图像生成
→ 图生视频 / 文生视频
→ 镜头控制
→ 配音
→ 字幕
→ 音乐 / 音效
→ 剪辑
→ 成片
→ 自动化
```

## 本仓库的核心原则

1. **能力优先，工具其次**  
   先定义要完成的能力，再选择当前合适的模型或软件。不要把知识体系绑定在某个具体工具上。

2. **项目驱动，而不是教程驱动**  
   学到的每个模块必须能落到真实产出：角色卡、分镜表、镜头、配音或成片。

3. **先跑通，再优化，再自动化**  
   第一阶段允许手工完成；第二阶段提高一致性和质量；第三阶段再用 ComfyUI / Python / Agent 自动化。

4. **Skill 化**  
   把可重复任务拆成独立 Skill，每个 Skill 应明确：输入、步骤、输出、依赖、检查标准和禁止事项。

5. **保留替换能力**  
   图像、视频、TTS、剪辑模型都可能变化。上层 Skill 不应依赖单一厂商或单一模型。

## 能力地图

```text
AIGC
├── 01 Story
│   ├── idea-generator
│   ├── story-writer
│   └── script-writer
├── 02 Character
│   ├── character-designer
│   ├── character-bible
│   └── character-consistency
├── 03 Storyboard
│   ├── scene-breakdown
│   ├── storyboard-generator
│   └── shot-planner
├── 04 Visual
│   ├── prompt-builder
│   ├── image-generator
│   ├── image-editor
│   └── consistency-controller
├── 05 Director
│   ├── cinema-director
│   ├── camera-movement
│   ├── lighting-director
│   └── composition
├── 06 Video
│   ├── text-to-video
│   ├── image-to-video
│   ├── reference-video
│   └── video-extension
├── 07 Audio
│   ├── tts
│   ├── voice-clone
│   ├── bgm
│   └── sound-effects
├── 08 Editing
│   ├── subtitle
│   ├── video-edit
│   ├── audio-mix
│   └── export
└── 09 Pipeline
    ├── project-manager
    ├── asset-manager
    ├── quality-check
    └── final-render
```

## 学习里程碑

### Milestone 1 — 跑通 30 秒 AI 漫剧
剧本 → 人物 → 分镜 → 生图 → 图生视频 → 配音 → 剪映 → 成片。

### Milestone 2 — 稳定完成 1–3 分钟作品
加入 Character Bible、角色一致性、镜头语言、统一声音和质量检查。

### Milestone 3 — ComfyUI 工作流化
把生图、修图、一致性、控制和视频生成逐渐节点化。

### Milestone 4 — Python / Agent 自动化
目标是实现：输入一个故事后，可自动创建项目、生成结构化剧本和分镜、组织资产，并逐步串起生成、配音、字幕、剪辑与导出。

## AI 进入本仓库后应先读什么

未来任何 AI / Agent / Codex 在执行任务前，按顺序读取：

1. `README.md` — 理解总目标与系统边界
2. `docs/AI_ROUTING.md` — 判断该调用哪些模块、哪些项目只能参考
3. `docs/FUSION_PLAN.md` — 理解外部项目如何被吸收进本体系

若未来新增 `skills/`，再读取对应模块下的 `SKILL.md`。

## 当前参考项目

这些项目用于“吸收方法”，不等于全部成为运行依赖：

- SamurAIGPT/Generative-Media-Skills
- Comfy-Org/ComfyUI
- comfyanonymous/ComfyUI_examples
- ZHO-ZHO-ZHO/ComfyUI-Workflows-ZHO
- RVC-Boss/GPT-SoVITS
- harry0703/MoneyPrinterTurbo
- linyqh/NarratoAI
- remotion-dev/remotion
- Zulko/moviepy

详细取舍见 `docs/FUSION_PLAN.md` 与 `docs/AI_ROUTING.md`。
