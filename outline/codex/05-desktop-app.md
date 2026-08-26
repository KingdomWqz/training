---
title: 第5课 桌面App多Agent协作（30分钟）
course: OpenAI Codex 从入门到精通
lesson: 5
tags:
  - training
  - codex
created: 2026-08-26
---

# 第 5 课：桌面 App 多 Agent 协作（30 分钟）

**对应教材**：《OpenAI Codex 从入门到精通》§06 Codex App：多Agent的指挥中心
**教学目标**：
1. 掌握 Codex 桌面 App 的项目/线程管理与 Local / Worktree / Cloud 三种线程模式
2. 理解 Worktree 隔离机制与 Handoff 流程，能安全地组织多 Agent 并行开发
3. 了解「桌面五件套」能力边界，会用 diff 面板 inline 评论进行精准反馈
4. 正视 MultiAgentV2 已知缺陷，掌握 smoke test 先行、生产慎用的使用纪律

## 时间分配与内容大纲

### 一、上节回顾与场景导入（3分钟）
1. 回顾 AGENTS.md 要点与作业分享
2. 场景引入：需要同时推进三个独立功能时，CLI 单线程的局限——开三个终端 tab 手动管三个 worktree，「到第三件事基本崩了」
3. 本课主线：从「指挥一个 Agent」升级为「指挥一支 Agent 编队」

### 二、App 总览与项目管理（5分钟）
1. **安装与平台支持**：macOS `codex app`；Windows 从 Microsoft Store；Linux 无官方桌面版（CLI + Chrome 扩展补位）；iOS/Android 仅 Cloud 网页
2. **界面结构**：左侧项目+线程面板、中间对话区、右侧 diff 面板
3. **项目隔离原则**：monorepo 拆成多个 App 项目，sandbox 只含各自文件防误改
4. **三种线程模式精讲**

   | 模式 | 工作方式 | 适用场景 |
   |------|----------|----------|
   | Local | 直接在项目目录工作 | 常规开发 |
   | Worktree | Git worktree 隔离 | 并行多功能互不干扰 |
   | Cloud | 远程云端环境 | 本地算力不足/特殊服务器环境 |

### 三、Worktree 与 Handoff 深度剖析（7分钟）
1. **解决的核心痛点**：多个 Agent 同时改同一仓库如何互不冲突
2. **三步机制**
   - 在 `$CODEX_HOME/worktrees` 创建独立 checkout（detached HEAD 不污染分支列表）
   - Agent 在隔离目录干活，本地不受影响
   - 完成后两条路：worktree 上直接建分支→push→PR；或 Handoff 移回 Local 在熟悉 IDE 中检查
3. **Handoff 不是文件复制**：Codex 代管底层 Git 操作，在 Local/Worktree 之间安全移动改动
4. **关键限制**：同一分支同一时间只能被一个 checkout 使用——冲突时用 Handoff 而非手动切分支

### 四、内置工具链速览（5分钟）
1. **diff 面板**：查看未提交/整分支/最近一轮改动；inline 评论锚定具体代码行——比聊天框描述「第几行有问题」精确得多
   - 反馈后需明确指令：「处理inline评论，改动范围尽量小」
2. **集成终端**：Cmd+J 切换；scope 跟随线程；**Codex 能读取终端输出**——dev server 报错无需复制粘贴它自己能看到
3. **其他实用项快讲**：语音输入 Ctrl+M、浮动窗口 Always on Top、防休眠开关、通知策略、图片拖拽输入
4. IDE Extension 同步：同项目打开时自动互通上下文

### 五、桌面五件套与多Agent并行（7分钟）
1. **五件套定位速览**（2026-04-16 大版本）
   - Computer Use：独立虚拟光标操作本机应用，不抢用户鼠标，多 agent 并行互不打架
   - In-App Browser：网页上直接圈元素加评论，得到带空间锚点的反馈（局限：无法复用登录态）
   - Image Generation：gpt-image-1.5 集成，截图→分析→出图→插代码一条流
   - Memory 预览：记住偏好与纠正，「隐式 AGENTS.md」心智
   - Automations 续跑：调度未来任务、跨天跨周续跑（第 7 课展开）
2. **多 Agent 并行的显式配置**（CLI 0.128+）：
   ```toml
   [agents]
   max_threads = 6
   max_depth = 1
   job_max_runtime_seconds = 1800
   ```
   agent 角色定义放 `~/.codex/agents/*.toml`（个人）或 `.codex/agents/*.toml`（项目）
3. **真实实战流程四步法**（web 项目三任务并行案例）
   - 主 thread 写清三个互相独立的任务并指定参考文档
   - 为每个子任务开 Worktree 线程实现物理隔离
   - 边干边审：Auto-review 兜底 + 主线程盯进度 + 必要时切子线程看 diff
   - 先完成先回收：review → Handoff → 集成测试 → commit & PR

### 六、MultiAgentV2 风险教育与使用纪律（3分钟）⚠️
1. **三个反复出现的已知 Bug**（含 Issue 编号供检索）
   - 子 agent 死循环：最简 PONG 指令陷入 MCP listing 死循环（#16657）
   - 子 agent 串话：裸 JSON 回执漏进主聊天（#17523）
   - stdio MCP 栈泄漏：long-lived 多 agent 会话被拖垮（#14233）
2. **不要放进 MultiAgentV2 的三类任务**：生产代码并行批改 / 强外部副作用任务 / 数小时长任务
3. **适合场景**：一次性、可中断、低风险的并行尝试（多方案重写测试对比等）
4. **操作纪律**：每次升级 CLI 后先跑「3 个子 agent 各报一句 PONG」smoke test，通过再上正式任务

## 本课课堂演示清单
- App 安装/登录/项目添加全过程
- 开两个 Worktree 线程并行执行两个小任务并分别回收合并
- diff 面板 inline 评论 → Agent 精准修复闭环演示
- （有条件时）Computer Use 操作计算器/Finder 的效果展示与风险说明

## 学员动手实践任务
1. 安装 Codex App 并将第 2 课的项目添加为新项目
2. 创建一个 Worktree 线程执行一个小型重构任务，走完 review → 合并全流程
3. 对 Agent 提交的代码使用 inline 评论提出至少两处修改意见并验证精准生效
4. 尝试本地/云双端登录体验同一项目的线程同步

## 课后作业
1. 设计一个你工作中的三任务并行方案（写明每个任务的隔离方式与验收标准）
2. 执行一次完整的 smoke test 并记录结果
3. 阅读《OpenAI Codex 从入门到精通》§06 全章

## 教学准备清单
- [ ] 讲师机 macOS/Windows 各一台用于平台差异演示（至少其一）
- [ ] 准备带三份独立改动画面的演示仓库
- [ ] 打印 MultiAgentV2 已知 Bug 清单（含 Issue 号）作为课堂资料

## 参考资源
- 教材：§06 Codex App 全章；附录A（/agent、/apps 等 App 相关命令）

---

*最后更新：2026-08-26*
