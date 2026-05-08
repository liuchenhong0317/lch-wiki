<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增28行/修改0行/删除0行; 总行数28行
 @AI-LastModified: 2026-04-27 11:09:51
-->

---
title: Superpowers 技能培训课堂讲义（源文档摘要）
created: 2026-04-27
updated: 2026-04-27
tags: [源文档, Superpowers, 技能体系, 培训]
sources: [Superpowers技能培训课堂讲义.md]
type: source
---

# Superpowers 技能培训课堂讲义（源文档摘要）

## 文档定位

该文档系统介绍了 `obra/superpowers` 技能套件的定位、13 个核心技能、触发条件、执行顺序以及三条铁律，属于 AI 编程代理流程方法论的培训材料。

> 来源：`raw/Superpowers技能培训课堂讲义.md`

## 关键信息

- **Superpowers 定义**：面向 AI 编程代理的可复用流程技能集合，强调在特定场景下使用经过验证的操作规范。
- **技能规模**：共 13 个技能，覆盖从需求梳理到开发收尾的完整链路。
- **核心流程链路**：`using-superpowers` 调度 → `brainstorming` → `writing-plans` → `using-git-worktrees` → `executing-plans`/`subagent-driven-development` → `verification-before-completion` → code review → 分支收尾。
- **三大铁律**：
  - 没有失败测试，不写生产代码（TDD）
  - 不找到根因，不提修复方案（系统化调试）
  - 没有验证证据，不得声称完成（完成前验证）

## 与本 Wiki 的关联

- 方法论关联：[[concepts/superpowers-skills|Superpowers 技能体系]]、[[concepts/spec-driven-development|Spec-Driven Development]]
- 平台关联：[[entities/github-copilot|GitHub Copilot]]、[[entities/vscode|VS Code]]
- 标准关联：[[concepts/copilot-skills|Copilot Skills]]

## 可沉淀的培训要点

- 将“技能调用顺序”和“触发条件”纳入实操检查清单。
- 在培训中用真实失败案例演示三条铁律，强化流程纪律。
- 对复杂任务优先采用“计划 + 子代理 + 双阶段审查”的执行方式。
