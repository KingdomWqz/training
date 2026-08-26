---
title: 第1课 认识Codex与快速上手（30分钟）
course: OpenAI Codex 从入门到精通
lesson: 1
tags:
  - training
  - codex
created: 2026-08-26
---

# 第 1 课：认识 Codex 与快速上手（30 分钟）

**对应教材**：《OpenAI Codex 从入门到精通》§01 五种形态一个系统、§02 10分钟开始用、附录B 定价与套餐
**教学目标**：
1. 理解 AI 编程工具从补全 → 对话 → Agent 三次范式变迁，说清 Codex 在当前格局中的定位
2. 掌握 Codex 五种形态的能力边界与适用场景，能根据自身情况选择正确的起步入口
3. 独立完成一种形态的安装、登录与首次对话，跑通「提问 → 得到分析结果」的最小闭环
4. 了解套餐与计费基本盘，建立用量成本意识

## 时间分配与内容大纲

### 一、课程导入与AI编程工具格局（4分钟）
1. **破冰：学员使用现状调查**
   - 是否用过 Copilot / Cursor / Claude Code / Codex
   - 本次培训最想解决的问题收集
2. **AI 编程工具三次范式变迁**
   - 补全时代（2022，Copilot）：更聪明的输入法，写代码的还是人
   - 对话时代（2023-2024，Cursor）：描述效果而非实现，但仍是 IDE 的延伸
   - Agent 时代（2025-2026）：终端 Agent 自主规划、执行、验证，人从「写代码」变成「做决策」
3. **2026 年中的两强格局**
   - Codex 运营数据：周活 400 万，年初至今涨 8 倍
   - Claude Code 与 Codex 各有生态；Copilot 式补全已是上个时代的玩法

### 二、Codex五种形态详解（8分钟）
1. **CLI**：本地终端 Agent，Rust 开源，三种沙盒模式，适合完整掌控与终端工作流
2. **桌面 App**：macOS/Windows，「五件套」（Computer Use / In-App Browser / Memory / Image Generation / Automations 续跑），原生多任务并行
3. **Cloud 云端版**：chatgpt.com/codex，云端容器隔离执行、agent 阶段默认断网、产出 diff/PR
4. **IDE 扩展**：VS Code/Cursor/Windsurf 侧边栏，可一键委派云端
5. **Chrome 扩展**（2026-05 新增）：复用已登录浏览器会话，操作 LinkedIn/Gmail/Salesforce/内网等登录态页面
6. **形态对比表精讲**（结合教材表格）
   - 运行位置、并行能力、是否需要本地环境、最适合场景五个维度
7. **共享配置体系**：`~/.codex/config.toml` + AGENTS.md + 同一 ChatGPT 账号，五种形态数据互通
8. **花叔入口推荐**：主力 CLI+Cloud 覆盖 80% 需求；按痛点逐个解锁其他形态，避免一上来全装

### 三、动手安装与环境配置（10分钟）
1. **前提条件检查**
   - ChatGPT Plus 及以上账号（说明各套餐差异，见附录B）
   - Node.js 18+（仅 CLI 和 IDE 扩展需要）
2. **方式一：安装 CLI**（主实操）
   ```bash
   npm install -g @openai/codex
   # 或 macOS/Linux: brew install codex
   codex        # 首次运行，浏览器授权登录 ChatGPT 账号
   ```
3. **服务器/CI 场景的 API Key 登录**
   ```bash
   export OPENAI_API_KEY=sk-...
   ```
4. **认识 TUI 全屏界面**：输入框、输出面板、状态栏；与流式输出的区别
5. **方式二~四概览演示**（讲师演示，学员课后自装）
   - `codex app` 启动桌面 App；chatgpt.com/codex 直接用云端；扩展市场搜 `openai.chatgpt`
6. **配置文件初识**：`~/.codex/config.toml` 中 model、web_search 等常用项

### 四、第一次对话实战（5分钟）
1. 进入一个真实 Git 项目目录，启动 `codex`
2. 实践指令一：`Explain this codebase to me` —— 观察自动扫描项目结构的行为
3. 实践指令二：`Find any potential bugs or code smells in this project`
4. 观察安全机制表现：读文件免确认，修改文件/执行命令先询问
5. 体验 `codex --full-auto` 与默认 Auto 模式的差别

### 五、套餐计费与成本意识（3分钟）
1. **个人三档套餐**：Plus $20 / Pro $100 / Pro $200，各自用量倍率
2. **关键认知：模型费率差异巨大**
   - GPT-5.5 credit 费率是 GPT-5.4 的两倍——「默认模型被腰斩配额」现象
   - 结论先行：日常任务用 GPT-5.4，关键任务才切 GPT-5.5（第 3 课展开）
3. **/status 查看用量**的习惯培养

## 本课课堂演示清单
- 五形态对比表讲解（教材 §01）
- CLI 安装 + 登录全过程
- 对已有仓库进行代码库解读与潜在 Bug 扫描

## 学员动手实践任务
1. 完成 Codex CLI 安装并用 ChatGPT 账号登录成功
2. 选择自己熟悉的任一 Git 项目，让 Codex 输出一份项目结构概览
3. 让 Codex 指出该项目的 3 个以上潜在问题，并记录它给出的建议是否准确
4. （课后）按自身情况再安装一种新形态：App 或 Cloud 或 IDE 扩展

## 课后作业
- 用一句话写下你目前工作流中最想用哪种形态解决的痛点，下节课分享
- 阅读《OpenAI Codex 从入门到精通》§01、§02、附录B

## 教学准备清单
- [ ] 讲师机预装 Node.js 18+ 并完成 codex 登录
- [ ] 准备一个中等规模的开源仓库作为演示项目
- [ ] 教室网络可访问 api.openai.com 与 chatgpt.com（受限环境需提前说明替代方案）
- [ ] 投屏分辨率适配 TUI 全屏界面

## 参考资源
- 教材：§01 五种形态一个系统；§02 10分钟开始用；附录B 定价与套餐
- 官方文档：developers.openai.com/codex
- 更新日志：developers.openai.com/codex/changelog

---

*最后更新：2026-08-26*
