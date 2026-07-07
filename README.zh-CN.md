<img src=".github/assets/banner.svg" alt="borrowed-brain-pro" width="100%">

[English](README.md) | [简体中文](README.zh-CN.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/DOTfei/borrowed-brain-pro?style=social)](https://github.com/DOTfei/borrowed-brain-pro/stargazers)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-6b4fbb)](SKILL.md)

**一份 AI 指令文件，把任何公众人物的思考方式蒸馏成一套可复用的框架——然后把它当作一个额外的视角，套用到你正在面对的真实决策上。**

支持 Claude（原生 Skill）、ChatGPT、Open WebUI、Hermes 等本地模型，或任何可以接受 system prompt 的 AI。

不是聊天机器人角色扮演，不是语录生成器。而是一份基于真实公开材料——访谈、决策记录、失败、批评——构建出的结构化「思维档案」，你可以拿它去照一照自己的问题：*这套框架会让我看到什么我原本忽略的东西？*

---

## Demo 演示

<video src=".github/assets/demo.mp4" controls width="100%"></video>

> *描述一个真实决策 → skill 读取档案索引 → 推荐最相关的视角 → 展示两个框架的冲突点*

---

## 🚀 刚装好这个 skill？从这里开始

开一个新对话，直接打以下任意一句——不需要特殊语法，不需要斜杠命令：

```
我有哪些人的档案可以用？
```
```
用 Warren Buffett 的档案，看看我这个投资机会值不值得做——[描述你的情况]
```
```
帮我建一份 Naval Ravikant 的思维档案
```
```
borrowed-brain-pro 是做什么的？
```

最后这句也完全没问题——如果你不确定该问什么，直接问这个 skill 本身，它会解释两种模式并直接给你一句能用的起手式。

---

## 它做什么

两种模式，一个 skill：

**Distill（蒸馏）模式** —— 给它一个名字，它会研究这个人并生成 `profiles/<name>.md`：核心立场、反复出现的原则（附带每条在什么条件下会失效）、默认推理顺序、取舍倾向、一个已记录的失败案例，以及一份说明材料扎实程度的可信度说明。

**Apply（应用）模式** —— 把一份已有档案套到你正面对的真实问题上，用这个视角推理你的处境——明确标注这只是"一个有局限的视角"，不是判决。

```mermaid
flowchart LR
    A("👤 人名\n例如「巴菲特」") -->|Distill 蒸馏模式| B

    subgraph B["研究"]
        direction TB
        b1["访谈 · 决策记录\n失败 · 批评"]
    end

    B --> C("📄 profiles/warren-buffett.md\n原则 · 失效条件\n来源 · 可信度说明")

    C -->|Apply 应用模式| D

    subgraph D["你的真实决策"]
        direction TB
        d1["用自己的话\n描述你的处境"]
    end

    D --> E("🔍 一个额外的视角\n不是判决——明确标注\n这个框架覆盖不到什么")
```

**档案路由** —— 如果你描述一个决策但没点名用谁，skill 会读 [`profiles/INDEX.md`](profiles/INDEX.md)，推荐 1–2 个最相关的档案，等你确认后才开始 Apply。

---

## 已内置 8 份档案——装完即用

这个 repo 附带 8 份真实运行 Distill 模式生成的档案，不是虚构的样例：

| 人物 | 领域 | 最适合的问题类型 |
|------|------|----------------|
| [Warren Buffett（巴菲特）](profiles/warren-buffett.md) | 投资 | 要不要押注这个机会？长期持有 vs. 卖出。估值纪律。 |
| [Steve Jobs（乔布斯）](profiles/steve-jobs.md) | 产品/创业 | 砍哪个功能？发布时机？对需求说不。 |
| [Chris Voss](profiles/chris-voss.md) | 谈判 | 合同谈判。打破僵局。应对强硬对手。 |
| [Richard Feynman（费曼）](profiles/richard-feynman.md) | 研究/推理 | 验证假设。找自我欺骗的盲点。审查自己的逻辑。 |
| [Cal Newport](profiles/cal-newport.md) | 个人效率 | 时间分配。保护深度工作。结构性修复 vs. 靠意志力。 |
| [Reed Hastings](profiles/reed-hastings.md) | 领导力/文化 | 在团队里建立坦诚文化。处理重大战略转向。 |
| [Travis Kalanick](profiles/travis-kalanick.md) | 激进增长 | 强攻充满阻力的市场还是等待？速度 vs. 合规。 |
| [Julia Evans](profiles/julia-evans.md) | 技术写作 | 把难懂的东西解释清楚。为过去的自己写作。 |

---

## 示例

以下是从 [`profiles/reed-hastings.md`](profiles/reed-hastings.md) 里摘出的真实片段：

> **原则**：主动征求异议，而不是把沉默当成同意（"farming for dissent"）。
> **体现之处**：直接源自 Qwikster 的失败案例（2011 年）——Hastings 发现多位副总裁私下都有疑虑却没说出来，其中一位告诉他，他一旦确信某件事就会"太 intense"，让人觉得反对也没用。
> **可能失效之处**：这条原则是事后补救——它是在一次导致 80 万订阅用户流失、股价暴跌 77% 的失败之后才建立起来的，不是之前。

同时载入两份档案，Apply 模式呈现真实分歧：

```
你：我们是一家快速增长的创业公司，面临压力要强攻一个监管环境
非常敌对的城市，律师说风险很高。该强推还是该等？

Claude：同时载入两个视角，呈现真实分歧：

- Kalanick 的框架 → 强推。他的逻辑明确把监管敌意当作正面信号
  ——挺过越难的仗，护城河就越深。
- Hastings 的框架 → 等待。他的原则是让良好的判断（包括律师的）
  发挥作用，而不是用个人确信压过它——他自己的失败案例
  （Qwikster）恰恰就是他的确信压过了正在提出担忧的人。

这两者之所以冲突，是因为它们对同一个信号——"来自权威的阻力"
——给出了相反方向的权重。这种张力本身就是有用的信息。
```

---

## 安装

> **简短版：克隆整个 repo（不只是 `SKILL.md`），这样 8 份内置档案也会跟着来。**

### Claude Code（命令行）——推荐

```bash
git clone https://github.com/DOTfei/borrowed-brain-pro.git ~/.claude/skills/borrowed-brain-pro
```

完成。重启 Claude Code 会话，skill 和全部 8 份档案即刻可用。如果只想在某个特定项目里使用，把路径换成该项目下的 `.claude/skills/borrowed-brain-pro/`。

之后更新：
```bash
cd ~/.claude/skills/borrowed-brain-pro && git pull
```

### Claude.ai（网页版）/ ChatGPT / 其他支持 system prompt 的 AI

使用**一键包**——把 `SKILL.md` 和全部 9 份档案合并在一个文件里。粘贴一次进 system prompt，所有档案立即可用，不需要单独上传。

1. 下载 [`claude-ai-bundle.md`](https://github.com/DOTfei/borrowed-brain-pro/raw/main/claude-ai-bundle.md)
2. 开一个新对话，把全文粘贴进 system prompt 字段
3. 直接开始——9 份档案已全部加载

**Claude.ai 通过 Skills 上传（仅 SKILL.md，不含内置档案）：**
1. 下载 [`SKILL.md`](https://github.com/DOTfei/borrowed-brain-pro/raw/main/SKILL.md)
2. 打开 **Settings → Capabilities → Skills**，上传该文件
3. 如需使用某份档案，把对应的 `profiles/<name>.md` 内容粘贴进对话开头

### Open WebUI / LM Studio / Ollama（本地模型）

把 `SKILL.md` 粘贴进 system prompt 字段。研究质量取决于你使用的模型是否有联网搜索权限——如果没有，模型会依赖训练知识，内容可能没有带实时搜索的模型那么完整或最新。

---

## 护栏（内置，不可选）

- 不编造引用；直接引用限 15 词以内、每个来源最多引一句，其余全部转述
- 档案里的每一条声称都必须能追溯到一个真实找到的来源
- 措辞统一是"根据公开材料，其做法似乎是……"——不会写成"其相信……"这种既定事实的口吻
- 拒绝为私人（非公众人物）建档——只处理有实质公开记录的人
- 争议人物：只描述其已记录的推理风格和立场，不推测未公开的私人动机

## 为什么做这个

大多数"像 X 一样思考"的提示词产出的都是千篇一律的励志海报式空话——每份档案读起来都一样，因为它们只用了这个人最光鲜的公开形象来构建。

`borrowed-brain-pro` 刻意去挖更混乱的材料——已记录的失败、批评、本人说法和外界说法对不上的地方——因为真正的决策逻辑正是在这些地方才会显现。它还强制要求档案里的每一条"原则"都要能追溯到一个具体的、有来源的事实，让档案保持扎实，而不是沦为吹捧。

## 这个 skill 不是什么

- 不是用来生成假语录或替人编话的工具
- 不能替代阅读这个人的真实著作——如果你想知道他们真正的观点，去读他们的原文；这个工具是用来找一个你可能忽略的**角度**
- 不是判决生成器——它被设计成每次应用都要以"这个视角覆盖不到什么"收尾，这是刻意的

---

欢迎贡献更好的来源检查清单和示例档案——参见 [CONTRIBUTING.md](CONTRIBUTING.md)（英文）。
