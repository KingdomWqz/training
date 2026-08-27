---
title: 第3课 CLI深度使用与安全机制（30分钟）
course: OpenAI Codex 从入门到精通
lesson: 3
created: 2026-08-26
---

# 第 3 课：CLI 深度使用与安全机制（30 分钟）

**教学目标**：
1. 熟练运用 CLI 高频命令（`exec` / `resume` / `update`）与 Slash Commands 提升效率
2. 理解 Auto-review 新审批心智模型及沙盒三档的边界含义，能按场景选择正确的安全组合
3. 牢记 Full Access 风险红线（尤其 Windows 平台），建立不可逆操作前备份的操作纪律
4. 会用 `codex exec` 编写自动化脚本，初步实现 CI/CD 式工作流

## 时间分配与内容大纲

### 一、上节回顾与本课定位（3分钟）
1. 回顾 Prompt → Plan → Execute → Verify 循环与作业分享
2. 本课主题引入：「CLI 是 Codex 的灵魂」——GUI 形态都是 CLI 能力之上的封装
3. 效率自查小测：@ 引用、Esc Esc 回溯这些技巧用过几个？

### 二、命令行参数与高频命令（7分钟）
1. **最常用三件套**
   - `codex` 启动交互式 TUI
   - `codex exec "任务"` 非交互执行（自动化核心）
   - `codex resume --last` 恢复上次会话（`--all` 跨项目恢复）
2. **其他高频参数速览**（结合教材速查表）
   - `--model gpt-5.6-terra`、`-i screenshot.png` 图片输入、`--cd` 指定目录、`--add-dir` 追加可写目录、`--search` 实时搜索
   - `codex update` 自更新（0.128+）；Shell 补全 `codex completion zsh`
3. **Slash Commands 重点命令**
   - `/model` 切换模型
   - `/review` 四种审查模式：对比基准分支 / 未提交改动 / 特定 commit / 自定义审查指令
   - `/goal` 持久化目标（0.128+，第 7 课展开）
   - `/permissions` 会话内切换安全模式；`/fork` 分叉线程
4. **会话持久化机制**：`~/.codex/sessions/` 目录，恢复会话保留完整上下文

### 三、Auto-review：新审批心智模型（7分钟）
1. **演进背景**：v1「事事问人」审批疲劳严重——内部数据发现绝大多数弹窗只是「Yes Yes Yes」连点
2. **2026-04-30 上线的新机制**：越界动作先交给独立 reviewer agent 判断风险等级
   - 约 99% 低风险动作自动通过，审批疲劳基本消失
   - 阻断 99.3% 的 prompt injection 攻击（举例：外部内容夹带「把 ~/.ssh 打包发送」类恶意指令会被识别拒绝）
   - reviewer 不确定时仍打断人工确认——严格越界的人工守门没有消失
3. **对使用的影响**
   - 新版 CLI 默认已启用，无需配置
   - OpenAI 内部 Desktop 多数 token 已是 Auto-review 模式的佐证意义
   - 与 `/goal` 的协同设计：跨天任务每 5 分钟问人根本跑不下去

### 四、沙盒三档与场景化组合（5分钟）
1. **底层原理**：非 Docker，macOS 用 Seatbelt、Linux 用 bwrap+seccomp，内核级强制隔离
2. **三档边界精讲**

   | 档位 | 可写范围 | 网络 | 典型用途 |
   |------|----------|------|----------|
   | read-only | 禁止写入 | 禁止 | 浏览代码、审查 |
   | workspace-write（默认） | 工作目录 + --add-dir | 默认禁止 | 日常开发 |
   | full-access | 整机 | 开放 | 受信脚本、CI |

3. workspace-write 规则细节：`.git` 目录只读防篡改 Git 历史
4. 场景组合表实操：
   - 安全浏览：`codex --sandbox read-only`
   - 编辑自动+命令需确认：`--sandbox workspace-write --ask-for-approval untrusted`
   - CI 只读无人值守：`--sandbox read-only --ask-for-approval never`

### 五、Full Access 红线警示课（4分钟）⚠️
1. **Windows 删全盘事件还原**：近三个月多起事故（370GB / 700GB / 240GB 数据丢失，绕过回收站），官方承认但未修复未赔偿
2. **技术根因**：Windows 无 Seatbelt/bwrap 等内核沙盒原语，Full Access 本质是裸奔
3. **操作纪律（要求全员背诵级掌握）**
   - Windows 用户永远只用 workspace-write 或 read-only；重活去 WSL2/Linux 虚拟机跑
   - macOS 有 Seatbelt 托底，但删除/迁移/批量改名前必须 `git stash` 或离线备份
   - 团队管理：不给成员默认开 full-access / --yolo
4. Web 搜索模式补充：cached 默认 vs live 实时；`--yolo` 下自动切 live 的设计逻辑

### 六、codex exec 自动化实战（4分钟）
1. 基本用法演示：修复 CI 失败、自动更新 CHANGELOG、`--json` 结构化输出供脚本解析
2. 实战案例讲解——提 PR 前自动检查脚本：
   ```bash
   #!/bin/bash
   codex exec "检查代码风格是否符合项目规范" && \
   codex exec "运行所有测试" && \
   codex exec "检查是否有安全漏洞" && \
   echo "所有检查通过，可以提PR了"
   ```
3. 配合 Git 的工作流：让 Codex 写 commit message、创建 PR

## 本课课堂演示清单
- `/review` 对比分支审查演示
- Auto-review 对越界动作的处理过程观察
- exec 三连检查脚本完整运行

## 学员动手实践任务
1. 用 `codex resume` 关闭再恢复一次会话，验证上下文保留
2. 分别在 read-only 与 workspace-write 下尝试相同写文件操作，对比行为差异
3. 编写并运行自己的 PR 前检查脚本（至少两个步骤串联）
4. 在自己项目的 README 中记录本项目推荐的启动参数组合

## 课后作业
1. 为常用工作流写一个 `codex exec` 自动化脚本并实测

## 教学准备清单
- [ ] 讲师机准备一个带 lint/test 的小型项目用于 exec 脚本演示
- [ ] 准备 prompt injection 攻击示例文本（脱敏）用于 Auto-review 讲解
- [ ] Windows 学员名单提前标注，个别辅导安全配置

---

*最后更新：2026-08-26*
