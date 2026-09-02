# 培训资料库（Training）

本仓库收集面向 AI 编程工具、智能体平台与内容创作的教学大纲、演示课件和实践资料，用于课程培训、技术分享和自学参考。

## 培训主线

本培训按“先解决日常工作，再扩展工具边界，最后升级方法论”的路径展开，逐步建立从工具使用到 AI Native 实践的完整能力：

1. **核心 Harness 工具**：学习 Codex、Claude Code 等核心 Harness 的使用，先解决写代码、改项目、查问题等最日常的工作。
2. **周边常用工具**：延伸到 CCSwitch、LobeHub 等工具，覆盖配置管理、模型切换、智能体协作等更多使用场景。
3. **验证过的能力沉淀**：将已经验证有效的工作方式沉淀为 Skill、MCP、Prompt 等可复用资产，让经验能够复用、共享和规模化。
4. **工具之外的思维升级**：理解 OPC（One Person Company，个人公司）与 AI Native 思维，重新思考个人生产力、工作流和组织协作方式。
5. **四大实战场景**：把方法落到个人知识库、Web 应用开发、生图和生视频四类高频场景中，完成从信息沉淀到应用成品的完整实践。

这条主线对应三层学习目标：**会用工具 → 能搭工作流 → 能持续产出**。仓库中的课程大纲、课件与演示素材均围绕这条路径组织。

## 课程亮点

- **从真实工作出发**：围绕写代码、做网页、整理知识、制作图片和生成视频等高频任务展开，学完即可迁移到日常工作。
- **工具与方法一起学**：不仅介绍 Codex、Claude Code、CCSwitch、LobeHub 等工具，还讲清楚如何选择工具、组织上下文和设计工作流。
- **每一步都有可见成果**：课程强调边学边做，从一个可运行的项目、一套个人知识库，到可发布的图片和视频作品，持续积累作品集。
- **沉淀可复用资产**：把有效经验整理成 Skill、MCP 和 Prompt，帮助个人和团队复制成功做法，越用越快。
- **覆盖四大实战场景**：个人知识库、Web 应用开发、生图、生视频，兼顾生产力提升与内容创作落地。
- **建立 AI Native 视角**：从“会使用 AI”进一步走向“用 AI 重构工作方式”，理解 OPC 与新型个人生产力。

## 目录结构

- [`outline/`](./outline)：Markdown 教学大纲。课程总纲与索引统一维护在本文件，课时内容按主题子目录组织。
- [`ppt/`](./ppt)：HTML 演示课件与版式资料，课件通常位于 `ppt/<主题>/ppt/index.html`。
- [`demo/`](./demo)：课堂演示用 Prompt 与示例素材。

## 课程总览

