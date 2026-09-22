# AI 调用与工具选择规则（AI_ROUTING）

> 本文件优先供未来 AI / Agent / Codex 读取。  
> 目标：让 AI 清楚“什么时候应该使用什么、什么时候不应该使用什么”。

## 0. 总规则

在选择任何工具前：

```text
先判断任务属于哪个能力模块
→ 再判断用户当前所处学习阶段
→ 再选择最低复杂度、能完成目标的工具
→ 必要时才升级到更复杂方案
```

### 默认原则

- 优先完成作品，不优先追求技术炫技。
- 优先低复杂度方案，不无理由上本地重型工作流。
- 优先保留用户学习过程，不直接黑盒代做全部步骤。
- 同一任务不要同时推荐 5 个同类工具。
- 所有模型/软件都视为“实现”，不是“能力本身”。

---

## 1. Story / Script

### 应使用

- LLM
- story-writer
- script-writer
- scene-breakdown

### 输出必须尽量结构化

至少包含：
- Character
- Scene
- Shot
- Action
- Dialogue

### 不应使用

- ComfyUI
- 视频模型
- TTS

除非已经进入对应后续阶段。

---

## 2. Character

### 应使用

- character-bible
- character-designer
- reference image
- 角色多角度 / 表情组

### 关键规则

必须先建立稳定角色，再批量生成连续场景。

不要：

```text
Scene 1 随机生一个人
Scene 2 再重新随机生一个人
Scene 3 再靠 Prompt 猜同一个人
```

---

## 3. Storyboard

### 应使用

先把剧本拆成：

```text
Story
→ Scene
→ Shot
```

每个 Shot 推荐字段：

- shot_id
- scene_id
- duration
- framing
- subject
- action
- environment
- camera
- lighting
- dialogue
- image_prompt
- video_prompt

### 不应使用

不要直接把一整段剧本丢给视频模型期待一次完成。

---

## 4. Visual / Image

### 初学阶段

优先使用最容易取得结果的生图工具。

目标：
- Prompt 基础
- 参考图
- 角色一致性
- 构图
- 修改

### 进入 ComfyUI 的条件

满足以下之一再优先使用 ComfyUI：

- 需要更强控制
- 需要重复工作流
- 需要 ControlNet / LoRA / Inpaint
- 需要本地化
- 需要批处理
- 需要工作流自动化

### 不应使用 ComfyUI 的情况

- 用户只是第一次做 30 秒作品
- 任务用简单工具 5 分钟即可完成
- 用户还不知道 T2I / I2I / Inpaint 的区别
- 为了“专业感”而无意义增加节点

---

## 5. Director

当任务涉及“镜头怎么拍”时，使用 cinema-director 思路。

### Prompt 结构

```text
Shot Type
+ Subject / Action
+ Environment
+ Lighting
+ Camera Movement
+ Lens Effect
```

### 不要

仅输出：
- cinematic
- masterpiece
- cool camera

这类空泛词不能替代镜头设计。

---

## 6. Video

### 选择顺序

有角色关键帧 / 场景图：
→ 优先 I2V

只需要探索画面：
→ 可以 T2V

需要动作或主体一致：
→ Reference Video / Reference Image

需要连续镜头：
→ Video Extension / shot-by-shot

### 不要

- 一条 Prompt 同时要求大量互相冲突的运动
- 在单镜头中频繁变身、换场、换装
- 用一个 10 秒生成任务承载完整剧情

优先多 Shot，再剪辑。

---

## 7. Audio

### 普通作品

优先普通 TTS，先完成。

### 需要固定角色声音

使用：
- Voice Profile
- reference audio
- voice clone / GPT-SoVITS 或替代引擎

### 不要

因为“可以克隆声音”就默认克隆现实人物声音。应使用获得授权或用户自己的合法参考音频。

---

## 8. Editing

### 当前学习初期

优先：
- 剪映 / 常规剪辑工具

学习：
- 轨道
- 字幕
- BGM
- SFX
- 节奏
- 转场
- 导出

### 什么时候使用 MoviePy

当出现：
- 重复拼接
- 批量字幕
- 批量导出
- 固定模板
- Python 自动化需求

### 什么时候使用 Remotion

当出现：
- React/代码驱动视频
- 动画模板
- 数据驱动视频
- 大规模批量渲染
- Agent 自动生成成片

初学阶段不要把 Remotion 当主线。

---

## 9. Pipeline / Automation

### 可参考

- MoneyPrinterTurbo
- NarratoAI

### 参考的重点

学习它们如何：

- 分阶段执行
- 保存中间结果
- 把模块串起来
- 允许用户修改中间产物
- 失败重试
- 调用不同模型

### 不应该

直接把“一键出片”当最终学习目标。

我们的目标是：

> 先理解每个环节，再逐步自动化。

---

## 10. 外部 GitHub 项目使用等级

### A — 核心方法参考

- SamurAIGPT/Generative-Media-Skills
- Comfy-Org/ComfyUI
- comfyanonymous/ComfyUI_examples

可以经常读取其架构与流程。

### B — 专项能力参考

- RVC-Boss/GPT-SoVITS
- ZHO-ZHO-ZHO/ComfyUI-Workflows-ZHO

按对应模块调用。

### C — Pipeline 架构参考

- harry0703/MoneyPrinterTurbo
- linyqh/NarratoAI

主要研究串联方式，不默认作为底层依赖。

### D — 后期程序化工具

- Zulko/moviepy
- remotion-dev/remotion

在 Python / 自动化阶段再重点使用。

---

## 11. 模型选择规则

AI 不应因为仓库文档出现某个模型名，就认为必须使用它。

选择模型时按：

```text
任务能力需求
> 可控性
> 一致性
> 用户当前可访问性
> 成本
> 速度
> 当前阶段学习价值
```

再做决定。

模型名称只应出现在“适配层”，不应成为知识体系顶层。

---

## 12. AI 执行任务前检查

未来任何 AI 在本仓库执行 AIGC 任务前，应快速回答：

```text
1. 用户现在要完成什么作品？
2. 当前属于 Story / Character / Storyboard / Visual / Director / Video / Audio / Editing / Pipeline 哪一层？
3. 当前阶段是否真的需要复杂工具？
4. 有没有已有 Skill 可以复用？
5. 是否需要先产出中间结果让用户确认？
6. 是否必须保证角色/声音/场景一致性？
7. 最终要输出什么可验证成果？
```

如果无法回答，不应直接进入复杂生成。

---

## 13. 当前默认路线

用户当前总目标：

> 建立系统化 AIGC 能力，并跑通完整 AI 漫剧 / AI 短视频制作流程。

默认学习路径：

```text
剧本
→ Character Bible
→ Scene / Shot
→ Storyboard
→ 生图
→ 角色一致性
→ I2V
→ 配音
→ 字幕
→ 剪辑
→ 第一条成片
→ ComfyUI
→ Python
→ 自动化
```

除非用户明确修改目标，否则不要随意把学习路线改成纯理论、纯模型研究或论文路线。
