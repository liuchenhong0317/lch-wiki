---
title: VS Code Copilot Skills 培训指南摘要
created: 2026-04-14
updated: 2026-04-14
tags: [培训, GitHub Copilot, Skills, VSCode, AI辅助开发]
sources: [vscode-copilot-skills-training-9568667871.md]
type: source
---

# VS Code Copilot Skills 培训指南摘要

> 来源：`raw/vscode-copilot-skills-training-9568667871.md`

## 文档概述

培训人：刘晨虹。本文档是 [[entities/vscode|VS Code]] + [[entities/github-copilot|GitHub Copilot]] + [[concepts/copilot-skills|Skills]] 的完整培训指南，从入门到精通，版本 1.0（2026年4月）。

## 核心内容

### 1. Skills 定义

Skills 是包含指令、脚本和资源的文件夹，AI 代理可在相关任务时自动加载。本质上是给 AI 智能体配备的"专业技能包"，让通用助手变成领域专家。Skills 是**开放标准**，可跨多种 AI 代理使用（GitHub Copilot、Claude Code 等）。

### 2. 存储位置

| 类型 | 路径 | 说明 |
|------|------|------|
| 项目级（推荐） | `.github/skills/` | 随项目版本控制 |
| 项目级（兼容） | `.claude/skills/` | 向后兼容 |
| 个人级 | `~/.copilot/skills/` | 跨项目可用 |
| 个人级（兼容） | `~/.claude/skills/` | 向后兼容 |

### 3. Skill 结构

```
skill-name/
├── SKILL.md        # 必需：指令文件（YAML frontmatter + 详细指令）
├── scripts/        # 可选：可执行脚本
└── references/     # 可选：文档、模板、示例
```

### 4. 渐进式披露（Progressive Disclosure）三级加载

| 级别 | 内容 | 何时加载 | Token 占用 |
|------|------|----------|------------|
| 第 1 级 | 元数据（name + description） | 启动时始终加载 | ~30-50 tokens |
| 第 2 级 | 核心指令（SKILL.md 主体） | 请求匹配时 | 按需加载 |
| 第 3 级 | 资源文件 | 仅在需要时引用 | 用完即释放 |

### 5. 创建 Skills 的两种方法

1. **`/create-skill` 命令**（推荐）：从对话历史中自动提取可复用知识，零配置
2. **手动创建**：完全自定义 SKILL.md 文件和目录结构

### 6. SKILL.md 格式

- **Header**（YAML frontmatter）：`name`（标识符，≤64字符）+ `description`（功能+使用场景，≤1024字符）
- **Body**：指令、流程、示例、资源引用（支持相对路径）

### 7. Description 编写公式

> **[功能描述] + [具体能力] + [使用场景] + [触发关键词]**

### 8. 核心优势

- 专业化能力、减少重复、可组合性、高效加载、多代理支持

### 9. 常见问题

- 无法触发 → description 不够具体，需添加触发关键词
- 过度触发 → description 过于宽泛，需精简
- 资源引用失败 → 使用相对路径，检查文件存在性

### 10. 安全考虑

- 审查共享 Skills 中的所有脚本
- VS Code 终端工具提供脚本执行控制
- 可配置允许列表

## 关键洞察

- Skills 采用渐进式披露机制，安装大量 Skills 也不会影响性能
- `/create-skill` 是从解决问题的经验中沉淀组织资产的高效方式
- Skills 作为开放标准，避免了对单一 AI 代理的绑定

## 相关页面

- [[concepts/copilot-skills|Copilot Skills]]
- [[concepts/spec-driven-development|Spec-Driven Development]]
- [[entities/github-copilot|GitHub Copilot]]
- [[entities/vscode|VS Code]]
- [[sources/spec-kit-cli培训文档|Spec Kit CLI 培训文档]]
