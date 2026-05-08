<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增37行/修改0行/删除0行; 总行数37行
 @AI-LastModified: 2026-04-27 11:10:06
-->

---
title: Superpowers 技能链实操跟练手册（源文档摘要）
created: 2026-04-27
updated: 2026-04-27
tags: [源文档, Superpowers, 实操, 跟练]
sources: [Superpowers技能链实操跟练手册.md]
type: source
---

# Superpowers 技能链实操跟练手册（源文档摘要）

## 文档定位

该文档通过“登录失败锁定”完整案例，按 9 幕演示 Superpowers 技能链在真实开发中的触发方式、可见行为和质量收益。

> 来源：`raw/Superpowers技能链实操跟练手册.md`

## 关键信息

- **教学目标**：在 20-30 分钟场景中掌握 11 个关键技能的触发与协同。
- **演示方式**：从模糊需求出发，依次触发需求澄清、计划编写、隔离开发、TDD、系统调试、验证、评审和收尾流程。
- **典型价值点**：
  - 防止“直接写代码”导致的返工
  - 通过 RED→GREEN 循环降低功能偏差
  - 通过根因调查避免猜测式修复
  - 通过命令验证避免“口头完成”

## 核心演示链路

1. `using-superpowers`：先判断适用技能，不直接编码
2. `brainstorming`：澄清需求边界并产出 Spec
3. `writing-plans`：将 Spec 拆解为可执行 Task
4. `using-git-worktrees`：创建隔离环境并跑基线
5. `executing-plans` + `test-driven-development`：按 RED→GREEN 执行
6. `systematic-debugging`：四阶段定位并修复时区问题
7. `verification-before-completion`：先跑命令再声明完成
8. `requesting-code-review` + `receiving-code-review`：闭环审查
9. `finishing-a-development-branch`：标准化收尾与清理

## 与本 Wiki 的关联

- 概念关联：[[concepts/superpowers-skills|Superpowers 技能体系]]、[[concepts/copilot-skills|Copilot Skills]]
- 实体关联：[[entities/github-copilot|GitHub Copilot]]、[[entities/vscode|VS Code]]

## 可沉淀的培训要点

- 可将 9 幕脚本直接改造成课堂演示 SOP。
- 可把“技能触发检查清单”作为学员实操评分标准。
- 可将“Bug 根因调查”与“完成前验证”作为强制验收门禁。
