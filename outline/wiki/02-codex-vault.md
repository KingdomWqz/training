---
title: 第9课 把知识库交给Codex：vault项目化与深度接入（30分钟）
course: OpenAI Codex 从入门到精通
lesson: 9
created: 2026-08-31
---

# 第 9 课：把知识库交给 Codex——vault 项目化与深度接入（30 分钟）

**教学目标**：
1. 完成 vault 的 Git 仓库化与 GitHub 私有同步，理解「版本控制 = 个人记忆的时间机器」
2. 能为知识库编写专属 AGENTS.md（目录职责 / 命名规范 / frontmatter 模板），让 Codex 遵守你的整理规则
3. 掌握三类高频整理任务的指令模式：批量补元数据、重构归档、生成 MOC 索引
4. 会把固定整理流程封装成 Skill，并实现对话式问答自己的知识库

## 时间分配与内容大纲

### 一、导入：从「文件夹」到「项目」（3分钟）
1. 回顾第 7 课作业：Skill+MCP+Automation+/goal 组合方案蓝图——**本模块就是它的落地场景**
2. 核心转变一句话：**vault 不只是笔记软件的文件夹，而是 Codex 的一个项目**——AGENTS.md / Skills / MCP / Git 全部适用
3. 认知锚点：你在知识库里立的所有规矩，本质都是写给 AI 看的说明书

### 二、vault 项目化：Git 与 GitHub 同步（7分钟）
1. 为什么给笔记上 Git：误删可恢复、改史可回溯、换设备不丢；**GitHub 私有仓库 = 免费同步盘**
2. 实操流程：

   ```bash
   cd 我的vault
   git init && git add -A && git commit -m "init: vault 初始化"
   # 在 GitHub 创建私有仓库后
   git remote add origin git@github.com:me/vault.git && git push -u origin main
   ```

3. `.gitignore` 建议（示例）：`.obsidian/workspace*`（界面状态属本地配置）、`.trash/`
4. 冲突纪律：多设备使用**先 pull 再写再 push**；Obsidian Sync 等付费方案与 Git 方案的取舍一句话带过
5. 顺手养成：commit message 也可以让 Codex 起草

### 三、为知识库编写 AGENTS.md（8分钟）
1. 最小可用版四要素（示范逐段讲解）：

   | 要素 | 示例约定 |
   |------|---------|
   | 目录职责 | Inbox 只进不出（由整理流程清空）；Projects 只放有截止时间的事 |
   | 命名规范 | 笔记 `YYYY-MM-DD 主题`；索引页统一 `MOC-主题` |
   | frontmatter | 每篇必含 tags / created / status 三字段 |
   | 写作风格 | 原子化：一篇只讲一个概念；观点给出来源链接 |

2. **实战演示：整理收件箱**——「按 AGENTS.md 把 Inbox 里 10 条笔记归位：补 frontmatter、建立双链、可合并的合并、该归档的移入 Archives，先给方案再动手」
3. **实战演示：生成 MOC**——「为 #ai 标签下所有笔记生成 MOC-AI 索引页，按子主题聚类」
4. 关键习惯：**整理类任务先让 Codex 输出方案（dry-run），人工确认后再执行；大重构前必须 commit**

### 四、Skill 封装与对话式检索（8分钟）
1. 把固定流程封装成「note-organizer」Skill（`.agents/skills/`，呼应第 7 课 SKILL.md 规范）：

   ```markdown
   ---
   name: note-organizer
   description: 当用户要求整理 Inbox、归档笔记或补全 frontmatter 时使用。
   ---

   按 AGENTS.md 的规范执行：
   1. 先列出变更方案等待确认
   2. 确认后执行归位 / 补链 / 合并
   3. 汇报 diff 与跳过项
   ```

2. **对话式检索实战**：
   - 「我三个月前关于提示词工程记过什么？」
   - 「把我所有提到 RAG 的笔记串成一篇综述草稿」
3. 可选进阶：社区 Obsidian MCP Server（如基于 Local REST API 插件的方案，示例方案，以社区项目现状为准）可直连运行中的 Obsidian；**起步阶段纯文件系统操作零依赖，已足够**
4. 安全边界：知识库场景无 full-access 必要；整理一律 workspace-write + 先方案后执行

### 五、动手实操与收尾（4分钟）
1. 实操链路：写 AGENTS.md → 让 Codex 整理 Inbox 3 条笔记 → review diff → commit
2. 本课小结 + 预告：规则和手艺都有了，下一课让整套系统**自动转起来**

## 本课课堂演示清单
- vault git init → 推送 GitHub 私有仓库全流程
- Codex 按 AGENTS.md 整理 Inbox 的 before/after 对比
- note-organizer Skill 触发 + 对话式知识库问答两连

## 学员动手实践任务
1. vault 完成 git init 并推送到 GitHub 私有仓库
2. 为 vault 编写 AGENTS.md，至少包含目录职责、命名规范、frontmatter 三项
3. 让 Codex 整理 Inbox 至少 5 条笔记，人工 review 后 commit
4. 向知识库提 2 个「只有你自己知道答案」的问题，验证检索效果并记录失败案例

## 课后作业
1. 把历史最常用的一个分类/文件夹迁入 PARA 对应层，并让 Codex 为该域生成一张 MOC
2. 写一个属于你自己的整理 Skill（如「文献笔记标准化」「周记生成」），description 写清触发时机

## 教学准备清单
- [ ] 演示 vault 预置 10+ 条「脏笔记」（缺 frontmatter / 未归位 / 重复）供整理演示
- [ ] GitHub 私有仓库创建流程课前预演
- [ ] （可选）预装 Local REST API 插件与对应 MCP Server 备用

## 参考资源
- 第 7 课讲义：SKILL.md 结构规范与四级存放路径
- Git 入门：任意版本控制基础教程（学员按需）

---

*最后更新：2026-08-31*
