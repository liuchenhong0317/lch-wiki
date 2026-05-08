<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增42行/修改0行/删除0行; 总行数42行
 @AI-LastModified: 2026-04-27 11:10:55
-->

---
title: GitHub Copilot
created: 2026-04-14
updated: 2026-04-27
tags: [工具, GitHub Copilot, AI辅助开发]
sources: [spec-kit-cli培训文档.md, vscode-copilot-skills-training-9568667871.md, Superpowers技能培训课堂讲义.md, Superpowers技能链实操跟练手册.md]
type: entity
---

# GitHub Copilot

## 概述

GitHub Copilot 是 GitHub 提供的 AI 编程助手，集成在 [[entities/vscode|VS Code]] 中。在培训体系中，它是 [[entities/spec-kit-cli|Spec Kit CLI]] 的默认 AI 代理，也是 [[concepts/copilot-skills|Skills]] 开放标准的主要载体。

> 来源：[[sources/spec-kit-cli培训文档|Spec Kit CLI 培训文档]]、[[sources/vscode-copilot-skills-training|VS Code Copilot Skills 培训]]

## 在培训中的角色

### 1. Spec Kit 的执行引擎

Copilot Chat 是 Spec Kit Slash 命令的运行环境：
- 在 Chat 界面中输入 `/speckit.xxx` 命令
- Copilot 读取 `.github/agents/` 和 `.github/prompts/` 中的配置
- 执行对应的 SDD 工作流阶段

### 2. Skills 的宿主平台

- 通过 `chat.useAgentSkills` 设置启用 Skills 功能（预览）
- 自动语义匹配触发相关 Skills
- 支持 `/create-skill` 命令创建新技能

### 3. 交互方式

| 模式 | 说明 | 示例 |
|------|------|------|
| 指令模式 | 使用 Slash 命令 | `/speckit.plan 使用 React` |
| 问答模式 | 自由提问 | "解释这个用户故事的映射" |
| 迭代模式 | 根据反馈调整 | "增加 Redis 缓存层" |
| 验证模式 | 检查确认 | "审查任务列表是否有遗漏" |

### 4. Superpowers 技能链训练承载平台

在 Superpowers 相关培训中，Copilot 通常作为代理执行入口，按技能链完成需求澄清、计划编写、实现、调试、验证和审查的全流程演练。

## 打开方式（VS Code）

- 快捷键：`Ctrl+Shift+I`（Windows/Linux）
- 侧边栏：点击活动栏的 Copilot 图标
- 命令面板：`Ctrl+Shift+P` → "Copilot Chat"

## 相关页面

- [[entities/vscode|VS Code]]
- [[entities/spec-kit-cli|Spec Kit CLI]]
- [[concepts/copilot-skills|Copilot Skills]]
- [[concepts/superpowers-skills|Superpowers 技能体系]]
- [[entities/superpowers|Superpowers]]
- [[concepts/spec-driven-development|Spec-Driven Development]]
