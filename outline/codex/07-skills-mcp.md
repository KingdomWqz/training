---
title: 第7课 Skills、MCP、Automations与goal 四大扩展（30分钟）
course: OpenAI Codex 从入门到精通
lesson: 7
created: 2026-08-26
---

# 第 7 课：扩展能力四层体系——Skills / MCP / Automations / goal（30 分钟）

**教学目标**：
1. 理解四层扩展各自回答的问题，建立「操作手册 → 应用商店 → 插头接口 → 定时器 → 项目经理」的整体框架
2. 掌握 SKILL.md 结构规范与 Progressive Disclosure 加载机制，能独立创建并正确触发一个 Skill
3. 会配置 MCP Server 连接外部工具，理解 STDIO/HTTP 两种类型与超时等精细控制项
4. 能用 Automations 编排定时任务并用 /goal 发起跨 session 长目标，同时守住安全边界

## 时间分配与内容大纲

### 一、导入：从一个助手到一个工作系统（3分钟）
1. v1 三层 → v2 四层的演进回顾：新增的 `/goal` 定义「这件事不做完不算完」
2. 五层体系总览表：

   | 层面 | 回答的问题 | 类比 |
   |------|-----------|------|
   | Skill | 做什么、怎么做 | 操作手册 |
   | Plugin Marketplace | 从哪找现成的 | 应用商店 |
   | MCP | 连什么工具拿什么信息 | 接口和插头 |
   | Automation | 什么时候做做多频繁 | 定时器 |
   | /goal | 不做完不算完 | 项目经理 |

### 二、Agent Skills 详解与实操（9分钟）
1. **结构极简**：一个目录 + 一个含 `name`/`description` frontmatter 的 SKILL.md
   ```markdown
   ---
   name: skill-name
   description: Explain exactly when this skill should and should not trigger.
   ---

   Skill instructions for Codex to follow.
   ```
2. **Progressive Disclosure 机制**：启动只读 metadata 占用极少 token；相关时才加载全文——装几十个 Skill 撑不爆上下文；**description 质量直接决定触发准确率**
3. **两种调用方式**：显式 `$skill-name`（CLI 输入 `$` 自动补全）vs 隐式自动匹配
4. **四级存放路径**

   | 层级 | 路径 | 场景 |
   |------|------|------|
   | REPO | `.agents/skills/` | 团队共享项目级 |
   | USER | `~/.agents/skills/` | 个人跨项目 |
   | ADMIN | `/etc/codex/skills/` | 企业统推 |
   | SYSTEM | 内置 | skill-creator 等 |

5. **行业格局**：SKILL.md 已成跨 agent 事实标准（Codex/Claude Code/Cursor/Gemini CLI 共用），第三方 marketplace 1600+ skills；迁移成本示例：`.claude/skills/` 改 `.agents/skills/` 一处路径即可
6. **安全开关**：`agents/openai.yaml` 中 `allow_implicit_invocation: false` 禁止隐式触发——有破坏性操作的 Skill 必设
7. **动手环节**：用 `$skill-creator` 创建第一个团队专属 Skill（如「提 PR 前自检清单」），在 config.toml 启停验证

### 三、MCP：连接外部世界的协议（7分钟）
1. 定位类比：Codex 的「USB 接口」；Codex 是 MCP-based API 消费最大单一驱动者
2. **两种 Server 类型**：STDIO 本地进程 vs Streamable HTTP 远程服务（支持 Bearer/OAuth，`codex mcp login <name>`）
3. **配置实操**
   ```bash
   codex mcp add context7 -- npx -y @upstash/context7-mcp
   codex mcp add linear --url https://mcp.linear.app/mcp
   codex mcp list        # TUI 里 /mcp 查看活跃 server
   ```
4. config.toml 精细控制项速览：startup_timeout_sec / tool_timeout_sec / enabled / required / enabled_tools / disabled_tools
5. 常用 Server 清单讲评：OpenAI Docs、Context7、Figma（设计稿→代码）、Playwright（浏览器自动化）、Chrome DevTools、Sentry（线上错误）、GitHub（PR/issue 管理）
6. 彩蛋能力：`codex mcp-server` 让 Codex 自己成为其他 Agent 的工具

### 四、Automations 定时任务系统（5分钟）
1. 2026-04 升级要点：从「定时跑 prompt」进化到「调度未来任务 + 跨天跨周续跑」，agent 自行 wake up
2. 配置要素：选项目 → 写 prompt → 设频率 → 选执行环境（local/worktree）；产出进 Triage 收件箱待审阅
3. **前提与建议**
   - 需要 App 保持运行且项目可访问；Git 仓库默认在独立 worktree 运行不影响本地编辑
   - **先手动跑通再设 Automation**；频率高时定期归档防 worktree 堆积
4. **权限红线**：无人值守场景禁用 full access（呼应第 3 课 Windows 删盘事件＝Full Access×Automation 最坏组合）；推荐 workspace-write + rules 选择性放开
5. 实用示例三则讲解：每日 commit 简报 / 自动修自己上周引入的 bug / 扫描 sessions 自动沉淀新 Skill
6. 现场配置一个「每日代码简报」Automation（演示）

### 五、/goal 持久化目标与四层联动（3分钟）
1. 解决什么：普通 prompt 会话一清就没了；/goal 是 app-server 一等对象，**跨 /clear、跨 compaction、跨 session 存活**
2. 五种状态机：pursuing / paused / achieved / unmet / budget-limited
3. 经典案例：Alex Finn 一小时自治构建完整小游戏（目标 + image generation skill + 关屏走人）；「Ralph loop」长程自治模式
4. **适用判断**：适合跨多 session 长任务、完成判据明确、愿意下放决策权；不适合短任务与需要人反复介入的调试探索
5. 反面教材：Karpathy autoresearch issue #57——长程目标对模型纪律性要求极高
6. 组合拳示例（本课收束）：goal + GitHub/Sentry MCP + review skill + 每 2 小时检查的 Automation = 周五回来收「这周修了多少 bug」报告

## 本课课堂演示清单
- skill-creator 全流程建 Skill + 显式/隐式两种触发对比
- codex mcp add 接入 Context7 并实际调用查文档
- Automations 面板配置与 Triage 收件箱查看
- /goal 设置→手动 pause→resume 的状态变化观察

## 学员动手实践任务
1. 创建一个属于你的 Skill 并提交到 `.agents/skills/`，测试两种触发方式
2. 接入一个 MCP Server（推荐 Context7 或 Playwright），完成一次真实调用
3. 为练习仓库设置一个低频（每日一次）的 Automation 并次日查验 Triage 结果
4. 用 /goal 发起一个 30~60 分钟能达成的中型任务，期间切窗口做别的事，回来看状态是否 achieved

## 课后作业
1. 把你重复解释过三次以上的偏好提炼成一个 Skill 并写清楚 description
2. 设计一个「Skill+MCP+Automation+/goal」组合方案（书面蓝图即可，不必全部落地）

## 教学准备清单
- [ ] 讲师机预装 2~3 个常用 MCP Server 备用
- [ ] 准备一个团队工作流 Skill 样例仓库供学员 fork
- [ ] Automations 演示需提前登录 App 并保持后台运行

## 参考资源
- agents 标准：SKILL.md 跨工具格式约定

---

*最后更新：2026-08-26*
