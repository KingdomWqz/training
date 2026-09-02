# 培训资料库（Training）

本仓库收集面向 AI 编程工具、智能体平台与内容创作的教学大纲、演示课件和实践资料，用于课程培训、技术分享和自学参考。

## 目录结构

- [`outline/`](./outline)：Markdown 教学大纲。多课时系列课程以主题子目录组织，并在目录的 `README.md` 提供总纲与索引。
- [`ppt/`](./ppt)：HTML 演示课件与版式资料，课件通常位于 `ppt/<主题>/ppt/index.html`。
- [`demo/`](./demo)：课堂演示用 Prompt 与示例素材。

## 课程总览

| 课程 | 主题 | 时长 | 大纲 |
|------|------|------|------|
| **AI Native** | 当 AI 成为团队的原住民 | 20 分钟 | [`outline/ainative/ai-native.md`](./outline/ainative/ai-native.md) · [`ppt/ai-native/ppt/index.html`](./ppt/ai-native/ppt/index.html) |
| **OPC：个人开发者与 AI 工具生态** | 工具链、配置管理与智能体协作专题（3 课时） | 60 分钟 × 3 | [`outline/opc/README.md`](./outline/opc/README.md) |
| **AI 生图实战** | 生图专题：文生图·图生图·修图 + 电商实战（6 课时） | 30 分钟 × 6 | [`outline/image/README.md`](./outline/image/README.md) |
| **电商带货短视频 AI 生成** | 工具、脚本、生成、剪辑与运营实战（6 课时） | 30 分钟 × 6 | [`outline/video/README.md`](./outline/video/README.md) |
| **OpenAI Codex 从入门到精通** | Codex 五形态全栈开发与个人知识库教学（25 课时） | 30 分钟 × 25 | [`outline/README.md`](./outline/README.md) |

### 课程简介

- **[OPC：个人开发者与 AI 工具生态专题](./outline/opc/README.md)**：将独立开发工具全景、CCSwitch 配置管理和 LobeHub 智能体平台整合为一条 OPC 工作流，覆盖工具选型、配置复用与智能体协作。
- **[AI Native 教学大纲](./outline/ainative/ai-native.md)**：用 20 分钟建立 AI Native 的核心认知，理解模型、上下文、Agent 与 Harness 四层技术栈，以及业务、技术、组织协同的落地方法；配套提供 [HTML PPT](./ppt/ai-native/ppt/index.html)。
- **[AI 生图实战：从入门到电商落地](./outline/image/README.md)**：面向电商运营与中小卖家的生图专题课程，共 6 课时（每课时 30 分钟）。基础篇系统讲授文生图（模型选型与提示词公式）、图生图（参考图锁商品）、修图（局部重绘/消除/扩图）三项核心能力；实战篇落到电商三大高频场景——封面图（白底主图/促销海报）、生活场景图（垫图换场景种草）、模特换装（平铺图→虚拟模特上身），全程强调「商品不跑样」的一致性与肖像/版权合规。
- **[电商带货短视频 AI 生成实战课程](./outline/video/README.md)**：面向电商运营与带货主播，共 6 课时（每课时 30 分钟）。基础篇覆盖工具选型、五段式脚本与分镜、图生视频；实战篇完成数字人口播、剪映合成、发布优化与内容矩阵，最终产出可发布的带货短视频。
- **[Codex 全栈开发课程](./outline/README.md)**：系统课程共 25 个课时（每课时 30 分钟）。内容覆盖五种形态认知与安装、核心工作循环、CLI 深度使用与安全机制、AGENTS.md 项目规则、桌面 App 多 Agent 协作、云端异步开发、Skills/MCP/Automations 与 `/goal` 扩展体系、结合 Obsidian 搭建 AI 维护的个人知识库（方法论、项目化接入、自动化流水线三课），并以「静态网站综合实战」+「内容创作实战」（公众号/小红书/生图/生视频）综合收尾，每个课时均含时间分配、课堂演示、动手任务与课后作业大纲。

### 配套资料

- [Skills 专题](./outline/skill/)：包含提示词规范、网页访问、UI/UX、PPT 制作与浏览器自动化等实践指南。
- [课堂演示 Prompt 与素材](./demo/README.md)：用于课程演示的可复用 Prompt 和示例入口。

## 使用方式

1. 浏览 `outline/` 目录下的对应大纲文件；多课时系列课程（如 Codex、AI 生图实战和短视频课程）以子目录为单位，从其 `README.md` 总纲进入。
2. 按大纲中的「教学准备清单」「实践任务」「课后作业」等模块组织课程或自学。
3. 需要授课演示时，打开 `ppt/` 下对应主题的 HTML 课件；课程资源、官方文档与扩展阅读均已在大纲末尾列出。

## 贡献指南

欢迎补充新的课程大纲或优化现有内容：

- 新的课程大纲请在 `outline/` 目录下按主题组织；多课时系列课程使用「子目录 + README.md 总纲 + 各课时大纲文件」结构。
- 新增演示课件请在 `ppt/` 下建立主题目录，并提供可直接打开的 HTML 入口（通常为 `ppt/<主题>/ppt/index.html`）。
- 建议包含：课程概述、课程目标、时间分配、动手实践、资源与考核等结构。
- 提交前请保持术语与格式统一，并在文件末尾标注更新日期。

---

*最后更新：2026-09-02*
