# VS Code + GitHub Copilot + Skills 完整培训指南

> 完整培训指南 - 从入门到精通
> 培训人：刘晨虹

---

## 目录

1. [什么是 Skills？](#section-1)
   - [Skill 的存储位置](#section-1-1)
   - [Skill 的基本结构](#section-1-2)
   - [核心设计原理](#section-1-3)
2. [Skills 的核心优势](#section-2)
3. [如何使用 Skills](#section-3)
   - [启用 Skills 功能](#section-3-1)
   - [自动触发机制](#section-3-2)
   - [支持多种 AI 编码代理](#section-3-3)
   - [使用共享 Skills](#section-3-4)
4. [如何创建自定义 Skills](#section-4)
   - [方法一：使用内置 /create-skill 命令（推荐）](#section-4-1)
   - [方法二：手动创建 Skill（完全自定义）](#section-4-2)
   - [SKILL.md 文件格式详解](#section-4-3)
   - [添加辅助资源（可选）](#section-4-4)
   - [编写高质量的 Description](#section-4-5)
   - [测试和优化](#section-4-6)
5. [示例 Skills](#section-5)
   - [示例：API 文档生成 Skill](#section-5-1)
6. [最佳实践案例](#section-6)
   - [案例一：会话内容总结技能](#section-6-1)
7. [进阶技巧与常见问题](#section-7)
   - [高级技巧](#section-7-1)
   - [常见问题与解决方案](#section-7-2)
   - [学习资源](#section-7-3)
   - [安全考虑](#section-7-4)

---

## 1. 什么是 Skills？

### 核心定义

**Skills** 是包含指令、脚本和资源的文件夹，AI 代理可以在相关任务时自动加载这些内容来执行专业任务。Skills 是一个**开放标准**，可在多个 AI 代理间工作，包括 VS Code 中的 GitHub Copilot、GitHub Copilot CLI、GitHub Copilot 编码代理、Claude Code 等其他支持 Skills 标准的 AI 工具。

简单来说，Skills 是给 AI 智能体配备的"专业技能包"，让它从通用助手变成领域专家。当需要处理特定领域任务时，智能体会自动加载相应的技能包，按照标准化的工作流程、最佳实践和操作规范完成任务，确保输出的稳定性和一致性。

> ⚠️ 预览功能提醒：VS Code 中的 Skills 支持目前处于预览阶段。需要在设置中启用 `chat.useAgentSkills` 选项才能使用。

![VS Code Skills 配置界面](https://www.coze.cn/s/zU5L6cD_jt8/?width_height=1391x632)
VS Code Skills 配置界面 - 启用功能及配置技能加载路径

### 📁 Skill 的存储位置

VS Code 支持两种类型的 Skills：

#### 项目级 Skills（推荐）

存储在你的代码仓库中，与项目一起版本控制：

```
my-project/
└── .github/
    └── skills/
        ├── webapp-testing/
        │   └── SKILL.md
        └── api-documentation/
            └── SKILL.md
```

**兼容性路径（向后兼容）：** `.claude/skills/`

#### 个人级 Skills

存储在你的用户配置文件中，跨项目可用：

```
~/.copilot/skills/
├── my-personal-skill/
│   └── SKILL.md
└── another-skill/
    └── SKILL.md
```

**兼容性路径（向后兼容）：** `~/.claude/skills/`

### 📦 Skill 的基本结构

每个 Skill 都是一个独立的文件夹，包含指令、脚本和资源这三类核心内容：

```
webapp-testing/
├── SKILL.md              # 必需：指令文件（元数据 + 详细指令）
├── scripts/              # 脚本：可执行的代码文件
│   ├── setup.py
│   └── run-tests.js
└── references/           # 资源：文档、模板、示例等
    ├── test-template.md
    ├── best-practices.md
    └── examples/
        ├── login-test.js
        └── checkout-test.js
```

**核心组成：**

- **SKILL.md**：包含 Skill 的元数据（name、description）和执行指令
- **scripts/**：存放可执行的脚本文件（Python、Bash、JavaScript 等）
- **references/**：存放参考文档、模板、示例等辅助资源

### ⚡ 核心设计原理：渐进式披露（Progressive Disclosure）

Skills 采用三级加载机制，确保高效利用上下文窗口，即使安装很多 Skills 也不会影响性能：

| 级别 | 内容 | 何时加载 | Token 占用 |
|------|------|----------|------------|
| **第 1 级：技能发现** | 元数据（YAML Frontmatter）<br>`name` 和 `description` | Copilot 启动时始终加载 | 极少（~30-50 tokens） |
| **第 2 级：指令加载** | 核心指令（SKILL.md 主体）<br>详细流程、最佳实践 | 请求匹配描述时 | 按需加载 |
| **第 3 级：资源访问** | 资源文件<br>脚本、示例、文档 | 仅在需要时引用 | 用完即释放 |

---

## 2. Skills 的核心优势

### 🎯 专业化能力

为 Copilot 定制特定领域能力，无需重复提供上下文。将通用 AI 转变为测试、调试、部署等领域的专家。

### ♻️ 减少重复

一次创建，自动在所有对话中使用。不再需要每次都重新告诉 Copilot 你的工作流程和规范。

### 🧩 可组合性

组合多个 Skills 构建复杂工作流。Copilot 会智能识别任务需求，协调多个 Skills 协作完成任务。

### ⚡ 高效加载

只在需要时加载相关内容，可以安装数十个 Skills 而不会消耗额外的上下文空间。

### 🌐 支持多种 AI 编码代理

Skills 是开放标准，可在多种 AI 编码代理中通用，无需重复配置。

### 🛠️ 资源丰富

除了指令，还可以包含脚本、示例、模板等资源，为 Copilot 提供更强大的执行能力。

---

## 3. 如何使用 Skills

### ⚙️ 启用 Skills 功能

首先需要在 VS Code 中启用 Skills 预览功能：

```
// 方法 1：通过 VS Code 设置界面
1. 打开 VS Code
2. 按 Ctrl+,（或 Cmd+,）打开设置
3. 搜索 "Skills"
4. 找到 "Chat: Use Skills" 选项
5. 勾选启用

// 方法 2：通过 settings.json
{
    "chat.useAgentSkills": true
}
```

### 🎯 自动触发机制

Skills 会根据你的请求自动激活，无需手动选择。Copilot 通过语义匹配来决定何时使用哪个 Skill：

#### 触发示例：

```
用户："帮我为这个 web 应用创建 Playwright 测试"
↓ Copilot 分析请求
↓ 识别关键词："Playwright"、"测试"、"web 应用"
↓ 匹配到 webapp-testing Skill 的 description
↓ 自动加载 webapp-testing Skill
↓ 执行测试创建任务

用户："调试失败的 GitHub Actions 工作流"
↓ Copilot 分析请求
↓ 识别关键词："GitHub Actions"、"调试"、"失败"
↓ 匹配到 github-actions-debugging Skill
↓ 自动加载并执行调试流程
```

> ✅ 自动激活的优势
> - 无需记忆或手动选择 Skills
> - 基于自然语言请求智能匹配
> - 可以在 Copilot 的思考链中看到正在使用的 Skills
> - 多个 Skills 可以同时激活协同工作

### 🌐 支持多种 AI 编码代理

Skills 作为开放标准，可在多种 AI 编码代理中使用：

#### 1. VS Code Chat (GitHub Copilot)

在 VS Code 的聊天界面中，Copilot 会自动识别并加载相关 Skills。支持聊天模式和代理模式。

#### 2. GitHub Copilot CLI

在终端中使用 Copilot CLI 时，Skills 同样可用：

```bash
# 安装 Copilot CLI
npm install -g @githubnext/github-copilot-cli

# 使用时 Skills 会自动激活
gh copilot suggest "帮我运行测试并生成报告"
```

#### 3. Claude Code

Claude Code 作为支持 Skills 开放标准的 AI 编码代理，同样可以加载和使用 Skills。Skills 的开放标准特性使其能够在不同的 AI 代理间通用，无需重复配置。

### 📚 使用共享 Skills

社区提供了大量现成的 Skills 可以直接使用：

#### 官方资源仓库：

- **[github/awesome-copilot](https://github.com/github/awesome-copilot)** - 社区技能、自定义代理、指令和提示词的集合
- **[anthropics/skills](https://github.com/anthropics/skills)** - 参考技能仓库，包含丰富的示例
- **[skills.sh](https://skills.sh/)** - 开放代理技能生态系统，支持多种 AI 代理，可通过 `npx skills add <owner/repo>` 快速安装技能包，提供技能排行榜和热门推荐

#### 如何使用共享 Skills：

1. 浏览仓库中的可用 Skills
2. 将 Skill 目录复制到你的 `.github/skills/` 文件夹
3. 根据需要审查和自定义 SKILL.md 文件
4. 根据需要修改或添加资源

> ⚠️ 安全提醒：在使用共享 Skills 之前，请务必审查它们，确保符合你的要求和安全标准。VS Code 的终端工具提供了脚本执行控制，包括可配置的允许列表和对运行代码的严格控制。

---

## 4. 如何创建自定义 Skills

### 🎨 创建流程概览

1. **方法一：** 使用内置的 `/create-skill` 命令（推荐，快速便捷）
2. **方法二：** 手动创建 Skill 目录和 `SKILL.md` 文件（完全自定义）

### ⚡ 方法一：使用内置 /create-skill 命令（推荐）

VS Code Copilot 提供了内置的 `/create-skill` 命令，可以快速创建 Skills，特别适合从对话历史中提取可复用的知识。

#### 📌 常用实践：从对话中泛化技能

当你解决了一个复杂问题后，可以立即将解决过程转化为可复用的技能：

```
// 场景：你刚刚帮用户解决了一个复杂的 Docker 部署问题
// 对话结束后，执行以下命令：

/create-skill 请审查当前对话历史，将 Docker 部署的解决流程泛化为可复用的技能

// Copilot 会：
// 1. 分析整个对话上下文
// 2. 识别关键的解决步骤和模式
// 3. 提取通用的解决方案
// 4. 自动生成完整的 SKILL.md 文件
// 5. 询问技能名称和描述
// 6. 自动创建目录结构并保存文件
```

> ✅ 这种方法的优势
> - **零配置：** 无需手动创建目录结构
> - **智能提取：** 自动识别对话中的关键模式和最佳实践
> - **即时可用：** 创建后立即可在后续对话中使用
> - **持续积累：** 将解决问题的经验沉淀为组织资产

#### 🎯 /create-skill 命令详解

##### 基本语法：

```
/create-skill [描述信息]
```

##### 使用场景示例：

| 场景 | 命令示例 | 效果 |
|------|----------|------|
| **从当前对话提取** | `/create-skill 审查当前对话历史，将其泛化为可复用的技能` | 分析当前会话，提取通用模式 |
| **指定技能类型** | `/create-skill 创建一个用于调试 React 性能问题的技能` | 提出澄清问题并生成针对性技能 |
| **详细描述需求** | `/create-skill 创建一个技能，用于：1. 识别代码中的安全漏洞 2. 提供修复建议 3. 生成安全测试用例` | 根据详细步骤生成完整技能 |

#### 📋 执行流程

当你输入 `/create-skill` 命令后，Copilot 会按照以下流程执行：

```
步骤 1：Copilot 分析你的需求
↓
步骤 2：提出澄清问题（如果需要）
  - 技能的具体用途是什么？
  - 应该包含哪些功能？
  - 需要哪些辅助资源？
↓
步骤 3：生成完整的目录结构
  .github/skills/your-skill-name/
  ├── SKILL.md          (核心指令文件)
  ├── examples/         (示例代码)
  └── scripts/          (辅助脚本，可选)
↓
步骤 4：展示生成的 SKILL.md 内容
↓
步骤 5：等待你确认或修改
↓
步骤 6：保存到指定位置（项目级或个人级）
```

#### 💡 高级技巧

> **技巧 1：结合具体场景描述**
> 提供更详细的上下文可以获得更精准的技能：
> ```
> /create-skill 创建一个技能，用于处理 Spring Boot 项目中的事务管理问题。
> 场景：当用户遇到 @Transactional 注解不生效、事务传播机制配置错误、
> 或者需要优化事务性能时，应该：
> 1. 检查事务配置是否正确
> 2. 分析事务传播行为
> 3. 提供优化建议
> 4. 生成配置示例
> ```

> **技巧 2：指定技能的触发条件**
> 在描述中明确技能的使用场景，确保正确的触发：
> ```
> /create-skill 创建一个技能，专门用于调试 Kubernetes Pod 启动失败问题。
> 触发条件：当用户提到 "Pod 启动失败"、"CrashLoopBackOff"、
> "容器无法启动"、"Kubernetes 调试" 等关键词时激活。
> 技能应该包含常见的失败原因分析和解决方案。
> ```

> **技巧 3：从多个对话中提取最佳实践**
> 如果你在多个会话中都解决了类似问题，可以综合创建技能：
> ```
> /create-skill 我最近在三个不同的项目中都遇到了 Elasticsearch 查询性能问题，
> 每次都通过创建合适的索引和优化查询语句解决了。
> 请创建一个技能，总结这些场景中的最佳实践，包括：
> 1. 索引设计原则
> 2. 查询优化技巧
> 3. 性能分析方法
> 4. 常见陷阱和解决方案
> ```

> ⚠️ 注意事项
> - **技能名称规范：** Copilot 会自动生成符合规范的名称（小写、连字符分隔），你也可以手动指定
> - **描述质量：** 确保描述清晰说明技能的功能和使用场景，这样才能正确触发
> - **内容审查：** 生成后请仔细审查 SKILL.md 的内容，确保准确性和完整性
> - **位置选择：** 根据技能的适用范围选择项目级或个人级存储
> - **持续优化：** 技能创建后可以根据实际使用情况进行调整和优化

### 📝 方法二：手动创建 Skill（完全自定义）

如果你需要完全控制 Skill 的结构和内容，可以手动创建：

#### 🎨 手动创建流程

1. 在 `.github/skills/` 创建 Skill 目录
2. 创建 `SKILL.md` 文件（必需）
3. 编写 YAML frontmatter（name 和 description）
4. 编写技能主体内容（指令、流程、示例）
5. 可选：添加脚本、示例、资源文件
6. 测试和优化触发条件

#### 📝 步骤 1：创建基础 SKILL.md

每个 Skill 都需要一个 `SKILL.md` 文件，采用以下结构：

```
---
name: webapp-testing
description: 使用 Playwright 测试 web 应用程序的指南。当被要求创建或运行基于浏览器的测试时使用此技能。
---

# 使用 Playwright 进行 Web 应用测试

此技能帮助您为 web 应用程序创建和运行基于浏览器的测试。

## 何时使用此技能

当您需要以下功能时使用此技能：
- 为 web 应用程序创建新的 Playwright 测试
- 调试失败的浏览器测试
- 为新项目设置测试基础设施

## 创建测试

1. 查看[测试模板](./test-template.js)了解标准测试结构
2. 识别要测试的用户流程
3. 在 `tests/` 目录中创建新的测试文件
4. 使用 Playwright 的定位器查找元素（推荐使用基于角色的选择器）
5. 添加断言以验证预期行为

## 运行测试

在本地运行测试：
```bash
npx playwright test
```

调试测试：
```bash
npx playwright test --debug
```

## 最佳实践

- 为动态内容使用 data-testid 属性
- 保持测试独立和原子化
- 对复杂页面使用页面对象模型
- 失败时截图
```

### 📋 SKILL.md 文件格式详解

#### Header（必需）

Header 采用 YAML frontmatter 格式，包含以下字段：

| 字段 | 必需 | 描述 | 限制 |
|------|------|------|------|
| `name` | ✅ 是 | Skill 的唯一标识符 | 小写，用连字符分隔（如 `webapp-testing`），最多 64 字符 |
| `description` | ✅ 是 | 描述 Skill 的功能**以及何时使用** | 需明确说明能力和使用场景，最多 1024 字符 |

#### Body（技能主体）

技能主体包含 Copilot 在使用此 Skill 时应遵循的指令、指南和示例。应编写清晰、具体的指令，描述：

- Skill 帮助完成什么
- 何时使用 Skill
- 遵循的分步程序
- 预期输入和输出的示例
- 对包含的脚本或资源的引用

可以使用相对路径引用 Skill 目录中的文件。例如，引用 Skill 目录中的脚本：

```
See [test template](./test-template.js) for the standard structure.
Reference [setup script](./scripts/setup.sh) for environment configuration.
```

### 🔧 步骤 2：添加辅助资源（可选）

根据 Skill 的复杂度，可以添加以下辅助资源：

```
webapp-testing/
├── SKILL.md              # 主指令文件
├── test-template.js      # 测试模板
├── scripts/
│   ├── setup.sh          # 环境设置脚本
│   └── run-tests.sh      # 测试运行脚本
└── examples/
    ├── login-test.js     # 登录测试示例
    └── checkout-test.js  # 结账测试示例
```

### 📝 步骤 3：编写高质量的 Description

description 是触发 Skill 的关键，必须同时说明功能和使用场景：

| 技巧 | 示例（好） | 示例（差） |
|------|-----------|-----------|
| **明确功能** | "使用 Playwright 测试 web 应用程序" | "测试助手" |
| **说明触发条件** | "当被要求创建或运行基于浏览器的测试时使用" | "需要时使用" |
| **包含关键词** | "Playwright、浏览器测试、web 应用" | "测试相关" |

> ✅ 优秀 Description 公式
> **[功能描述] + [具体能力] + [使用场景] + [触发关键词]**
> ```
> description: 调试失败的 GitHub Actions 工作流的指南。分析日志、识别问题并提供修复建议。当被要求调试失败的 GitHub Actions 工作流、CI/CD 失败或构建错误时使用。
> ```

### 🧪 步骤 4：测试和优化

#### 测试触发条件

创建 Skill 后，通过自然语言请求测试是否能正确触发：

```
// 测试用例 1：应触发
"帮我为这个页面创建 Playwright 测试"
"为登录功能编写浏览器测试"
"设置 web 应用的测试环境"

// 测试用例 2：不应触发（验证不过度触发）
"帮我写一个 Python 脚本"
"创建一个 React 组件"
"优化 SQL 查询性能"
```

#### 优化技巧

- **不足触发：** 在 description 中添加更多细节和关键词
- **过度触发：** 精简 description，使其更具体
- **添加示例：** 在 SKILL.md 中包含更多输入/输出示例
- **引用资源：** 合理使用相对路径引用其他文件

---

## 5. 示例 Skills

### 🏗️ 示例：API 文档生成 Skill

```
---
name: api-documentation
description: 从 OpenAPI 规范和代码注释生成全面的 API 文档。当被要求创建或更新 API 文档时使用此技能。
---

# API 文档生成器

此技能帮助为 REST 和 GraphQL API 生成全面的 API 文档。

## 何时使用

当您需要以下功能时使用此技能：
- 从 OpenAPI/Swagger 规范生成 API 文档
- 为 API 端点创建内联代码文档
- 生成 API 参考文档
- 记录请求/响应模式

## 文档结构

1. 概述部分，包含 API 用途和身份验证
2. 按资源分组的端点列表
3. 详细的端点文档：
   - HTTP 方法和路径
   - 请求参数和标头
   - 请求正文模式
   - 响应示例（成功和错误）
   - 状态码和错误处理

## 最佳实践

- 为每个端点包含实际示例
- 记录所有可能的错误响应
- 在端点之间使用一致的格式
- 包含身份验证和速率限制信息
- 提供 curl 示例以便快速测试
```

---

## 6. 最佳实践案例

### 📋 案例一：会话内容总结技能

这是一个完整的技能案例，展示了如何创建一个实用的会话总结技能。该技能可以自动将当前会话的关键内容提炼为结构化 Markdown 文档，便于后续查阅和归档。

#### 技能概览

| 属性 | 内容 |
|------|------|
| **技能名称** | `session-summary` |
| **功能描述** | 总结当前会话内容并生成文档。会话结束时、需要保存会话记录、总结对话、归档会话内容时使用 |
| **触发关键词** | 总结会话、保存会话、会话归档、summarize session |
| **参数提示** | 可选：指定会话主题名称，否则自动识别 |

#### 技能主体内容结构

该技能包含完整的使用场景、执行步骤、输出模板和质量标准：

> 🎯 使用场景
> - 当前会话包含有价值的讨论、决策或操作记录
> - 需要归档会话内容以供后续参考
> - 会话即将结束，想保留关键信息

> 📝 执行步骤
> 1. **回顾会话内容**：识别核心主题、关键决策、操作变更、问题和解决方案
> 2. **确定会话主题**：从对话中提取2-8字的简洁主题短语
> 3. **生成文档**：使用标准模板创建结构化 Markdown 文档
> 4. **保存文档**：按命名规则保存到指定目录并确认

> 📄 输出模板
> 文档采用统一的结构化格式：
> ```
> # {会话主题}
> 
> > 会话时间：{YYYY-MM-DD HH:mm}
> 
> ## 摘要
> {用 2-3 句话概括本次会话的核心内容和成果}
> 
> ## 主要内容
> ### {子主题1}
> - {要点}
> - {要点}
> 
> ## 关键决策
> - {决策1}：{原因/背景}
> 
> ## 变更记录
> {如果会话中有代码/文件变更，列出变更的文件和内容概要}
> 
> ## 待办事项
> - [ ] {后续需要处理的事项}
> 
> ## 相关文件
> - {涉及的关键文件路径}
> ```

> ✅ 质量标准
> - **压缩率**：文档长度应远小于原始会话长度，只保留关键信息
> - **可读性**：不熟悉会话上下文的人也能理解文档内容
> - **准确性**：不遗漏关键决策和操作，不添加会话中未提及的内容
> - **可操作性**：待办事项具体明确，相关文件路径准确

#### 💡 最佳实践要点

从这个案例中我们可以学习到以下关键要点：

> 1. 清晰的触发条件
> 在 description 中明确说明了使用场景和触发关键词，确保技能在合适的时候被自动加载。

> 2. 结构化的执行流程
> 将复杂任务分解为明确的步骤，每个步骤都有具体的目标和操作指南。

> 3. 标准化的输出格式
> 提供统一的文档模板，确保输出的一致性和可读性。

> 4. 明确的质量标准
> 定义了清晰的质量指标，帮助用户和 AI 理解什么是高质量的输出。

> 5. 灵活的参数处理
> 支持可选参数，同时提供默认行为，提高技能的适用性。

---

## 7. 进阶技巧与常见问题

### 🚀 高级技巧

#### 1. Skills 组合调用

多个 Skills 可以同时激活，协同完成复杂任务：

```
用户请求："调试失败的 CI/CD 工作流并优化慢测试"

Copilot 会自动激活：
✅ cicd-debugger Skill (调试工作流)
✅ test-optimizer Skill (优化测试)

两个 Skills 协作，先调试问题，再优化性能
```

#### 2. 引用外部资源

在 SKILL.md 中使用相对路径引用目录中的文件：

```
## Setup Instructions

1. Run the [setup script](./scripts/setup.sh)
2. Review the [configuration template](./templates/config.yaml)
3. See [examples](./examples/) for reference implementations
```

#### 3. 版本控制最佳实践

- 将项目级 Skills 放在 `.github/skills/` 并提交到仓库
- 在 SKILL.md 中添加版本信息：

```
---
name: my-skill
description: ...
version: 1.0.0
---

# My Skill

## Changelog

### v1.0.0 (2026-04-01)
- Initial release
- Add basic functionality
```

### ⚠️ 常见问题与解决方案

#### 问题 1：Skill 无法自动触发

> **可能原因：** description 不够具体或缺少触发关键词
> **解决方案：**
> - 添加明确的触发词（如 "Use when asked to..."）
> - 包含更多场景描述
> - 确保启用了 `chat.useAgentSkills` 设置

#### 问题 2：Skill 触发过于频繁

> **可能原因：** description 过于宽泛
> **解决方案：**
> - 精简 description，使其更具体
> - 移除通用关键词
> - 添加排除场景说明

#### 问题 3：资源文件引用失败

> **可能原因：** 路径错误或文件不存在
> **解决方案：**
> - 使用相对路径（如 `./scripts/setup.sh`）
> - 确保文件存在于 Skill 目录中
> - 检查文件名拼写和大小写

#### 问题 4：Skill 在其他平台无法使用

> **可能原因：** 平台特定依赖
> **解决方案：**
> - 确保 Skill 符合 Skills 开放标准
> - 避免使用平台特定工具
> - 提供适用于不同 AI 编码代理的替代方案

### 📚 学习资源

- **官方文档：** [VS Code Copilot Skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
- **Skills 标准：** [agentskills.io](https://agentskills.io)
- **社区集合：** [github/awesome-copilot](https://github.com/github/awesome-copilot)
- **参考示例：** [anthropics/skills](https://github.com/anthropics/skills)

### 🔐 安全考虑

#### 脚本执行安全

- VS Code 终端工具提供脚本执行控制
- 可以配置自动批准选项和允许列表
- 对运行的代码进行严格控制
- 审查共享 Skills 中的所有脚本

#### 最佳实践

- 只使用受信任来源的 Skills
- 审查 SKILL.md 和所有脚本文件
- 在测试环境中先验证 Skills
- 定期更新 Skills 以获得安全补丁
- 对敏感操作添加额外的确认步骤

---

## VS Code + GitHub Copilot Skills 培训指南

**版本：1.0 | 更新日期：2026年4月**

开放标准 · 跨平台兼容 · 社区驱动

遵循 Skills 开放标准：[agentskills.io](https://agentskills.io)