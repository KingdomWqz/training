---
title: 第4课 AGENTS.md 项目规则（30分钟）
course: OpenAI Codex 从入门到精通
lesson: 4
tags:
  - training
  - codex
created: 2026-08-26
---

# 第 4 课：AGENTS.md 项目规则（30 分钟）

**对应教材**：《OpenAI Codex 从入门到精通》§05 AGENTS.md：给Codex一张地图
**教学目标**：
1. 理解 AGENTS.md 作为「人机协作契约」的角色定位与三层发现合并机制
2. 掌握「写 AI 推断不出的信息」这一核心内容判断标准，能写出短而准的项目规则
3. 熟练运用 override 机制处理团队规范与个人偏好的冲突
4. 学会验证配置生效与常见问题排查

## 时间分配与内容大纲

### 一、导入：从「空降新人」到「懂规矩的老手」（3分钟）
1. 类比引入：没有 AGENTS.md，Codex 是蒙着眼写代码的新同事；有了它，一进门就懂规矩
2. 与 CLAUDE.md 的关系定位：名字不同、逻辑相通（Claude Code 的「宪法」）
3. 回顾第 2/3 课中的痛点：哪些错误如果有规矩就能提前避免？

### 二、发现机制详解：指令链如何构建（7分钟）
1. **第一层：全局级**
   - 位置 `~/.codex/AGENTS.md`（可用 CODEX_HOME 改）
   - 先找 `AGENTS.override.md`，再找 `AGENTS.md`，每层只取一个
2. **第二层：项目级**
   - 从 Git 根目录逐级向下到当前工作目录
   - 每个目录检查 override → AGENTS.md → fallback 文件名，每级取一个
3. **第三步：合并**
   - 按根到当前目录顺序拼接；**越靠近当前目录优先级越高**（覆盖前面的指令）
4. **关键约束**
   - 跳过空文件；合并总量默认上限 32KB（project_doc_max_bytes 可调至 64KB 等）
   - 超限时后面的文件被跳过——嵌套目录滥用是踩坑重灾区
5. 最佳实践：核心规则集中根目录，子目录只写该目录特有内容

### 三、override 机制：团队与个人的解耦设计（5分钟）
1. 场景还原：团队规范用 npm 并进 Git，个人偏好 pnpm——不删原文件怎么破？
2. 同级放置 `AGENTS.override.md` 即替代同级 AGENTS.md，override 加入 `.gitignore`
3. 全局 override 同理，适合短期实验，删掉即恢复
4. fallback 文件名配置：
   ```toml
   # ~/.codex/config.toml
   project_doc_fallback_filenames = ["TEAM_GUIDE.md", ".agents.md"]
   ```
   检查顺序变为 override → AGENTS.md → TEAM_GUIDE.md → .agents.md

### 四、内容标准：该写什么，不该写什么（7分钟）
1. **黄金判断法**：AI 自己能从代码推断出来的不要写；AI 猜不到的必须写
2. 对照教材表格精讲：

   | 该写 | 不该写 |
   |------|--------|
   | 构建/测试/lint 命令 | 「这是 Python 项目」这类废话 |
   | 与默认不同的风格偏好 | 语言标准规范 |
   | 架构决策与技术选型 | 详细 API 文档全文粘贴 |
   | 环境的坑与特殊配置 | 频繁变化的信息 |
   | PR 要求与完成定义 | 「整洁代码」「最佳实践」空话 |
   | 禁止事项（带替代方案） | 人尽皆知的常识 |

3. 实例解剖：教材 MyProject 示例逐行分析——不到 200 字为何足够好
   - 「完成」定义明确（CI 通过 + 文档更新）
   - 「禁止」项带原因（generated 目录是自动生成的）
4. `/init` 快速生成起点：分析项目结构产出初稿，人工增删校准
5. 长度哲学：花叔经验——短而准 > 长而全，核心文件控制在 8KB 内，每条规则对应真实踩过的坑

### 五、实战演练：为一个真实项目编写 AGENTS.md（6分钟）
学员分组或独立完成：
1. 选定练习仓库（或用第 2 课的 md2html 升级版），先运行 `/init` 得到脚手架
2. 按「该写清单」补充：实际构建命令、测试要求、目录结构说明、PR 标准
3. 写入至少两条「带原因的禁止事项」和一条明确的「完成定义」
4. 追加一条高价值行为规则（源自教材 FAQ）：
   ```markdown
   开始任何非trivial任务之前，先用2-3个问题确认需求范围和验收标准，
   得到我的回答后再开干。
   ```
5. 多目录实践：在子目录放一个只属于该模块的 AGENTS.md，观察合并效果

### 六、验证与排查方法（2分钟）
1. 验证加载是否正确：
   ```bash
   codex "Summarize the current instructions."
   codex --cd services/payments "Show which instruction files are active."
   cat ~/.codex/log/codex-tui.log
   ```
2. 关键认知：每次运行重建指令链、无缓存——改完重启即生效
3. 常见问题速查：没加载（目录/空文件）、加载错（上层 override 干扰）、被截断（调 project_doc_max_bytes 或拆分）

## 本课课堂演示清单
- 三层发现的日志级演示（故意在多层级放置不同内容的 AGENTS.md）
- override 切换前后行为对比
- /init 生成的初稿 vs 手工打磨后的成品对比

## 学员动手实践任务
1. 为练习仓库产出一个完整可用的 AGENTS.md 并提交入库
2. 在子目录中放置差异化规则并验证就近覆盖生效
3. 用 `Summarize the current instructions.` 验证最终生效的完整指令链
4. 尝试配置一组 fallback 文件名让 Codex 复用已有规范文档

## 课后作业
1. 将你所在团队的真实开发规范浓缩成一份 AGENTS.md（目标 ≤200 行），请一位同事评审
2. 记录接下来一周内 Codex 因缺失某条规则而犯的错，逐步补充进文件
3. 阅读《OpenAI Codex 从入门到精通》§05 全章

## 教学准备清单
- [ ] 准备一个有多层目录的开源仓库用于发现机制演示
- [ ] 打印「该写/不该写」对照表作为课堂发材料
- [ ] 准备一份反例 AGENTS.md（长而全的失败案例）供批判性讲解

## 参考资源
- 教材：§05 AGENTS.md；附录A 中 AGENTS.md 基本语法模板
- 扩展视野：SKILL.md 已成跨 agent 事实标准（Codex/Claude Code/Cursor/Gemini CLI 共用格式）

---

*最后更新：2026-08-26*
