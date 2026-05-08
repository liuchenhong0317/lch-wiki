<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增33行/修改0行/删除0行; 总行数33行
 @AI-LastModified: 2026-04-27 11:10:24
-->

---
title: Superpowers 技能体系
created: 2026-04-27
updated: 2026-04-27
tags: [概念, Superpowers, Agent模式, 流程规范]
sources: [Superpowers技能培训课堂讲义.md, Superpowers技能链实操跟练手册.md]
type: concept
---

# Superpowers 技能体系

## 定义

Superpowers 是一套面向 AI 编程代理的流程化技能体系，目标是用可复用、可验证的操作规范替代“模型自由发挥”，提升开发过程的稳定性与可审计性。

> 来源：[[sources/Superpowers技能培训课堂讲义|Superpowers 技能培训课堂讲义]]、[[sources/Superpowers技能链实操跟练手册|Superpowers 技能链实操跟练手册]]

## 核心特征

- **强流程约束**：先判断是否命中技能，再执行任务。
- **阶段化执行**：需求澄清、计划编写、实现、调试、验证、评审、收尾形成闭环。
- **证据驱动完成**：声明完成前必须有新鲜命令输出作为验证证据。
- **可并行扩展**：独立任务可分派子代理并行执行并做合并校验。

## 技能分层

| 分层 | 代表技能 | 作用 |
|------|----------|------|
| 入口调度层 | `using-superpowers` | 判定和调度后续技能 |
| 需求与计划层 | `brainstorming`, `writing-plans` | 将模糊需求转为可执行计划 |
| 执行层 | `executing-plans`, `subagent-driven-development`, `test-driven-development` | 按任务实现并验证 |
| 质量保障层 | `systematic-debugging`, `verification-before-completion` | 保障修复质量与完成真实性 |
| 审查与收尾层 | `requesting-code-review`, `receiving-code-review`, `finishing-a-development-branch` | 闭环审查与分支治理 |

## 三条铁律

1. 没有失败测试，不写生产代码。
2. 不找到根因，不提修复方案。
3. 没有验证证据，不得声称完成。

## 与现有概念的关系

- 与 [[concepts/copilot-skills|Copilot Skills]]：Superpowers 是基于技能机制构建的流程技能集。
- 与 [[concepts/spec-driven-development|Spec-Driven Development]]：两者都强调先规格/计划后实现。
- 与 [[entities/github-copilot|GitHub Copilot]]、[[entities/vscode|VS Code]]：常见承载平台。
