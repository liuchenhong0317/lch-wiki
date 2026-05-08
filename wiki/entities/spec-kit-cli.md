---
title: Spec Kit CLI（Specify）
created: 2026-04-14
updated: 2026-04-14
tags: [工具, Spec-Kit, CLI, AI辅助开发]
sources: [spec-kit-cli培训文档.md]
type: entity
---

# Spec Kit CLI（Specify）

## 概述

Spec Kit（又称 Specify CLI）是一个 AI 驱动的命令行工具，用于实践 [[concepts/spec-driven-development|Spec-Driven Development]] 方法论。它通过结构化的 Slash 命令将软件开发流程标准化为可重复的工作流。

> 来源：[[sources/spec-kit-cli培训文档|Spec Kit CLI 培训文档]]

## 基本信息

| 属性 | 值 |
|------|-----|
| 类型 | 命令行工具 |
| 语言 | Python |
| 协议 | MIT 开源 |
| 前置要求 | Python 3.8+, Git 2.20+, uv |
| AI 支持 | 11+ 种（Copilot, Claude, Gemini, Cursor 等） |

## 核心命令

### 项目初始化

```bash
specify init <project-name> --ai copilot    # 创建新项目
specify init . --ai copilot                  # 在现有项目中初始化
specify init <name> --ai copilot --no-git    # 跳过 Git 初始化
```

### Slash 命令（在 Copilot Chat 中使用）

| 命令 | 用途 | 生成文件 |
|------|------|----------|
| `/speckit.constitution` | 建立项目原则 | `.specify/memory/constitution.md` |
| `/speckit.specify` | 定义功能需求 | `.specify/specs/NNN-feature/spec.md` |
| `/speckit.clarify` | 澄清不明确需求 | 更新 spec.md |
| `/speckit.plan` | 制定技术实现方案 | `plan.md`, `data-model.md`, `research.md` |
| `/speckit.tasks` | 生成任务列表 | `tasks.md` |
| `/speckit.analyze` | 跨文档一致性分析 | 分析报告 |
| `/speckit.implement` | 执行实现生成代码 | 项目源代码 |

## 项目结构

```
project/
├── .github/
│   ├── agents/           # AI Agent 配置（9个 agent.md 文件）
│   └── prompts/          # Prompt 模板（9个 prompt.md 文件）
└── .specify/
    ├── integrations/     # 外部工具集成
    ├── memory/           # 项目记忆与原则
    ├── scripts/          # 自动化脚本（PowerShell）
    └── templates/        # 文档模板
```

## 使用场景

- **快速原型**：简化流程，快速验证核心功能
- **企业级应用**：完整流程，含严格质量和安全原则
- **现有项目扩展**：在已有代码库中初始化 Spec Kit

## 相关页面

- [[concepts/spec-driven-development|Spec-Driven Development]]
- [[entities/github-copilot|GitHub Copilot]]
- [[entities/vscode|VS Code]]
