<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增33行/修改0行/删除0行; 总行数33行
 @AI-LastModified: 2026-04-27 11:11:02
-->

---
title: VS Code
created: 2026-04-14
updated: 2026-04-27
tags: [工具, VSCode, IDE]
sources: [spec-kit-cli培训文档.md, vscode-copilot-skills-training-9568667871.md, Superpowers技能培训课堂讲义.md, Superpowers技能链实操跟练手册.md]
type: entity
---

# VS Code

## 概述

Visual Studio Code（VS Code）是微软开发的代码编辑器，是本培训体系中 AI 辅助开发的核心工作环境。[[entities/github-copilot|GitHub Copilot]] 和 [[concepts/copilot-skills|Skills]] 均以 VS Code 扩展形式运行。

> 来源：[[sources/spec-kit-cli培训文档|Spec Kit CLI 培训文档]]、[[sources/vscode-copilot-skills-training|VS Code Copilot Skills 培训]]

## 在培训中的角色

- **Spec Kit 开发环境**：通过 Copilot Chat 执行 [[entities/spec-kit-cli|Spec Kit]] Slash 命令
- **Skills 宿主**：加载和管理 [[concepts/copilot-skills|Skills]] 技能包
- **配置中心**：通过 `settings.json` 配置 AI 功能

## 关键配置

```json
{
    "chat.useAgentSkills": true    // 启用 Skills 预览功能
}
```

## Skills 存储路径

VS Code 读取以下路径的 Skills：
- 项目级：`.github/skills/`
- 个人级：`~/.copilot/skills/`

在 Superpowers 场景下，常见全局技能目录为 `~/.agents/skills/`。

## 相关页面

- [[entities/github-copilot|GitHub Copilot]]
- [[entities/spec-kit-cli|Spec Kit CLI]]
- [[concepts/copilot-skills|Copilot Skills]]
- [[concepts/superpowers-skills|Superpowers 技能体系]]
- [[entities/superpowers|Superpowers]]
