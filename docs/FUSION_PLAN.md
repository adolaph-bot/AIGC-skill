# 融合计划（FUSION_PLAN）

## 目标

本文件回答一个问题：

> 外部优秀 AIGC 项目里，哪些思想值得吸收进本仓库，哪些只能作为参考，哪些不应该成为核心依赖？

本仓库采用“**能力层 → Skill 层 → 工具适配层 → 自动化层**”的融合方式，而不是复制整个外部项目。

---

## 一、融合总架构

```text
用户目标 / 创作任务
        ↓
能力层
故事 / 角色 / 分镜 / 视觉 / 导演 / 视频 / 音频 / 剪辑
        ↓
Skill 层
结构化输入 → 执行步骤 → 输出格式 → 检查标准
        ↓
工具适配层
ComfyUI / 商业模型 / GPT-SoVITS / 剪映 / MoviePy / Remotion ...
        ↓
自动化层
Python / CLI / API / Agent / Pipeline
```

### 为什么这样融合

- 模型会更新，能力不会频繁失效。
- 工具可以替换，Skill 逻辑应尽量稳定。
- 初学阶段可以人工执行，熟练后再自动化。
- 后续 AI 调用时，可以先判断任务属于哪个能力模块，再选择当前最佳实现。

---

## 二、外部项目的吸收策略

### 1. SamurAIGPT/Generative-Media-Skills

**定位：最重要的 Skill 结构参考。**

重点吸收：

- 每个任务独立为 `SKILL.md`
- 明确 Inputs / Steps / Outputs / Notes
- Storyboard Generator 的故事节拍拆分
- Character Story Video 的“先建立角色，再生成连续场景”
- Cinema Director 的摄影语言结构
- 多阶段 Workflow Recipe 的设计方式

重点转化：

```text
外部 Skill
→ 去掉特定 API 强绑定
→ 提炼通用方法
→ 改造成自己的 Skill
→ 接入可替换工具
```

**不要直接照搬：**

- 不把 MuAPI 当成本仓库唯一执行层
- 不照搬特定模型 ID
- 不让 API 供应商决定学习路线

---

### 2. Comfy-Org/ComfyUI

**定位：中后期的视觉/视频节点化生产引擎。**

重点吸收：

- 节点化思想
- 工作流可视化
- 模型、条件控制、参考图和后处理的组合
- 可保存、复用、共享工作流

用于：

- 生图
- 图生图
- 局部重绘
- ControlNet / 姿态控制
- LoRA
- 放大修复
- 角色一致性
- 图生视频 / 文生视频
- 音频相关工作流

**暂时不要：**

- 初学期同时安装大量自定义节点
- 为了“看起来高级”而构建复杂工作流
- 在没跑通手工流程前先做自动化

---

### 3. comfyanonymous/ComfyUI_examples

**定位：ComfyUI 学习标准样例库。**

重点吸收：

- Txt2Img
- Img2Img
- Inpainting
- LoRA
- ControlNet
- Upscale
- Flux / Qwen Image 等图像模型
- Wan / Hunyuan / LTX 等视频工作流

规则：

> 学一个例子 → 理解每个节点为什么存在 → 自己复现 → 再改造成项目需要的工作流。

不建议一次性学习全部。

---

### 4. ZHO-ZHO-ZHO/ComfyUI-Workflows-ZHO

**定位：中文工作流拆解参考。**

适合：

- 看别人怎样组织 ComfyUI 图
- 对照中文说明理解工作流
- 寻找角色一致性、图像控制、视频等案例

**只作参考，不作为标准答案。**

原因：第三方工作流可能依赖旧节点、旧模型或大量额外插件。

---

### 5. RVC-Boss/GPT-SoVITS

**定位：角色声音系统的重要参考。**

重点吸收：

- Zero-shot TTS
- Few-shot TTS
- 参考音频
- 音色克隆
- 多语言
- ASR / 数据切分

本仓库应该抽象成：

```text
VOICE_ID
角色
年龄感
音色
语速
情绪
参考音频
TTS 引擎
```

**不强制绑定 GPT-SoVITS。**

未来可以切换其他 TTS/Voice Clone 引擎。

---

### 6. harry0703/MoneyPrinterTurbo

**定位：完整自动视频 Pipeline 架构参考。**

重点吸收：

```text
主题
→ AI 脚本
→ 素材
→ 配音
→ 字幕
→ BGM
→ 剪辑
→ 成片
```

重点研究：

- 每一阶段如何传递数据
- 如何允许用户覆盖自动生成结果
- WebUI / API / CLI / Agent 多入口
- 批量任务和历史记录

**不要直接把“一键生成”当学习方式。**

目标是理解流水线，而不是依赖黑盒。

---

### 7. linyqh/NarratoAI

