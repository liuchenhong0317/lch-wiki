---
title: Spec Kit CLI 培训文档摘要
created: 2026-04-14
updated: 2026-04-14
tags: [培训, AI辅助开发, Spec-Kit, CLI, GitHub Copilot]
sources: [spec-kit-cli培训文档.md]
type: source
---

# Spec Kit CLI 培训文档摘要

> 来源：`raw/spec-kit-cli培训文档.md`

## 文档概述

本文档是 Spec Kit（Specify CLI）的完整培训材料，介绍 [[concepts/spec-driven-development|Spec-Driven Development（规格驱动开发）]]方法论及其工具链的使用。培训人未注明，适用于使用 [[entities/vscode|VSCode]] + [[entities/github-copilot|GitHub Copilot]] 的开发者。

## 核心内容

### 1. Spec-Driven Development 理念

- 规格说明书不再只是文档，而是**可执行的蓝图**，能直接生成工作代码
- 核心翻转：关注 **What & Why**（构建什么、为什么），而非 How（怎么做）
- AI 驱动：利用 AI 代理自动将规格转换为实现

### 2. Specify CLI 工具

- 通过 `specify init` 命令初始化项目
- 支持 11+ 种 AI 编程助手（Copilot、Claude、Gemini、Cursor 等）
- 项目结构包含：
  - `.github/agents/` — AI Agent 配置文件
  - `.github/prompts/` — Prompt 模板文件
  - `.specify/memory/` — 项目记忆与原则
  - `.specify/scripts/` — 自动化脚本
  - `.specify/templates/` — 文档模板

### 3. 开发工作流（七阶段）

| 阶段 | Slash 命令 | 必要性 | 说明 |
|------|-----------|--------|------|
| 建立原则 | `/speckit.constitution` | 仅一次 | 建立项目指导原则和开发标准 |
| 创建规格 | `/speckit.specify` | 必须 | 定义功能需求（What & Why） |
| 澄清需求 | `/speckit.clarify` | 可选 | 结构化提问，澄清不明确部分 |
| 技术计划 | `/speckit.plan` | 必须 | 选择技术栈，制定实现方案 |
| 任务拆分 | `/speckit.tasks` | 必须 | 分解为可执行任务列表 |
| 交叉验证 | `/speckit.analyze` | 可选 | 跨文档一致性和覆盖率分析 |
| 执行实现 | `/speckit.implement` | 必须 | 根据计划生成工作代码 |

### 4. 使用场景

- **快速原型开发**：简化流程，跳过澄清阶段
- **企业级应用**：完整流程，含严格原则（覆盖率、安全、GDPR）
- **现有项目扩展**：`specify init .` 在已有项目中初始化

### 5. 前置要求

- Python 3.8+、Git 2.20+、uv 包管理器（必需）
- VSCode、GitHub Copilot 订阅（推荐）

## 关键洞察

- Spec Kit 将传统的"先写代码再补文档"模式翻转为"先定义规格再自动生成代码"
- 通过结构化的 Slash 命令流水线，将软件开发标准化为可重复的工作流
- 声称可提升开发效率 3-10 倍

## 相关页面

- [[concepts/spec-driven-development|Spec-Driven Development]]
- [[entities/spec-kit-cli|Spec Kit CLI]]
- [[entities/github-copilot|GitHub Copilot]]
- [[sources/vscode-copilot-skills-training|VS Code Copilot Skills 培训]]
