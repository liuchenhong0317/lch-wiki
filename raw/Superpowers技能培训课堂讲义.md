

# Superpowers 技能培训手册

> 基于 [obra/superpowers](https://github.com/obra/superpowers) 开源技能套件
> 适用环境：GitHub Copilot / Claude Code / Cursor 等 AI 代理工具
>
> 培训人：刘晨虹  研究院智能所

---

## 一、什么是 Superpowers 技能

Superpowers 是一套面向 AI 编程代理的**可复用流程技能**，每个技能是一份精心测试过的"最佳实践文档"，告诉 AI 代理在特定场景下**应该怎么做**，而非靠模型默认行为碰运气。

- 技能存放位置：`~/.agents/skills/` （全局安装）
- 安装命令：`npx skills add obra/superpowers@<技能名> -g -y(单个安装)`  `npx skills add obra/superpowers`(全部安装)
- 技能查询：`npx skills find superpowers`

---

## 二、技能总览（共 13 个）

| # | 技能名 | 触发条件 | 核心功能（精简） |
|---|--------|----------|-----------------|
| 1 | **using-superpowers** | 每次对话开始时 | 总调度器，强制调用适用技能，用户指令优先级最高 |
| 2 | **brainstorming** | 开始任何新功能/项目设计时 | 交互式梳理需求，产出 Spec 规格文档 |
| 3 | **writing-plans** | 有 Spec 需拆解为实施步骤时 | 将规格转为含完整代码的原子任务 Plan |
| 4 | **using-git-worktrees** | 执行任何计划前/需要隔离环境时 | 创建隔离 Git 工作分支，验证 gitignore，跑基线测试 |
| 5 | **executing-plans** | 有 Plan 需在当前会话执行时 | 批次逐步执行计划，设审查检查点，遇阻即停询问 |
| 6 | **subagent-driven-development** | 有 Plan 且任务相互独立时（推荐） | 每任务派新子代理，两阶段审查（规格合规→代码质量） |
| 7 | **test-driven-development** | 实现任何功能或修复 Bug 时 | 铁律：先写失败测试，再写最小实现，禁止反向操作 |
| 8 | **systematic-debugging** | 遇到 Bug/测试失败/异常行为时 | 铁律：必须找根因再修，禁止猜测，四阶段调查法 |
| 9 | **dispatching-parallel-agents** | 出现 2+ 个互不相关的独立故障时 | 按问题域分组，并行派遣代理同时调查，整合修复结果 |
| 10 | **verification-before-completion** | 声明任务完成/提交/发 PR 前 | 铁律：必须运行命令取得真实输出后才能声称通过 |
| 11 | **requesting-code-review** | 每个任务完成后/功能合并前 | 派遣审查子代理，按严重性分级处理反馈 |
| 12 | **receiving-code-review** | 收到代码审查反馈时 | 先验证建议再实施，技术评估后合理推回，禁止盲从 |
| 13 | **finishing-a-development-branch** | 所有任务完成、分支就绪时 | 验证测试→提供4选项（合并/PR/保留/丢弃）→清理工作区 |

---

## 三、技能详解

### 1. using-superpowers（总调度器）

**定位：** 贯穿整个对话的"大脑"，决定何时调用哪个技能。

**核心规则：**

- 收到任何用户消息，若有 **哪怕 1% 的可能性**适用某个技能，**必须先加载该技能**
- 优先级顺序：用户指令 > Superpowers 技能 > 系统默认行为
- 调用顺序：先调流程类技能（brainstorming、debugging），再调实现类技能

**优先级举例说明：**

> **场景 1：用户指令覆盖技能**
>
> - 技能规则：`test-driven-development` 要求"任何功能实现前必须先写失败测试"
> - 用户在 AGENT.md 中写："本项目不使用 TDD，直接编码即可"
> - **结果：** 跳过 TDD，直接编码。用户说了不用 TDD，技能无权强制。
>
> **场景 2：技能覆盖系统默认行为**
>
> - 系统默认行为：AI 收到"添加登录功能"后直接开始写代码
> - 技能规则：`using-superpowers` 要求先检查适用技能 → 命中 `brainstorming` → 先梳理需求 → 再写 Plan → 再执行
> - 用户没有额外指令
> - **结果：** 按技能流程走，而不是直接写代码。技能覆盖了系统默认的"直接动手"行为。
>
> **场景 3：三级同时存在**
> - 系统默认行为：遇到 Bug → 直接尝试修复
> - 技能规则：`systematic-debugging` 要求四阶段调查，禁止直接修
> - 用户说："别走调试流程了，直接把这行改成 `return null`"
> - **结果：** 直接改。用户的明确指令 > 技能的调试流程 > 系统默认的随意修复。

| 优先级 | 来源 | 本质 |
|--------|------|------|
| **最高** | 用户指令（AGENT.md / 直接对话） | "老板说了算" |
| **中间** | Superpowers 技能 | "团队规范" |
| **最低** | 系统默认行为 | "AI 自由发挥" |

**常见错误（禁止这样想）：**

| 错误想法 | 真实情况 |
|----------|----------|
| "这只是个简单问题" | 简单问题也是任务，先检查技能 |
| "我需要先了解更多" | 技能检查先于澄清性问题 |
| "这个技能太重了" | 简单的事会变复杂，用技能 |

---

### 2. brainstorming（头脑风暴）

**定位：** 项目起点，需求分析与方案探讨。

**产出：** `docs/superpowers/specs/` 下的规格文档（Spec）

**核心流程：**
1. 与用户交互式探讨需求
2. 分解子系统，确认边界
3. 生成完整规格文档
4. 派遣 Spec 审查子代理验证完整性

> **关于 Spec 审查子代理：** 这不是一个独立的 skill，而是 `brainstorming` 技能内置的子代理 prompt 模板（`spec-document-reviewer-prompt.md`）。Spec 文档写完后，用通用 Task 工具派遣一个临时审查代理，按 5 个维度检查：
> | 维度 | 审查内容 |
> |------|----------|
> | 完整性 | 是否存在 TODO、占位符、未完成章节 |
> | 一致性 | 是否有内部矛盾、冲突的需求 |
> | 清晰度 | 是否有歧义到可能导致实现错误的需求 |
> | 范围 | 是否聚焦于单个计划，而非跨多个独立子系统 |
> | YAGNI | 是否存在未被请求的功能或过度设计 |
>
> 审查结果为 **Approved**（通过）或 **Issues Found**（发现问题），仅阻止"会导致实施计划出错的严重问题"。

**适合用浏览器可视化展示的内容：**

- UI 线框图、布局对比
- 架构图、数据流图
- 两套设计方案对比

> **注意：** 可视化浏览器伴侣需要本地启动 HTTP Server，在 VS Code Copilot Chat 环境中无法使用。

---

### 3. writing-plans（编写计划）

**定位：** 将规格文档转化为可执行的实施计划。

**产出：** `docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md`

**核心原则：**
- 假设执行者对代码库**零了解**
- 每步是 **2-5 分钟**的原子操作
- 每步必须包含**完整代码**、精确文件路径、测试命令和预期结果
- **禁止占位符**（如 TBD、TODO、"参考 Task N"）

**Plan 文档结构：**
```markdown
# [功能名] 实施计划
**目标：** 一句话描述
**架构：** 2-3 句方案说明
**技术栈：** 关键技术/库

### Task N: [组件名]
**文件：**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py`

- [ ] **步骤 1: 写失败测试**
- [ ] **步骤 2: 运行确认测试失败**
- [ ] **步骤 3: 写最小实现**
- [ ] **步骤 4: 运行确认测试通过**
- [ ] **步骤 5: 提交**
```

**完成后提供两种执行选择：**
1. **Subagent 驱动（推荐）** — 每个 Task 派独立子代理
2. **内联执行** — 在当前会话使用 executing-plans 执行

---

### 4. using-git-worktrees（Git 隔离工作区）

**定位：** 所有计划执行前的环境隔离。

**目录选择优先级：**
1. 检查 `.worktrees/` 目录是否存在
3. 检查 AGENT.md 中是否有配置偏好

**验证 gitignore 操作：**

```bash
git check-ignore -q .worktrees
```
- 通过 → 直接创建 worktree
- 未通过 → 立即在 `.gitignore` 中添加 `.worktrees/`，提交后再创建

**目的：** 防止隔离工作区内容被意外提交进代码库。

**创建完成后：**
1. 自动检测并安装依赖（npm install / pip install 等）
2. 跑基线测试确认干净起点
3. 若测试失败 → 报告失败，询问是否继续

---

### 5. executing-plans（内联执行计划）

**适用场景：** 有 Plan 文件，在当前会话批次执行（非并行子代理）。即 AI 代理自己在当前对话中逐个读取 Task、逐步执行，上下文共享同一个会话；而 `subagent-driven-development` 则是每个 Task 派遣全新的子代理（独立上下文）。

**执行流程：**
1. 读取并批判性审查 Plan
2. 发现疑问 → 先向用户提出，确认后再开始
3. 逐 Task 标记 in_progress → 按步骤执行 → 标记 completed
4. 所有 Task 完成后调用 `finishing-a-development-branch`

**遇到以下情况立即停止：**

- 缺少依赖
- 测试持续失败
- 指令不清晰
- 计划存在根本性缺陷

> **提示：** 有子代理支持时，优先使用 `subagent-driven-development` 效果更好。当前环境（VS Code + GitHub Copilot）具备子代理能力（`runSubagent` 工具），因此推荐使用 `subagent-driven-development`。

---

### 6. subagent-driven-development（子代理驱动开发）

**定位：** `executing-plans` 的升级版，每个 Task 派遣独立子代理实现。

**核心优势：**
- 新鲜上下文，无污染
- 两阶段自动质量门禁
- 支持模型分级（简单任务用便宜模型）

**执行流程（每个 Task）：**

```
派遣实现子代理
    ↓
子代理提问？ → 回答后重新派遣
    ↓
子代理实现 + 自测 + 自审
    ↓
派遣规格合规审查子代理
    ↓
不合规 → 实现子代理修复 → 重新审查
    ↓
规格合规 ✅ → 派遣代码质量审查子代理
    ↓
不通过 → 实现子代理修复 → 重新审查
    ↓
质量通过 ✅ → Task 完成
```

**模型选择策略：**
| 任务类型 | 推荐模型 |
|----------|----------|
| 单文件、规格明确的机械实现 | 快速/便宜模型 |
| 多文件集成、模式匹配 | 标准模型 |
| 架构设计、审查类任务 | 最强模型 |

---

### 7. test-driven-development（测试驱动开发）

**铁律：**
```
没有失败的测试，就不写生产代码
```

**红绿重构循环：**

```
RED（写失败测试）
    → 验证它确实失败
    → GREEN（写最小实现让测试通过）
    → 验证所有测试通过
    → REFACTOR（重构优化）
    → 验证重构后测试仍然通过
    → 下一个功能点，回到 RED
```

**先写失败测试的意义：**
- 测试先行 = 验证"应该做什么"
- 测试后补 = 验证"你写了什么"（毫无价值）
- **必须亲眼看到测试失败**，才能证明这个测试在测正确的事

**如果先写了代码：**
- 删掉，重来
- 不能保留作"参考"
- 不能"边写测试边调整"
- 删除 = 真正的删除

**适用场景：** 新功能、Bug 修复、重构、行为变更（无例外）

---

### 8. systematic-debugging（系统化调试）

**铁律：**
```
不找到根因，不提修复方案
```

**四阶段调查法：**

| 阶段 | 名称 | 具体操作 |
|------|------|----------|
| **第一阶段** | 根因调查 | 仔细读错误信息和堆栈；稳定复现问题；检查近期 git 变更；多组件系统加诊断日志逐层确认 |
| **第二阶段** | 形成假说 | 基于证据推理出可能的根本原因（非猜测） |
| **第三阶段** | 验证假说 | 设计实验确认假说，而不是直接动手修 |
| **第四阶段** | 修复并验证 | 最小化修复，回归测试确认无新问题 |

**特别重要 — 多组件系统调试：**
```bash
# 在每个组件边界加日志：
# - 记录进入组件的数据
# - 记录离开组件的数据
# - 验证配置/环境变量传递
# 运行一次收集证据，再分析是哪层出问题
```

**什么时候最要遵守此规则：**
- 时间紧张时（紧急情况最容易猜测）
- "看起来很明显"时（简单Bug也有根因）
- 已经试了好几次修法还没好时

---

### 9. dispatching-parallel-agents（并行派遣代理）

**适用条件：**
- 3+ 个测试文件因**不同原因**失败
- 多个子系统**独立**出现问题
- 各问题域之间**没有共享状态**

**不适用条件：**
- 问题可能相互关联（修一个可能带动修另一个）
- 需要理解全局系统状态
- 代理之间会相互干扰（编辑同一文件）

**操作流程：**
1. 将故障按问题域分组
2. 每组写一份聚焦的代理任务（范围明确 + 清晰输出要求）
3. 并行派遣，同时调查
4. 等所有代理返回后整合，检查修改是否冲突
5. 运行全量测试套件验证

**触发场景举例：**
> 做了一次大的依赖升级后，跑全量测试发现 3 个模块同时报错：
> - `user-service`：`NullPointerException`（MyBatis 字段映射行为变了）
> - `order-service`：`Connection refused: localhost:6379`（Redis mock 版本不兼容）
> - `notification-service`：`IllegalArgumentException: unsupported charset`（HTTP Client 默认编码变了）
>
> 这三个问题互不相关、不会编辑同一文件 → **适用并行派遣**，3 个代理同时调查，耗时从串行的 35 分钟降到并行的 15 分钟。
>
> **反例：** 如果 3 个模块都报 `ClassNotFoundException: com.fasterxml.jackson.core.JsonParser`，说明根因相同（Jackson 依赖缺失），修一处即可 → **不适用并行**，串行调查。

---

### 10. verification-before-completion（完成前验证）

**铁律：**

```
没有新鲜的验证证据，不得声称完成
```

**声明完成前必须执行的门禁：**

1. 确定"哪条命令能证明这个声明"
2. **当场运行**这条命令（不能用上次的结果）
3. 读完整输出，检查退出码，数失败条数
4. 输出确认无误后，才能声明

**常见失败场景：**

| 声明 | 必须做的验证 | 不够的做法 |
|------|-------------|-----------|
| 测试通过 | 运行测试命令，看到 0 failures | 上次运行结果 |
| 构建成功 | 运行构建命令，退出码为 0 | Lint 通过 |
| Bug 已修复 | 重现原症状，测试通过 | 代码已改动 |
| 需求已满足 | 逐条对照 Plan 核查 | 测试通过即可 |

**红色警告词（出现即 STOP）：**
- "应该可以了"
- "看起来没问题"
- "大概通过了"
- "Done!"、"完成！"（在运行命令之前）

**触发时机（任何"正面状态断言"之前）：**

| 场景 | 举例 |
|------|------|
| 声称任务完成 | "Task 3 已完成"、"登录功能实现好了" |
| 表达满意/成功 | "搞定！"、"一切正常" |
| 准备提交代码 | `git commit`、`git push` |
| 准备创建 PR | `gh pr create` |
| 标记 Task 为 completed | TodoList 状态 in_progress → completed |
| 移到下一个 Task | "Task 2 通过了，开始 Task 3" |
| 子代理返回成功报告 | 子代理说"全部通过" → 不能直接信，要自己验 |

**对比示例：**
```
❌ AI 改完代码 → "Bug 已修复！" → 实际没测 → 线上又炸
✅ AI 改完代码 → 运行 mvn test → 看到 "Tests: 47, Failures: 0"
   → 退出码 0 → "Bug 已修复。验证：47 个测试通过，退出码 0。"
```

> **一句话：嘴巴说话之前，先让命令行说话。**

---

### 11. requesting-code-review（请求代码审查）

**必须审查的时机：**
- 每个 Task 完成后
- 重大功能完成后
- 合并到 main 前

**操作步骤：**
```bash
# 1. 获取 git SHA
BASE_SHA=$(git rev-parse HEAD~1)
HEAD_SHA=$(git rev-parse HEAD)

# 2. 派遣 code-reviewer 子代理审查
# 3. 按反馈严重性处理
```

**反馈处理规则：**

| 级别 | 处理方式 |
|------|----------|
| Critical | 立即修复，修完才能继续 |
| Important | 继续下一步之前必须修复 |
| Minor | 记录，稍后处理 |

---

### 12. receiving-code-review（接收代码审查）

**核心原则：** 技术评估，不是情绪表演。

**响应流程：**
```
读完全部反馈（不要边读边反应）
    → 用自己的话复述需求（或提问澄清）
    → 对照代码库验证建议
    → 技术评估是否合理
    → 技术性回应或有理由地推回
    → 逐条实施（每条单独测试）
```

**绝对禁止的回应：**
- "你说得对！" / "很好的建议！"（奉承式）
- "好的，马上实现" （未验证就承诺）

**正确的回应方式：**
- 复述技术需求后直接行动
- 有理有据地推回（当建议确实有误时）
- "已修复。[简述改了什么]"

**何时应该推回：**

- 建议会破坏现有功能
- 审查者缺少完整上下文
- 违反 YAGNI（添加没人用的功能）
- 技术上对当前技术栈不适用

---

### 13. finishing-a-development-branch（完成开发分支）

**定位：** 所有任务完成后的标准化收尾流程。

**四步流程：**

1. **验证测试**（先决条件）
   ```bash
   npm test / pytest / cargo test / go test ./...
   ```
   测试失败 → 停止，必须先修

2. **确认基础分支**
   ```bash
   git merge-base HEAD main
   ```

3. **提供 4 个选项**（固定格式）
   
   ```
   1. 本地合并到 <base-branch>
   2. Push 并创建 Pull Request
   3. 保留分支（稍后自行处理）
   4. 丢弃本次工作
   ```
   
4. **执行选择 + 清理 worktree**
   - 选项 1/2/4：自动清理 worktree
   - 选项 3：保留 worktree
   - 选项 4：需输入 `discard` 确认，防止误操作

---

## 四、完整开发流程时序

```
用户提出需求
    │
    ▼
[using-superpowers] 评估并调度
    │
    ├─→ [brainstorming] 梳理需求，产出 Spec
    │
    ├─→ [writing-plans] 拆解为 Plan
    │
    ├─→ [using-git-worktrees] 创建隔离工作分支
    │
    └─→ [subagent-driven-development] 启动计划执行
              │
              └─ Per Task 循环：
                    │
                    ├─→ [test-driven-development] 先写测试再实现
                    │
                    ├─→ [systematic-debugging] 遇阻时找根因（可选）
                    │
                    ├─→ [dispatching-parallel-agents] 多处独立故障（可选）
                    │
                    ├─→ [verification-before-completion] 带证据声明完成
                    │
                    ├─→ [requesting-code-review] 发起代码审查
                    │
                    └─→ [receiving-code-review] 处理审查反馈（有反馈时）
              │
              ▼ 所有 Task 通过
    [finishing-a-development-branch] 验证→选择→合并/PR→清理
```

---

## 五、三大铁律汇总

| 铁律 | 技能 | 违反后果 |
|------|------|----------|
| **没有失败的测试，就不写生产代码** | test-driven-development | 删掉已写代码，重来 |
| **不找到根因，不提修复方案** | systematic-debugging | 继续调查，禁止猜测 |
| **没有验证证据，不得声称完成** | verification-before-completion | 运行命令，取得证据后再说 |

---

## 六、安装命令速查

```bash
# 安装全套（13个）
npx --yes skills add obra/superpowers@using-superpowers -g -y
npx --yes skills add obra/superpowers@brainstorming -g -y
npx --yes skills add obra/superpowers@writing-plans -g -y
npx --yes skills add obra/superpowers@using-git-worktrees -g -y
npx --yes skills add obra/superpowers@executing-plans -g -y
npx --yes skills add obra/superpowers@subagent-driven-development -g -y
npx --yes skills add obra/superpowers@test-driven-development -g -y
npx --yes skills add obra/superpowers@systematic-debugging -g -y
npx --yes skills add obra/superpowers@dispatching-parallel-agents -g -y
npx --yes skills add obra/superpowers@verification-before-completion -g -y
npx --yes skills add obra/superpowers@requesting-code-review -g -y
npx --yes skills add obra/superpowers@receiving-code-review -g -y
npx --yes skills add obra/superpowers@finishing-a-development-branch -g -y
```

---

*整理时间：2026年4月22日*
*技能来源：https://github.com/obra/superpowers*
