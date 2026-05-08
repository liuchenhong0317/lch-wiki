# 🌱 Spec Kit CLI 培训文档
*掌握 Spec-Driven Development，使用 AI 驱动的规格驱动开发方法构建高质量软件*
## 项目统计
| 数字 | 标签 |
|------|------|
GitHub Stars
11+
AI Agents
2.3K+
Forks
MIT
开源协议
## 1. 培训概述
### 1.1 培训目标
通过本培训，您将能够：
- 理解 Spec-Driven Development（规格驱动开发）的核心理念
- 掌握 Specify CLI 工具的安装和配置
- 熟练使用 Slash 命令进行项目开发
- 在 VSCode 中高效使用 GitHub Copilot 与 Spec Kit
- 独立完成从需求到实现的完整开发流程
### 1.2 适用人群
- 使用 VSCode 作为主要开发环境的开发者
- 已订阅 GitHub Copilot 的开发者
- 希望提升开发效率和代码质量的软件工程师
- 对 AI 辅助开发感兴趣的技术团队
- 想要学习现代化开发流程的项目管理者
### 1.3 前置要求
> **📋 📋 培训前置条件**
>
在开始培训前，请确保您具备以下条件：
| 要求项 | 说明 | 重要程度 |
| --- | --- | --- |
| Python 3.8+ | 用于运行 Specify CLI 工具 | 必需 |
| Git 2.20+ | 版本控制和项目管理 | 必需 |
| uv 包管理器 | Python 包管理工具（推荐） | 必需 |
| VSCode | 代码编辑器和开发环境 | 推荐 |
| GitHub Copilot 订阅 | AI 编程助手 | 推荐 |
## 2. Spec Kit 简介
### 2.1 什么是 Spec-Driven Development
#### 📋 传统开发模式 几十年来，代码一直是王道。规格说明书只是临时搭建的脚手架，一旦"真正的编码工作"开始就会被丢弃。这导致了沟通误解和技术债务。
#### ⚡ Spec Kit 方式 使用 Spec Kit，规格说明书变得可执行，直接生成工作实现，而不仅仅是指导实现。帮助您专注于产品场景，而不是编写重复代码。
> **💡 💡 核心理念**
>
Spec-Driven Development 翻转了传统软件开发的脚本。规格说明书不再是文档，而是可执行的、能够直接生成工作代码的蓝图。
### 2.2 Spec Kit 的核心理念
#### 🎯 Focus on What 定义您想要构建什么以及为什么，而不是技术实现细节。让 AI 帮您处理"如何做"。
#### 🤖 AI-Powered 利用 AI 代理自动将规格说明书转换为工作代码，大幅提升开发效率。
#### 🚀 Faster Delivery 消除规格与实现之间的鸿沟，减少开发时间，加速产品交付。
### 2.3 Spec Kit 的核心优势
| 优势 | 描述 | 影响 |
| --- | --- | --- |
| 规格可执行 | 规格说明书直接转换为代码实现 | 减少人工编码错误 |
| AI 驱动 | 利用先进的 AI 模型理解和执行规格 | 提高开发效率 3-10 倍 |
| 多代理支持 | 支持 11+ 种 AI 编程助手 | 灵活选择工具 |
| 开放源代码 | MIT 协议，完全开源 | 可自由定制和扩展 |
| 社区活跃 | 28K+ GitHub Stars，活跃的社区支持 | 丰富的资源和帮助 |
## 3. 环境准备与安装
> **📋 📄 详细指南**
>
环境准备和安装步骤请参考附件 SDD-quick-start-V0.1.5.pdf，其中包含了完整的安装配置说明。
### 3.1 核心要求
| 要求项 | 说明 | 重要程度 |
| --- | --- | --- |
| Python 3.8+ | 用于运行 Specify CLI 工具 | 必需 |
| Git 2.20+ | 版本控制和项目管理 | 必需 |
| uv 包管理器 | Python 包管理工具（推荐） | 必需 |
| VSCode | 代码编辑器和开发环境 | 推荐 |
| GitHub Copilot 订阅 | AI 编程助手 | 推荐 |
> 💡 **💡 快速开始：请先查阅附件文档 SDD-quick-start-V0.1.5.pdf 完成环境配置，然后继续学习后续章节。**
>
## 4. 项目初始化
### 4.1 创建新项目
**Step 1:**
#### 使用 CLI 创建项目
<pre><code># 创建新项目并指定使用 GitHub Copilot
specify init my-project --ai copilot
# 或使用交互式选择
specify init my-project</code></pre>
**Step 2:**
#### 支持的其他 AI 代理
<pre><code># Claude Code
specify init my-project --ai claude
# Gemini CLI
specify init my-project --ai gemini
# Cursor
specify init my-project --ai cursor
# 其他支持的代理：codex, windsurf, qwen, opencode 等</code></pre>
### 4.2 在现有项目中初始化
<pre><code># 在当前目录初始化
specify init . --ai copilot
# 或使用 --here 标志
specify init --here --ai copilot
# 跳过 Git 初始化
specify init my-project --ai copilot --no-git
### 4.3 项目结构说明
初始化完成后，您的项目目录结构如下：
<pre><code>项目名称/
├── .github/
│   ├── agents/
│   │   ├── speckit.analyze.agent.md
│   │   ├── speckit.checklist.agent.md
│   │   ├── speckit.clarify.agent.md
│   │   ├── speckit.constitution.agent.md
│   │   ├── speckit.implement.agent.md
│   │   ├── speckit.plan.agent.md
│   │   ├── speckit.specify.agent.md
│   │   ├── speckit.tasks.agent.md
│   │   └── speckit.taskstoissues.agent.md
│   └── prompts/
│       ├── speckit.analyze.prompt.md
│       ├── speckit.checklist.prompt.md
│       ├── speckit.clarify.prompt.md
│       ├── speckit.constitution.prompt.md
│       ├── speckit.implement.prompt.md
│       ├── speckit.plan.prompt.md
│       ├── speckit.specify.prompt.md
│       ├── speckit.tasks.prompt.md
│       └── speckit.taskstoissues.prompt.md
└── .specify/
├── integrations/
├── memory/
├── scripts/
│   └── powershell/
│       ├── check-prerequisites.ps1
│       ├── common.ps1
│       ├── create-new-feature.ps1
│       ├── setup-plan.ps1
│       └── update-agent-context.ps1
└── templates/</code></pre>
> **📋 📁 目录说明**
>
- .github/agents/ - AI Agent 配置文件，定义各个阶段的智能助手行为
- .github/prompts/ - Prompt 模板文件，定义与 AI 交互的提示词模板
- .specify/memory/ - 存储项目记忆和原则，包含项目指导方针
- .specify/integrations/ - 集成配置目录，用于外部工具集成
- .specify/scripts/powershell/ - PowerShell 自动化脚本，包含环境检查、功能创建等工具
- .specify/templates/ - 文档模板，用于生成规格、计划、任务等文档
## 5. 开发工作流程（重点）
### 开发工作流程图
## 开发工作流程图
```
┌─────────────────────────────────────────────────────────────┐
│                        项目初始化                           │
└─────────────────────────────────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────────┐
│  /constitution                                               │
│  建立项目原则，只执行一次                                     │
└─────────────────────────────────────────────────────────────┘
│
▼
┌───────────────────────────┐
│     功能开发流程            │
│     (每个功能重复)          │
└───────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────────┐
│  /specify [必须]                                             │
│  定义功能需求                                                 │
└─────────────────────────────────────────────────────────────┘
│
┌──────────────────┴──────────────────┐
│ (可选)                                 │
▼                                       ▼
┌──────────────────────┐              ┌────────────────────────┐
│ /clarify [可选]      │              │ /plan [必须]            │
│ 澄清需求              │──────────────▶│ 制定技术方案            │
└──────────────────────┘              └────────────────────────┘
│
▼
┌────────────────────────────┐
│ /tasks [必须]               │
│ 生成任务列表                 │
└────────────────────────────┘
│
┌─────────────────────────┴─────────────────────────┐
│ (可选)                                              │
▼                                                     ▼
┌────────────────────────┐                           ┌────────────────────────┐
│ /analyze [可选]         │                           │ /implement [必须]       │
│ 交叉验证分析             │────────────────────────▶│ 执行实现                 │
└────────────────────────┘                           └────────────────────────┘
```
### 图例
- **初始化节点**: 项目初始化（仅一次）
- **必须流程**: 每个功能必须执行的步骤
- **可选流程**: 根据需要执行的步骤
> **💡 🎯 核心重点**
>
本节是培训的核心内容，详细讲解从需求到实现的完整 Spec-Driven Development 流程。
### 5.1 Phase 1: Foundation（基础阶段）
### 📋 阶段目标：建立清晰的项目基础
#### 1. /constitution - 建立项目原则
首先建立项目的指导原则和开发标准，确保后续所有决策都有一致的基础。
操作位置：VSCode 中的 GitHub Copilot Chat
/speckit.constitution 创建项目原则，重点关注代码质量、测试标准、用户体验一致性和性能要求。包含这些原则如何指导技术决策和实现选择的治理规则。
生成文件：.specify/memory/constitution.md
💡
培训提示：项目原则应该反映团队的价值观和项目的具体要求。好的原则包括：代码规范、测试覆盖率要求、性能指标、安全标准等。
#### 2. /specify - 创建功能规格
定义您想要构建什么以及为什么，关注业务需求而非技术实现。
操作位置：VSCode 中的 GitHub Copilot Chat
/speckit.specify 构建一个任务管理应用，支持用户认证、实时协作和移动端支持。用户应该能够创建项目、分配任务，并使用看板跟踪进度。
生成文件：.specify/specs/001-feature-name/spec.md
> **📋 📝 规格文档内容**
>
- User Stories（用户故事）
- Functional Requirements（功能需求）
- Acceptance Criteria（验收标准）
- Review & Acceptance Checklist（审查清单）
#### 3. /clarify - 澄清需求细节
通过结构化提问澄清规格中不明确的部分，必须在 /plan 之前运行。
操作位置：VSCode 中的 GitHub Copilot Chat
/speckit.clarify
AI 会提出针对性问题：
- 用户认证的具体方式？
- 实时协作需要哪些功能？
- 移动端是原生应用还是响应式 Web？
- 看板的列如何定义？
> **⚠️ ⚠️ 重要提示**
>
/clarify 命令必须在 /plan 之前运行，除非您明确要跳过澄清阶段（例如探索性原型）。
### 5.2 Phase 2: Implementation（实现阶段）
### 🚀 阶段目标：将规格转换为可工作的代码
#### 1. /plan - 创建技术实现计划
选择技术栈和架构，制定详细的技术实现方案。
操作位置：VSCode 中的 GitHub Copilot Chat
/speckit.plan 使用 React + TypeScript 前端，Node.js + Express 后端，PostgreSQL 数据库。前端使用 Material-UI 组件库，支持实时更新的 WebSocket。
生成文件：
specs/001-feature/plan.md - 实现计划
specs/001-feature/data-model.md - 数据模型
specs/001-feature/research.md - 技术研究
specs/001-feature/quickstart.md - 快速开始指南
#### 2. /tasks - 任务拆分
将实现计划分解为可执行的任务列表，按依赖关系排序。
操作位置：VSCode 中的 GitHub Copilot Chat
/speckit.tasks
生成文件：specs/001-feature/tasks.md
> **📋 📋 任务文档结构**
>
- 按用户故事组织的任务分解
- 依赖关系管理（任务按依赖排序）
- 并行执行标记 [P]
- 精确的文件路径指定
- 测试驱动开发结构
- 检查点验证
#### 3. /analyze - 交叉验证分析
在实现前进行跨文档一致性和覆盖率分析。
操作位置：VSCode 中的 GitHub Copilot Chat
/speckit.analyze
在 /tasks 之后、/implement 之前运行。
#### 4. /implement - 执行实现
执行所有任务，根据计划构建功能。
操作位置：VSCode 中的 GitHub Copilot Chat
/speckit.implement
> **⚠️ ⚠️ 重要说明**
>
AI 代理会执行本地 CLI 命令（如 dotnet、npm 等），确保您的机器上安装了所需的工具。
### 5.3 完整流程演示
<pre><code># 步骤 1: 初始化项目（终端）
specify init taskify --ai copilot
cd taskify
# 步骤 2: 在 VSCode 中打开项目
code .
# 步骤 3: 在 Copilot Chat 中执行以下命令（按顺序）
# 3.1 建立项目原则
/speckit.constitution 创建专注于代码质量、测试、用户体验一致性和性能的项目原则
# 3.2 创建功能规格
/speckit.specify 开发 Taskify 团队生产力平台。允许用户创建项目、添加团队成员、分配任务、评论和在看板中移动任务...
# 3.3 澄清需求
/speckit.clarify
# 3.4 创建技术计划
/speckit.plan 使用 .NET Aspire，PostgreSQL 数据库，Blazor Server 前端，支持拖拽看板和实时更新
# 3.5 生成任务列表
/speckit.tasks
# 3.6 执行实现
/speckit.implement</code></pre>
#### Slash 命令完整参考
| 命令 | 描述 | 使用场景 |
| --- | --- | --- |
| /speckit.constitution | 创建项目指导原则和开发指南 | 首先运行以建立项目标准 |
| /speckit.specify | 定义需求（what 和 why，非技术栈） | 关注业务需求，而非技术实现 |
| /speckit.clarify | 通过结构化提问澄清不明确区域 | 必须在 /plan 前运行 |
| /speckit.plan | 创建技术实现计划和架构决策 | 指定架构、框架和技术决策 |
| /speckit.tasks | 生成可执行的任务列表 | 将计划分解为具体步骤 |
| /speckit.analyze | 跨文档一致性和覆盖率分析 | /tasks 后、/implement 前运行 |
| /speckit.implement | 执行所有任务构建功能 | 根据规格生成工作代码 |
## 6. 使用 GitHub Copilot 的最佳实践
### 6.1 在 VSCode 中配置和使用
#### 打开 Copilot Chat
在 VSCode 中有三种方式打开 Copilot Chat：
快捷键：Ctrl+Shift+I (Windows/Linux) 或 Cmd+Shift+I (macOS)
侧边栏：点击左侧活动栏的 Copilot 图标
命令面板：Ctrl+Shift+P → 输入 "Copilot Chat"
#### 验证 Spec Kit 命令已加载
在 Copilot Chat 中输入 /，您应该看到以下 Spec Kit 命令：
/speckit.constitution
/speckit.specify
/speckit.clarify
/speckit.plan
/speckit.tasks
/speckit.analyze
/speckit.implement
> **📋 ✅ 验证成功**
>
如果看到这些命令，说明 Spec Kit 已正确配置！
### 6.2 Slash 命令的使用技巧
#### 🎯 命令参数传递 在命令后直接添加描述： /speckit.constitution 创建注重安全性和性能的项目原则
#### 📝 详细需求描述 可以多行描述详细需求： /speckit.specify 构建照片相册管理器。 支持功能： - 按日期分组相册 - 拖拽排序 - 平铺预览 - 本地存储
> 💡 **💡 最佳实践： 使用清晰、具体的语言描述需求 提供足够的上下文信息 按顺序执行命令，不要跳过关键步骤 定期审查 AI 生成的文档和代码**
>
### 6.3 与 Copilot Chat 的交互方式
#### 交互模式
1. 指令模式 - 使用 Slash 命令执行特定任务
/speckit.plan 使用 React 和 TypeScript
2. 问答模式 - 提问并获得解释
请解释 spec.md 中的用户故事是如何映射到技术实现的？
3. 迭代模式 - 根据反馈调整
我需要修改 plan.md，增加 Redis 缓存层，请更新技术方案
4. 验证模式 - 检查和确认
请审查当前生成的任务列表，确认是否有遗漏的步骤
### 6.4 常见使用场景
#### 场景 1：快速原型开发
<pre><code># 1. 快速建立基础
/speckit.constitution 这是一个快速原型项目，重点验证核心功能
# 2. 描述核心功能
/speckit.specify 构建一个简单的待办事项列表，支持添加、删除、标记完成
# 3. 跳过详细澄清（快速原型）
这是一个快速验证项目，跳过详细澄清
# 4. 使用简单技术栈
/speckit.plan 使用 vanilla JavaScript，HTML，CSS，数据存储在 localStorage
# 5. 快速实现
/speckit.tasks
/speckit.implement</code></pre>
#### 场景 2：企业级应用开发
<pre><code># 1. 建立严格的项目原则
/speckit.constitution 创建企业级应用原则：
- 代码覆盖率不低于 80%
- 所有 API 必须有认证和授权
- 敏感数据必须加密
- 符合 GDPR 要求
# 2. 详细的功能规格
/speckit.specify 构建企业客户管理系统，支持多租户、角色权限、审计日志...
# 3. 详细澄清需求
/speckit.clarify
# 4. 技术方案
/speckit.plan 使用 Spring Boot，PostgreSQL，Redis，支持 Docker 部署
# 5. 验证和实现
/speckit.tasks
/speckit.analyze
/speckit.implement</code></pre>
#### 场景 3：现有项目扩展
<pre><code># 1. 在现有项目中初始化（终端）
cd existing-project
specify init . --ai copilot
# 2. 基于现有代码建立原则（Copilot Chat）
/speckit.constitution 基于项目现有架构，创建与新功能一致的开发原则
# 3. 描述新功能
/speckit.specify 在现有系统中添加通知模块，支持邮件、短信、站内信
# 4. 集成现有架构
/speckit.plan 集成现有的认证系统、使用现有消息队列、遵循现有 API 规范
# 后续步骤同上...</code></pre>
## 7. 实战案例
### 待办事项应用案例
#### 项目背景
构建一个简单的待办事项应用，帮助用户管理日常任务。
#### Step 1: 初始化项目
specify init todo-app --ai copilot
cd todo-app
code .
#### Step 2: 建立项目原则
<pre><code>/speckit.constitution 创建项目原则：
1. 用户体验优先，界面简洁直观
2. 代码可维护性高，注释清晰
3. 技术栈约束：
- 前端：必须使用 Vue 3 (Composition API +