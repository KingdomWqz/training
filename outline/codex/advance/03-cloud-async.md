---
title: 第6课 云端异步开发新范式（30分钟）
course: OpenAI Codex 从入门到精通
lesson: 6
created: 2026-08-26
---

# 第 6 课：云端异步开发新范式（30 分钟）

**教学目标**：
1. 理解同步对话与异步委派的本质区别，能判断什么任务适合丢给云端
2. 掌握云端任务的完整生命周期与 Environments 配置（setup 脚本、环境变量 vs Secrets、容器缓存）
3. 深刻理解「agent 阶段默认断网」的安全设计及 prompt injection 攻防原理
4. 会用 @codex 触发 GitHub PR 审查与任务委派，了解 Linear/Slack/Chrome 扩展集成

## 时间分配与内容大纲

### 一、导入：两种工作模式的分野（3分钟）
1. 回顾第 1 课的对比表，聚焦本课主角 Cloud 的独特价值
2. 核心心智转换：「坐在终端前对话」vs「把任务丢出去就不管了」
   - 同步适合：需要实时讨论的复杂决策
   - 异步适合：已经想清楚要做什么、只需执行的任务
3. 入口：chatgpt.com/codex 连接 GitHub 即可开始，浏览器关掉照跑

### 二、云端任务生命周期五步精讲（7分钟）
1. **创建容器 checkout 代码**：每任务独立容器互不干扰
2. **运行 setup 脚本（可联网）**：npm/pip install 阶段；有缓存时额外跑 maintenance 脚本更新依赖
3. **应用网络设置**：setup 结束后默认进入 agent 断网阶段
4. **Agent 循环执行**：编辑代码 → 运行检查 → 验证结果 → 继续编辑；自动读取 AGENTS.md 找 lint/test 命令自证
5. **展示结果**：完整 diff + 追问通道；满意直接创建 PR 或用 `codex apply` 应用到本地

### 三、Environments 配置详解（7分钟）
1. **Universal 默认镜像**：预装常用语言工具链，多数项目免配置；版本可指定（参考 github.com/openai/codex-universal）
2. **自定义 setup 脚本**
   ```bash
   pip install pyright
   poetry install --with test
   pnpm install
   ```
3. **易踩之坑**：setup 与 agent 运行在不同 Bash session——setup 里 export 的变量 agent 拿不到；持久化写 ~/.bashrc 或环境配置面板
4. **环境变量 vs Secrets 对照**（安全核心）

   | 类型 | 可用阶段 | 说明 |
   |------|----------|------|
   | 环境变量 | setup + agent 全程 | 普通变量 |
   | Secrets | 仅 setup | 加密存储，agent 开始前移除 |

   为什么：agent 阶段代码可能被 prompt injection 影响，密钥必须限制在 setup 阶段
5. **容器缓存机制**：最长 12 小时；修改脚本/变量后自动失效；不兼容时手动 Reset cache

### 四、GitHub 集成实战（5分钟）
1. **@codex 双动作**：PR 评论 `@codex review` → 眼睛 emoji 确认 → 标准 GitHub code review 回复；其他评论内容 → 创建云端任务（如 `@codex fix the CI failures`）
2. Automatic reviews：每次新 PR 自动触发审查
3. **审查标准联动 AGENTS.md**：Review guidelines 生效；一次性行内指令示例 `@codex review for security regressions`
4. 默认只标 P0/P1 问题——想让文档 typo 也被报需在 AGENTS.md 注明「Treat typos in docs as P1」
5. 配套修复类场景四例：PR 审查 / issue→PR 一条龙 / 大改动面重构 / 并行修 10 个 bug 批量提交

### 五、Codex for Chrome：另一种「云端」（3分钟）
1. **与 Cloud 的本质差异**：Cloud 在无登录态的独立容器里跑；Chrome 扩展复用你已登录的真实会话干活
2. 典型任务：整理 LinkedIn 列表、Gmail 分类打标、Salesforce 抓数、操作内部 dashboard——过去要写爬虫解决登录反爬，现在直接交给 agent
3. 细节要点：thread 自动归 tab group 关组即清理；按站点 allowlist/blocklist（银行/生产后台建议手动 block）；仅 Chrome 支持且需从 App 内 Plugins 面板跳转安装
4. 选型口诀：要登录态/真实账号/跨 SaaS → Chrome 扩展；纯代码/GitHub 留痕 → Codex Cloud

## 本课课堂演示清单
- 从 chatgpt.com/codex 提交一个真实仓库的重构任务到 diff 产出全程
- setup 脚本缺失导致的失败案例 + 修复对照
- （有条件）在演示仓库 PR 上实际触发 `@codex review`

## 学员动手实践任务
1. 连接自己的 GitHub，向一个练习仓库提交第一个云端任务并审查 diff
2. 为该仓库写一个自定义 setup 脚本并验证缓存命中行为
3. 在任一开源项目的练习分支上体验 @codex review（或观看讲师演示后书面总结其输出结构）
4. 列出你工作中 5 个候选任务并标注：适合同步 / 适合异步 / 需要 Chrome 扩展登录态

## 课后作业
1. 把一周积压的小型 issue 整理成 5 个以上描述清晰的云端任务批量提交，记录完成率与 diff 质量
2. 为你的项目补齐一份「云端任务描述模板」（含文件路径、预期行为、验证方式三要素）

## 教学准备清单
- [ ] 讲师 GitHub 测试仓库预连接 Codex Cloud 并开通权限
- [ ] 准备 prompt injection 案例（脱敏版）截图材料
- [ ] 确认学员账号均有 Cloud 使用权限（Plus 及以上；Enterprise 注意管理员开关）

---

*最后更新：2026-08-26*
