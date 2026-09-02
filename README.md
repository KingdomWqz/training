# 培训资料库（Training）

本仓库收集面向 AI 编程工具与智能体平台的教学大纲与实践资料，用于课程培训、技术分享和自学参考。

## 仓库内容

所有课程大纲存放在 [`ppt/`](./ppt) 与 [`outline/`](./outline) 目录下，以 Markdown 形式维护，便于阅读、修改与版本管理。单课时课程位于 `ppt/`，多课时系列课程以子目录形式位于 `outline/`。

| 课程 | 主题 | 时长 | 大纲 |
|------|------|------|------|
| **CCSwitch** | AI 编程时代的工具配置管理实践 | 60 分钟 | [`outline/ccswitch/CCSwitch.md`](./outline/ccswitch/CCSwitch.md) |
| **LobeHub** | AI 智能体平台快速入门 | 60 分钟 | [`outline/agent/LobeHub.md`](./outline/agent/LobeHub.md) |
| **独立开发者工具全景** | 独立开发者的工具介绍 | 60 分钟 | [`outline/opc/01-IndieDevTools.md`](./outline/opc/01-IndieDevTools.md) |
| **AI 生图实战** | 生图专题：文生图·图生图·修图 + 电商实战（6 课时） | 30 分钟 × 6 | [`outline/image/README.md`](./outline/image/README.md) |
| **电商带货短视频AI生成** | 主流AI视频工具实战 | 60 分钟 | [`outline/video/EcommerceVideo.md`](./outline/video/EcommerceVideo.md) |
| **OpenAI Codex 从入门到精通** | Codex 五形态全栈开发与个人知识库教学（25 课时） | 30 分钟 × 25 | [`outline/README.md`](./outline/README.md) |

### 课程简介

- **[CCSwitch 教学大纲](./outline/ccswitch/CCSwitch.md)**：面向在校学生，介绍 AI 编程工具生态现状与配置管理痛点，讲解 CCSwitch 的供应商管理、MCP 服务器管理、Skills 与 Prompts 管理等核心功能，并融入产品思维与职业发展的启发。
- **[LobeHub 教学大纲](./outline/agent/LobeHub.md)**：面向初次接触 AI 智能体平台的用户，在 60 分钟内掌握 LobeHub 的Agent 创建、技能与知识库、群组协作与记忆，以及社区资源与典型应用场景。
- **[AI 生图实战：从入门到电商落地](./outline/image/README.md)**：面向电商运营与中小卖家的生图专题课程，共 6 课时（每课时 30 分钟）。基础篇系统讲授文生图（模型选型与提示词公式）、图生图（参考图锁商品）、修图（局部重绘/消除/扩图）三项核心能力；实战篇落到电商三大高频场景——封面图（白底主图/促销海报）、生活场景图（垫图换场景种草）、模特换装（平铺图→虚拟模特上身），全程强调「商品不跑样」的一致性与肖像/版权合规。
- **[电商带货短视频AI生成教学大纲](./outline/video/EcommerceVideo.md)**：面向电商运营与带货主播，介绍主流AI视频生成工具（可灵AI、即梦AI、Vidu 等）与数字人工具的选型方法，讲解五段式带货脚本公式与分镜方法，并通过图生视频、数字人口播、剪映合成三个实战任务完成从脚本到成片的全流程。
- **[Codex 全栈开发课程](./outline/README.md)**：系统课程共 25 个课时（每课时 30 分钟）。内容覆盖五种形态认知与安装、核心工作循环、CLI 深度使用与安全机制、AGENTS.md 项目规则、桌面 App 多 Agent 协作、云端异步开发、Skills/MCP/Automations//goal 扩展体系、结合 Obsidian 搭建 AI 维护的个人知识库（方法论、项目化接入、自动化流水线三课），并以「静态网站综合实战」+「内容创作实战」（公众号/小红书/生图/生视频）综合收尾，每个课时均含时间分配、课堂演示、动手任务与课后作业大纲。

## 使用方式

1. 浏览 `ppt/` 与 `outline/` 目录下的对应大纲文件；多课时系列课程（如 Codex、AI 生图实战）以子目录为单位，从其 `README.md` 总纲进入。
2. 按大纲中的「教学准备清单」「实践任务」「课后作业」等模块组织课程或自学。
3. 课程资源、官方文档与扩展阅读均已在大纲末尾列出。

## 贡献指南

欢迎补充新的课程大纲或优化现有内容：

- 新的单课时课程请在 `ppt/` 目录下新增一个独立的 Markdown 文件；新的多课时系列课程请在 `outline/` 目录下按「子目录 + README.md 总纲 + 各课时大纲文件」组织。
- 建议包含：课程概述、课程目标、时间分配、动手实践、资源与考核等结构。
- 提交前请保持术语与格式统一，并在文件末尾标注更新日期。

---

*最后更新：2026-09-02*
