---
title: Spec-Driven Development（规格驱动开发）
created: 2026-04-14
updated: 2026-04-14
tags: [概念, AI辅助开发, 方法论, Spec-Kit]
sources: [spec-kit-cli培训文档.md]
type: concept
---

# Spec-Driven Development（规格驱动开发）

## 定义

Spec-Driven Development（SDD，规格驱动开发）是一种软件开发方法论，核心理念是**将规格说明书从传统的文档角色提升为可执行的蓝图**。规格说明书不再是编码的参考资料，而是直接驱动代码生成的源头。

> 来源：[[sources/spec-kit-cli培训文档|Spec Kit CLI 培训文档]]

## 核心理念

### 传统模式 vs SDD

| 方面 | 传统开发 | Spec-Driven Development |
|------|----------|------------------------|
| 规格说明书 | 临时脚手架，编码后丢弃 | 可执行蓝图，持续维护 |
| 关注点 | How（怎么做） | What & Why（做什么、为什么） |
| 代码生成 | 人工编写 | AI 自动转换 |
| 沟通成本 | 高（规格与实现脱节） | 低（规格即实现） |

### 三个支柱

1. **Focus on What** — 定义构建目标和原因，而非技术细节
2. **AI-Powered** — 利用 AI 代理自动将规格转换为代码
3. **Faster Delivery** — 消除规格与实现之间的鸿沟

## 工作流程

SDD 定义了一个标准化的七阶段流水线：

```mermaid
flowchart TD
    A[/constitution<br>建立项目原则] --> B[/specify<br>创建功能规格]
    B --> C{需要澄清？}
    C -->|是| D[/clarify<br>澄清需求]
    D --> E[/plan<br>技术实现计划]
    C -->|否| E
    E --> F[/tasks<br>任务拆分]
    F --> G{需要验证？}
    G -->|是| H[/analyze<br>交叉验证]
    H --> I[/implement<br>执行实现]
    G -->|否| I
```

- **必须阶段**：/specify → /plan → /tasks → /implement
- **可选阶段**：/clarify、/analyze
- **仅一次**：/constitution（项目初始化时）

## 实际工具

SDD 方法论通过 [[entities/spec-kit-cli|Spec Kit CLI（Specify）]] 工具落地，结合 [[entities/github-copilot|GitHub Copilot]] 在 [[entities/vscode|VS Code]] 中使用。

## 相关页面

- [[entities/spec-kit-cli|Spec Kit CLI]]
- [[concepts/copilot-skills|Copilot Skills]]
- [[sources/spec-kit-cli培训文档|Spec Kit CLI 培训文档]]