**定位：中文短剧、解说、视频理解与剪辑流程参考。**

重点吸收：

- 短剧处理
- 视频理解
- 自动转录
- TTS
- 字幕
- AI 配乐
- 剪辑
- 剪映导出

特别适合研究：

> “已有视频素材如何被 AI 理解、再加工、再剪辑。”

但与“从零生成 AI 漫剧”要分开看，不要混成一个 Skill。

---

### 8. Zulko/moviepy

**定位：Python 视频自动化入门层。**

适合在 Python 基础建立后学习：

- cut
- concatenate
- text overlay
- audio mix
- image/video composite
- export

推荐用途：

> 把人工剪辑中重复、规则明确的步骤程序化。

---

### 9. remotion-dev/remotion

**定位：更高级的程序化视频与 Agent 视频层。**

适合后期：

- React 驱动视频
- 模板化动画
- 数据驱动视频
- 批量渲染
- Agent 生成视频

不是当前初学阶段主线。

---

## 三、我们的融合版本

外部项目不按“项目名称”进入主知识树，而按能力拆解。

### Story
来源：Generative-Media-Skills + LLM 实践

吸收：
- 创意生成
- 故事结构
- 剧本格式
- 场景拆分

### Character
来源：Character Story Video + 图像一致性工作流

吸收：
- Character Bible
- 基准角色图
- 多角度
- 表情组
- 服装与物件固定
- reference image

### Storyboard
来源：Storyboard Generator + 影视分镜方法

吸收：
- story beat
- scene
- shot
- 景别
- 镜头运动
- 时长
- 图像 Prompt
- 视频 Prompt

### Director
来源：Cinema Director

标准 Prompt 结构：

```text
Shot Type
+ Subject / Action
+ Environment
+ Lighting
+ Camera Movement
+ Lens / Optical Effect
```

### Visual
来源：ComfyUI + 官方 examples + 商业模型

重点：
- T2I
- I2I
- Inpaint
- Control
- Consistency
- Upscale

### Video
来源：ComfyUI 视频工作流 + 各视频模型

重点：
- T2V
- I2V
- Reference Video
- Video Extension
- 人物运动
- 镜头运动
- 环境运动

### Audio
来源：GPT-SoVITS + 其他 TTS

重点：
- 角色声音身份
- 配音
- 情绪
- BGM
- SFX

### Editing
来源：剪映 → MoviePy → Remotion

顺序：
1. 先人工
2. 再半自动
3. 再程序化

### Pipeline
来源：MoneyPrinterTurbo + NarratoAI + Agent Skill 思路

最终目标：

```text
输入故事
→ 建立项目
→ 生成结构化剧本
→ 生成角色 Bible
→ 拆分 Scene / Shot
→ 生成 Prompt
→ 生成/组织资产
→ 视频
→ 配音
→ 字幕
→ 剪辑
→ QC
→ Final Render
```

---

## 四、学习路线与融合节奏

### Phase 1：先跑通人工流程

只要求：

```text
30 秒 AI 漫剧成片
```

不要求：
- ComfyUI 高级节点
- 自动化
- Python 视频脚本
- 本地部署所有模型

### Phase 2：提高可控性

加入：
- Character Bible
- 人物一致性
- Storyboard
- 镜头语言
- 声音一致性
- 项目资产管理

### Phase 3：工作流化

开始：
- ComfyUI
- 可复用 Workflow
- 固定输出格式
- Skill 化

### Phase 4：自动化

开始：
- Python
- MoviePy
- API
- CLI
- Agent
- Pipeline orchestration

### Phase 5：产品化

目标：
- 一个输入入口
- 项目自动创建
- 每一步可人工介入
- 支持模型替换
- 有失败重试与质量检查
- 输出完整项目与成片

---

## 五、绝对不要融合的错误模式

不要把下面这些做法带进本仓库：

- “每发现一个新工具就建一个一级目录”
- “把具体模型名称当核心知识结构”
- “未理解流程就一键自动化”
- “为了追新模型不断重做系统”
- “堆大量 Prompt，却没有输入/输出规范”
- “只有教程收藏，没有作品”
- “复制别人工作流却不知道节点作用”
- “把 API 平台绑定进 Skill 核心逻辑”
- “同时学习太多相似工具”

---

## 六、未来新增项目时的判断标准

任何新 GitHub 项目进入本体系前，AI 必须回答：

1. 它解决的是哪个能力模块？
2. 它带来了新能力，还是只是另一个同类工具？
3. 它提供的是方法、工作流、模型、UI，还是 API？
4. 有什么值得抽象进 Skill？
5. 哪些部分是供应商/模型特有，不应进入核心？
6. 能否替换现有实现？
7. 是否值得当前阶段学习？

只有能明显增强系统能力的内容，才应该融合。
