<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增22行/修改2行/删除0行; 总行数67行
 @AI-LastModified: 2026-04-28 14:36:49
-->

---
title: 操作日志
created: 2026-04-14
updated: 2026-04-28
tags: [日志]
sources: []
type: overview
---

# 操作日志

按时间倒序记录所有 Wiki 操作。

---

## [2026-04-28] 摄入 | LLM-Wiki 培训手册

摄入 `raw/LLM-Wiki培训手册.md`，新增源文档摘要并更新索引与综述统计。

**源文件：**
- `raw/LLM-Wiki培训手册.md` — LLM Wiki 从零搭建与日常运营培训手册

**新建页面：**
- 源文档摘要：[[sources/LLM-Wiki培训手册]]

**更新页面：**
- [[topics/how-to-create-wiki]]、[[index]]、[[overview]]、[[log]]

---

## [2026-04-27] 创建 | Superpowers 技能链实操指南

基于已摄入的两份 Superpowers 培训文档，创建专题页 [[topics/superpowers-skillchain-practice-guide]]，沉淀课堂可执行 SOP、验收清单与落地建议。

- 影响页面：[[topics/superpowers-skillchain-practice-guide]], [[index]], [[log]]

---

## [2026-04-27] 摄入 | Superpowers 相关培训文档（2 份）

摄入 `raw/` 目录中新增的 2 份 Superpowers 培训文档，完成源摘要、概念与实体扩展，并更新索引和综述。

**源文件：**
- `raw/Superpowers技能培训课堂讲义.md` — Superpowers 13 技能体系、触发规则与三大铁律
- `raw/Superpowers技能链实操跟练手册.md` — 技能链 9 幕演示脚本与实操检查清单

**新建页面：**
- 源文档摘要：[[sources/Superpowers技能培训课堂讲义]]、[[sources/Superpowers技能链实操跟练手册]]
- 概念页：[[concepts/superpowers-skills]]
- 实体页：[[entities/superpowers]]

**更新页面：**
- [[concepts/copilot-skills]]、[[entities/github-copilot]]、[[entities/vscode]]
- [[index]]、[[overview]]、[[log]]

---

## [2026-04-24] 更新 | 知识库主题从 MOM 培训改为 AI 编程培训

将整个知识库的主题定位从"MOM（制造运营管理）培训"修改为"AI 编程（AI-Assisted Programming）培训"。更新了 Schema 配置中的领域约定（标签和实体类型）、overview 综述页、index 索引页等。

- 影响页面：[[overview]], [[index]], [[log]], [[topics/how-to-create-wiki]]

---

## [2026-04-14] 创建 | LLM Wiki 创建指南

基于当前会话的实际搭建过程，总结出完整的 LLM Wiki 创建指南，含目录结构、Schema 模板、日常使用流程和领域适配方法。

- 影响页面：[[topics/how-to-create-wiki]], [[index]]

---

## [2026-04-14] 创建 | 摄入操作指南

创建专题页 [[topics/how-to-ingest]]，说明新增源文件时的摄入操作流程。

- 影响页面：[[topics/how-to-ingest]], [[index]]

---

## [2026-04-14] 摄入 | Spec Kit CLI 培训文档 & VS Code Copilot Skills 培训指南

批量摄入 `raw/` 目录下 2 个源文件，生成 7 个 Wiki 页面。

**源文件：**
- `raw/spec-kit-cli培训文档.md` — Spec-Driven Development 方法论与 Specify CLI 工具培训
- `raw/vscode-copilot-skills-training-9568667871.md` — VS Code + GitHub Copilot + Skills 完整培训指南

**新建页面：**
- 源文档摘要：[[sources/spec-kit-cli培训文档]]、[[sources/vscode-copilot-skills-training]]
- 概念页：[[concepts/spec-driven-development]]、[[concepts/copilot-skills]]
- 实体页：[[entities/spec-kit-cli]]、[[entities/github-copilot]]、[[entities/vscode]]

**更新页面：**
- [[index]]、[[overview]]、[[log]]

---

## [2026-04-14] 创建 | Wiki 初始化

搭建 MOM 培训 Wiki 基础结构：

- 创建目录结构：`raw/`, `raw/assets/`, `wiki/`, `wiki/concepts/`, `wiki/entities/`, `wiki/sources/`, `wiki/topics/`
- 创建 Schema 配置：`.github/copilot-instructions.md`
- 创建初始页面：`wiki/index.md`, `wiki/log.md`, `wiki/overview.md`

- 影响页面：[[index]], [[overview]], [[log]]

