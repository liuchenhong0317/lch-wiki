---
title: 如何创建 LLM Wiki 知识库
created: 2026-04-14
updated: 2026-04-28
tags: [指南, Wiki, LLM, 操作流程]
sources: [LLM-Wiki培训手册.md]
type: topic
---

# 如何创建 LLM Wiki 知识库

本文基于实际搭建 AI 编程培训 Wiki 的完整过程，提供一份可直接复用的操作指南。

> 来源：[[sources/LLM-Wiki培训手册|LLM Wiki 培训手册]]

---

## 一、前置准备

| 准备项 | 说明 |
|--------|------|
| VS Code | 编辑器 + Copilot Chat（`Ctrl+Shift+I`） |
| GitHub Copilot 订阅 | Agent 模式，用于驱动 Wiki 维护 |
| Obsidian（推荐） | 打开 `wiki/` 目录，实时浏览双链和图谱 |
| Git（可选） | 版本控制，追踪 Wiki 演变历史 |

---

## 二、初始化 Wiki（5 分钟）

### Step 1：准备 AGENT.md

在项目根目录放置 `AGENT.md` 文件。这是 LLM Wiki 的方案说明文档，描述了 Wiki 的核心理念、架构设计和操作模式。可以从 [LLM Wiki 模板](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 获取，也可以自行编写。

```
my-wiki/
└── AGENT.md    # 方案说明 — 告诉 AI 什么是 LLM Wiki
```

### Step 2：让 AI 搭建整个 Wiki

在 Copilot Chat 中直接说：

```
按照 AGENT.md 中的方案帮我搭建 LLM Wiki
```

AI 会询问你几个关键问题（也可以在指令中直接说明）：

| 问题 | 示例回答 | 说明 |
|------|----------|------|
| Wiki 主题/领域 | AI 编程培训 | 决定标签体系和实体类型 |
| 内容语言 | 中文 | 决定页面语言 |
| 预期规模 | 小型 (<50 源文件) | 决定是否需要搜索工具 |

AI 随后会自动完成以下所有工作：

1. **创建目录结构**：`raw/`、`raw/assets/`、`wiki/` 及所有子目录
2. **编写 Schema 配置**：`.github/copilot-instructions.md`（核心！定义了角色、格式、流程、原则）
3. **创建初始页面**：`wiki/index.md`、`wiki/log.md`、`wiki/overview.md`

最终生成的目录结构：

```
my-wiki/
├── AGENT.md                          # 方案说明（只读参考）
├── .github/
│   └── copilot-instructions.md       # Schema 配置（AI 自动生成）
├── raw/                              # 原始源文件（只读区）
│   └── assets/                       # 图片与附件
└── wiki/                             # LLM 生成的 Wiki 页面
    ├── index.md                      # 内容索引
    ├── log.md                        # 操作日志
    ├── overview.md                   # 全局综述
    ├── concepts/                     # 概念页
    ├── entities/                     # 实体页（产品、工具、系统）
    ├── sources/                      # 源文档摘要页
    └── topics/                       # 专题分析页
```

### Schema 配置说明

`.github/copilot-instructions.md` 是 AI 自动生成的核心配置，包含：

1. **角色定义** — 告诉 LLM 它是知识库维护助手
2. **目录结构** — 每个文件夹的用途
3. **页面格式** — YAML frontmatter 规范、双链引用规范
4. **操作流程** — 摄入、查询、维护三大流程的具体步骤
5. **领域约定** — 根据你的主题定制的标签和实体类型
6. **重要原则** — raw 只读、增量更新、交叉引用、溯源

> 💡 Schema 生成后可根据需要手动调整。随着使用深入，你和 LLM 可以共同迭代优化这份配置。

---

## 三、日常使用

### 摄入新文件

```
1. 将源文件复制到 raw/ 目录
2. 在 Copilot Chat 中说：
   "请摄入 raw/新文件.md"
3. LLM 自动：创建摘要页 → 更新概念/实体页 → 更新索引和日志
4. 在 Obsidian 中验证图谱
```

### 查询知识

```
直接在 Copilot Chat 中提问：
"Spec-Driven Development 的核心流程是什么？"

LLM 会先读 index.md 定位页面，再综合回答。
```

### 维护健康度

```
在 Copilot Chat 中说：
"请 lint 一下 Wiki"

LLM 会检查：矛盾、孤立页、缺失引用、frontmatter 完整性。
```

---

## 四、实际搭建记录

以下是本次 AI 编程培训 Wiki 搭建的实际操作序列：

| 步骤 | 操作 | 执行者 |
|------|------|--------|
| 1 | 在项目根目录放置 `AGENT.md` | 人 |
| 2 | 在 Chat 中说"按照 AGENT.md 的方案帮我搭建 LLM Wiki" | 人 |
| 3 | AI 询问：主题、语言、预期规模 | AI |
| 4 | 回答：AI 编程培训、中文、小型 | 人 |
| 5 | AI 创建目录结构（raw/、wiki/ 及所有子目录） | AI |
| 6 | AI 编写 `.github/copilot-instructions.md` Schema | AI |
| 7 | AI 创建 `index.md`、`log.md`、`overview.md` | AI |
| 8 | 放入 2 个源文件到 raw/ | 人 |
| 9 | 在 Chat 中说"请摄入 raw 目录下的文件" | 人 |
| 10 | AI 自动生成 7 个页面（2 摘要 + 2 概念 + 3 实体） | AI |
| 11 | AI 更新 index.md、overview.md、log.md | AI |

**最终产出：** 10 个 Wiki 页面，所有页面通过 `[[双链]]` 互相关联。

---

## 五、适配你自己的领域

只需修改两处即可复用到任何领域：

### 1. Schema 中的领域约定

将标签和实体类型替换为你的领域：

```markdown
## 领域约定

### 常见分类标签
- `你的标签1`, `你的标签2`, ...

### 实体类型
- **产品/系统**：...
- **标准/规范**：...
- **概念**：...
```

### 2. overview.md 中的知识库范围

```markdown
## 知识库范围
- **领域 A**：...
- **领域 B**：...
```

**可参考的领域示例：**

| 领域 | 标签举例 | 实体类型举例 |
|------|----------|-------------|
| MOM 培训 | MOM, MES, ISA-95, 批次管理 | 和利时产品, 工业标准 |
| 前端开发 | React, TypeScript, 性能优化 | 框架, 库, 工具链 |
| 个人读书 | 文学, 心理学, 经济学 | 作者, 书籍, 理论 |
| 竞品分析 | SaaS, 定价, 功能对比 | 竞品公司, 产品, 功能模块 |

---

## 六、核心理念

> Wiki 是一个 **持续复利的知识资产**。

- 你负责：**选择源文件、提出问题、做判断**
- LLM 负责：**摘要、交叉引用、索引维护、一致性检查**
- 每次摄入和查询都让 Wiki 更丰富，知识不会随聊天记录消失
