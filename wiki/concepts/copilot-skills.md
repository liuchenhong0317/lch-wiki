<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增61行/修改0行/删除0行; 总行数61行
 @AI-LastModified: 2026-04-27 11:10:47
-->

---
title: Copilot Skills（AI 技能包）
created: 2026-04-14
updated: 2026-04-27
tags: [概念, GitHub Copilot, Skills, AI辅助开发]
sources: [vscode-copilot-skills-training-9568667871.md, Superpowers技能培训课堂讲义.md, Superpowers技能链实操跟练手册.md]
type: concept
---

# Copilot Skills（AI 技能包）

## 定义

Skills 是包含指令、脚本和资源的文件夹，AI 代理在执行相关任务时自动加载。本质上是给 AI 智能体配备的**专业技能包**，让通用助手变成领域专家。

Skills 是一个**开放标准**，支持多种 AI 编码代理：[[entities/github-copilot|GitHub Copilot]]、Claude Code 等。

> 来源：[[sources/vscode-copilot-skills-training|VS Code Copilot Skills 培训]]

## 核心机制

### 渐进式披露（Progressive Disclosure）

Skills 采用三级加载机制，确保高效利用上下文窗口：

| 级别 | 加载内容 | 触发时机 | Token 消耗 |
|------|----------|----------|------------|
| 第 1 级 | name + description | 始终加载 | ~30-50 |
| 第 2 级 | SKILL.md 完整内容 | 请求匹配时 | 按需 |
| 第 3 级 | 脚本、模板、示例 | 需要引用时 | 用完释放 |

### 自动触发

Skills 通过语义匹配自动激活，无需手动选择。Copilot 分析用户请求中的关键词，匹配 Skill 的 `description` 字段。

### Skill 结构

```
skill-name/
├── SKILL.md        # 必需：YAML frontmatter + 指令正文
├── scripts/        # 可选：可执行脚本
└── references/     # 可选：文档、模板、示例
```

### SKILL.md 格式

```yaml
---
name: skill-name          # 唯一标识符，≤64字符
description: 功能描述...    # 功能+使用场景，≤1024字符
---

# 技能标题
（详细指令、流程、示例）
```

## 存储位置

| 类型 | 路径 | 特点 |
|------|------|------|
| 项目级 | `.github/skills/` | 随项目版本控制，推荐 |
| 个人级 | `~/.copilot/skills/` | 跨项目可用 |

## 创建方法

1. **`/create-skill` 命令**（推荐）：从对话中自动提取可复用知识
2. **手动创建**：完全自定义目录和 SKILL.md

## Description 编写公式

> **[功能描述] + [具体能力] + [使用场景] + [触发关键词]**

好的 description 是 Skill 正确触发的关键。过于宽泛会导致过度触发，过于狭窄会导致无法匹配。

## 与 Superpowers 的关系

[[concepts/superpowers-skills|Superpowers 技能体系]]可以看作基于 Skills 机制构建的“流程化技能集”实践：

- Skills 负责“能力打包与触发”
- Superpowers 进一步定义“技能调用顺序、门禁规则和质量铁律”

这种组合将“可调用能力”升级为“可治理流程”。

## 相关页面

- [[entities/github-copilot|GitHub Copilot]]
- [[entities/vscode|VS Code]]
- [[concepts/spec-driven-development|Spec-Driven Development]]
- [[concepts/superpowers-skills|Superpowers 技能体系]]
- [[sources/vscode-copilot-skills-training|VS Code Copilot Skills 培训]]