| 课程 | 主题 | 时长 | 大纲 |
|------|------|------|------|
| **AI Native** | 当 AI 成为团队的原住民 | 20 分钟 | [`outline/ainative/ai-native.md`](./outline/ainative/ai-native.md) · [`ppt/ai-native/ppt/index.html`](./ppt/ai-native/ppt/index.html) |
| **OPC：个人开发者与 AI 工具生态** | 工具链、配置管理与智能体协作专题（3 课时） | 60 分钟 × 3 | [课程课时索引](#opc个人开发者与-ai-工具生态) |
| **AI 生图实战** | 生图专题：文生图·图生图·修图 + 电商实战（6 课时） | 30 分钟 × 6 | [课程课时索引](#ai-生图实战) |
| **电商带货短视频 AI 生成** | 工具、脚本、生成、剪辑与运营实战（6 课时） | 30 分钟 × 6 | [课程课时索引](#ai-电商短视频) |
| **OpenAI Codex 从入门到精通** | Codex 使用、提示词、知识库与网站实战（25 课时规划） | 30 分钟 × 25 | [课程资料索引](#openai-codex-从入门到精通) |

### 课程简介

- **OPC：个人开发者与 AI 工具生态专题**：将独立开发工具全景、CCSwitch 配置管理和 LobeHub 智能体平台整合为一条 OPC 工作流，覆盖工具选型、配置复用与智能体协作。
- **[AI Native 教学大纲](./outline/ainative/ai-native.md)**：用 20 分钟建立 AI Native 的核心认知，理解模型、上下文、Agent 与 Harness 四层技术栈，以及业务、技术、组织协同的落地方法；配套提供 [HTML PPT](./ppt/ai-native/ppt/index.html)。
- **AI 生图实战：从入门到电商落地**：面向电商运营与中小卖家的 6 课时专题，覆盖文生图、图生图、修图，以及封面图、生活场景图、模特换装三大场景。
- **电商带货短视频 AI 生成实战课程**：面向电商运营与带货主播的 6 课时课程，覆盖工具选型、脚本分镜、图生视频、数字人口播、剪辑合成、发布优化与内容矩阵。
- **Codex 全栈开发课程**：课程规划共 25 个课时（每课时 30 分钟），覆盖 Codex 五种形态、核心工作流、安全机制、提示词、扩展能力、Obsidian 知识库、静态网站综合实战与内容创作迁移；当前已收录基础、知识库和网站实战资料。

### 配套资料

- [Skills 专题](#skills-资料)：提示词规范、网页访问、UI/UX、PPT 制作与浏览器自动化等资料入口。
- [课堂演示 Prompt 与素材](./demo/prompts.md)：用于课程演示的可复用 Prompt 和示例入口。

## 课程课时索引

### OpenAI Codex 从入门到精通

课程规划共 40 课时；以下为当前仓库已收录的课时大纲与实战单元。

**Codex 基础与进阶课时**

- [认识 Codex 与快速上手](./outline/codex/base/01-intro-and-setup.md)
- [第一个项目与核心工作流](./outline/codex/base/02-first-project.md)
- [CLI 深度使用与安全机制](./outline/codex/advance/01-cli-deep-dive.md)
- [Prompt 工程：把想法变成可执行任务](./outline/codex/base/04-prompt-engineering.md)
- [AGENTS.md 项目规则](./outline/codex/advance/02-agents-md.md)
- [桌面 App 多 Agent 协作](./outline/codex/base/03-desktop-app.md)
- [云端异步开发](./outline/codex/advance/03-cloud-async.md)
- [Skills、MCP、Automations 与 /goal](./outline/codex/advance/04-skills-mcp.md)

### OPC：个人开发者与 AI 工具生态

- [独立开发者工具全景](./outline/opc/01-IndieDevTools.md)
- [CCSwitch：AI 编程工具配置管理](./outline/opc/02-CCSwitch.md)
- [LobeHub：AI 智能体平台快速入门](./outline/opc/03-LobeHub.md)

### Skills 资料

- [Karpathy Prompt 指南](./outline/skill/01-karpathy-guildline.md)
- [网页访问](./outline/skill/02-web-access.md)
- [UI/UX Pro Max](./outline/skill/03-ui-ux-pro-max.md)
- [归藏 PPT 制作](./outline/skill/04-guizang-ppt.md)
- [Agent Browser](./outline/skill/05-agent-browser.md)

### AI Native 思维

- [AI Native 教学大纲](./outline/ainative/ai-native.md)

### 个人知识库实战

- [个人知识库方法论与 Obsidian](./outline/wiki/01-obsidian-vault.md)
- [把知识库交给 Codex](./outline/wiki/02-codex-vault.md)
- [知识自动化流水线](./outline/wiki/03-knowledge-automation.md)

### Web 应用开发实战

- [确定主题并准备工具](./outline/website/01-idea-and-setup.md)
- [做出第一张网页](./outline/website/02-first-page.md)
- [用 Tailwind 统一样式](./outline/website/03-tailwind-style.md)
- [拆分复用组件](./outline/website/04-components.md)
- [增加页面和内容](./outline/website/05-pages-and-content.md)
- [响应式与自测](./outline/website/06-responsive-testing.md)
- [Git 协作](./outline/website/07-git-collaboration.md)
- [发布上线与复盘](./outline/website/08-deploy-and-review.md)

### AI 生图实战

- [文生图](./outline/image/base/01-text-to-image.md) 
- [图生图](./outline/image/base/02-image-to-image.md) 
- [修图](./outline/image/base/03-image-editing.md)
- [电商封面图](./outline/image/advance/04-ecommerce-cover.md) 
- [生活场景图](./outline/image/advance/05-ecommerce-scene.md) 
- [模特换装](./outline/image/advance/06-ecommerce-tryon.md)

### AI 电商短视频

- [工具与工作流](./outline/video/base/01-tools-and-workflow.md) 
- [脚本与分镜](./outline/video/base/02-script-and-storyboard.md) 
- [图生视频](./outline/video/base/03-image-to-video.md)
- [数字人口播](./outline/video/advance/04-digital-human.md) 
- [剪辑合成](./outline/video/advance/05-editing-and-composition.md) 
- [发布与运营](./outline/video/advance/06-publishing-and-operations.md)

## 使用方式

1. 从本 README 的课程索引进入对应大纲文件。
2. 按大纲中的「教学准备清单」「实践任务」「课后作业」等模块组织课程或自学。
3. 需要授课演示时，打开 `ppt/` 下对应主题的 HTML 课件；课程资源、官方文档与扩展阅读均已在大纲末尾列出。

## 贡献指南

欢迎补充新的课程大纲或优化现有内容：

- 新的课程大纲请在 `outline/` 目录下按主题组织，并在本 README 的课程索引中登记入口。
- 新增演示课件请在 `ppt/` 下建立主题目录，并提供可直接打开的 HTML 入口（通常为 `ppt/<主题>/ppt/index.html`）。
- 建议包含：课程概述、课程目标、时间分配、动手实践、资源与考核等结构。
- 提交前请保持术语与格式统一，并在文件末尾标注更新日期。

---

*最后更新：2026-09-02*
