<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增262行/修改0行/删除0行; 总行数262行
 @AI-LastModified: 2026-04-22 11:19:50
-->

# Superpowers 技能链跟练方案

> 通过一个完整的"登录失败锁定"需求，逐步学习 11 个技能的触发过程

---

## 一、目标

用一个 20-30 分钟的真实开发场景，来学习每个 Superpowers 技能何时被触发、产出什么、为什么比"直接写代码"更好。

---

## 二、演示环境

### 项目结构

```
demo-project/
├── src/
│   ├── models/user.py           # User 模型 + UserRepository
│   ├── services/auth_service.py  # 登录逻辑（含 datetime.now() 时区陷阱）
│   ├── api/auth_controller.py    # HTTP 接口层
│   └── exceptions.py            # 自定义异常
├── tests/
│   ├── conftest.py              # 测试 fixtures（3 个用户）
│   └── test_auth.py             # 基线测试（11 条，全部通过）
├── requirements.txt
└── pytest.ini
```

### 基线状态

- 11 条测试全部通过
- 现有功能：登录成功/失败、禁用账户检查
- **埋设陷阱：** `auth_service.py` 第 42 行使用 `datetime.now()`（本地时间），后续添加锁定功能时会与 UTC 时间比较产生偏差

### 输入（故意模糊的一句话需求）

> "用户登录失败太多次后要锁定账户"

---

## 三、脚本（9 幕）

### 第 1 幕：触发 using-superpowers（总调度器）

**操作：** 在新对话中输入需求

**预期可见标志：**

- AI 的第一个动作**不是写代码**
- 输出中出现类似："检查适用技能... 命中 brainstorming，先加载"

**要点：**

| 没有此技能 | 有此技能 |
|-----------|---------|
| AI 直接开始写代码 | AI 先检查流程，按规范走 |
| 需求不清楚就猜 | 需求不清楚就问 |

**注意：**

> "注意看，AI 收到需求后没有直接动手。using-superpowers 作为总调度器，会先判断应该走哪个技能流程。这里它判断出这是一个新功能需求，所以先调度了 brainstorming。"

---

### 第 2 幕：触发 brainstorming（头脑风暴）

**预期可见标志：** AI 开始**反问**，而不是动手

预期追问的问题：

| # | AI 的追问 | 建议回答 |
|---|----------|---------|
| 1 | 失败几次触发锁定？ | 5 次 |
| 2 | 锁定多久？永久还是临时？ | 临时锁定 15 分钟 |
| 3 | 登录成功后是否清零失败计数？ | 是 |
| 4 | 锁定期间登录提示什么？ | 返回 423 状态码 + 剩余锁定时间 |
| 5 | 需要管理员手动解锁吗？ | 本期不做，标注 out-of-scope |

**产出物：** `docs/superpowers/specs/login-lockout-spec.md`

**要点：**

> "如果跳过这一步直接写代码，'锁定多久？计数器何时清零？' 这些问题会在写到一半时才暴露，导致返工。brainstorming 把这些问题前置了。"

**关于 Spec 审查子代理：**
Spec 写完后，brainstorming 会自动派遣一个审查子代理，按 5 个维度检查：

| 维度 | 检查内容 |
|------|---------|
| 完整性 | 是否有 TODO、占位符、未完成章节 |
| 一致性 | 是否有内部矛盾 |
| 清晰度 | 是否有歧义到可能导致实现错误的需求 |
| 范围 | 是否聚焦于单个功能 |
| YAGNI | 是否存在未被请求的过度设计 |

---

### 第 3 幕：触发 writing-plans（编写计划）

**预期可见标志：** 生成包含完整代码的实施计划

**产出物：** `docs/superpowers/plans/2026-04-22-login-lockout.md`

**预期 Plan 结构：**

```
Task 1: 扩展 User 模型
  - 新增字段: failed_attempts (int), locked_until (datetime)
  - Step 1: 写测试验证新字段默认值 → 跑红
  - Step 2: 添加字段 → 跑绿
  - Step 3: 提交

Task 2: 实现锁定逻辑
  - 修改 auth_service.py 的 login() 方法
  - Step 1: 写测试 - 第6次登录失败应抛异常 → 跑红
  - Step 2: 写测试 - 锁定期间登录应抛异常 → 跑红
  - Step 3: 实现锁定逻辑 → 跑绿
  - Step 4: 提交

Task 3: API 层返回 423 状态码
  - 修改 auth_controller.py
  - Step 1: 写测试 - 锁定状态返回 423 → 跑红
  - Step 2: 添加异常捕获 → 跑绿
  - Step 3: 提交
```

**要点：**

> "注意每个步骤都包含完整代码和预期结果，没有 TODO 和占位符。这是为了让执行者（无论是 AI 还是人）零上下文就能跟着做。"

---

### 第 4 幕：触发 using-git-worktrees（Git 隔离工作区）

**预期可见标志：** 终端中看到以下命令执行

```bash
git worktree add .worktrees/login-lockout -b feat/login-lockout
cd .worktrees/login-lockout
pip install -r requirements.txt
pytest -v   # 基线测试 → 11 passed, 0 failed
```

**要点：**

> "创建隔离工作分支后，先跑一次基线测试。11 条全绿 = 干净起点。后续任何红色测试都是我们自己引入的，不会和别人的改动混淆。"

**注意事项：**

- 会自动检查 `.gitignore` 是否包含 `.worktrees/`
- 若未包含 → 自动添加并提交，防止 worktree 内容意外入库

---

### 第 5 幕：触发 executing-plans + test-driven-development（红绿循环）

**预期可见标志：** 终端中出现经典的 RED → GREEN 循环

**Task 1 示例（扩展 User 模型）：**

```
[Task 1, Step 1] 写测试: test_user_has_failed_attempts_field
$ pytest tests/test_auth.py::TestUserLockoutFields::test_user_has_failed_attempts_field
→ FAILED ❌  (RED — 字段还不存在)

[Task 1, Step 2] 在 User.__init__ 中添加 self.failed_attempts = 0
$ pytest tests/test_auth.py::TestUserLockoutFields::test_user_has_failed_attempts_field
→ PASSED ✅  (GREEN — 字段已添加)
```

**Task 2 示例（锁定逻辑）：**

```
[Task 2, Step 1] 写测试: test_account_locks_after_5_failures
$ pytest tests/test_auth.py::TestLoginLockout::test_account_locks_after_5_failures
→ FAILED ❌  (RED — 锁定逻辑还不存在)

[Task 2, Step 3] 在 login() 中添加失败计数 + 锁定判断
$ pytest tests/test_auth.py::TestLoginLockout -v
→ 3 passed ✅  (GREEN — 所有锁定测试通过)
```

**要点：**

> "为什么必须先看到红色？因为如果测试一开始就绿了，说明这个测试根本没在测你想测的东西——它可能写错了条件，或者测了已有功能。"

---

### 第 6 幕：触发 systematic-debugging（时区陷阱爆发）

**触发时机：** Task 2 实现锁定逻辑后，运行测试出现诡异结果

**预期可见标志：**

```
test_account_locks_after_5_failures      → PASSED ✅
test_locked_account_rejects_login        → PASSED ✅
test_account_unlocks_after_15_minutes    → FAILED ❌
  AssertionError: Expected login to succeed, but got AccountLockedException
  locked_until = 2026-04-22 18:30:00   ← 本地时间 (UTC+8)
  now          = 2026-04-22 10:30:00   ← UTC 时间
```

**AI 进入四阶段调查（而非直接猜测修复）：**

| 阶段 | AI 的操作 | 可见输出 |
|------|----------|---------|
| **1. 根因调查** | 读错误信息，检查时间值 | "locked_until 和 now 差了 8 小时，怀疑时区问题" |
| **2. 形成假说** | 检查代码中的时间函数 | "发现 datetime.now()（本地）和 datetime.utcnow()（UTC）混用" |
| **3. 验证假说** | 加诊断日志确认 | 打印两个时间值，确认 8 小时差异 |
| **4. 修复并验证** | 统一为 `datetime.now(timezone.utc)` | 重跑测试，全绿 |

**要点：**
> "这个 Bug '看起来很明显'，但 systematic-debugging 技能禁止直接猜。为什么？因为如果你只改了新代码中的一处 `utcnow()`，却忘了原有的 `datetime.now()` 也需要改，Bug 会在生产环境以更隐蔽的方式爆发。四阶段调查逼着你查全面。"

---

### 第 7 幕：触发 verification-before-completion（完成前验证）

**触发时机：** 所有代码修改完成，AI 准备声明 Task 通过

**预期可见标志：** AI **不会直接说"搞定了"**，而是先运行命令

```bash
$ pytest tests/test_auth.py -v
tests/test_auth.py::TestAuthServiceLogin::test_login_success_returns_token       PASSED
tests/test_auth.py::TestAuthServiceLogin::test_login_success_updates_last_login  PASSED
tests/test_auth.py::TestAuthServiceLogin::test_login_wrong_password_raises       PASSED
tests/test_auth.py::TestAuthServiceLogin::test_login_nonexistent_user_raises     PASSED
tests/test_auth.py::TestAuthServiceLogin::test_login_disabled_account_raises     PASSED
tests/test_auth.py::TestAuthServiceLogin::test_multiple_successful_logins        PASSED
tests/test_auth.py::TestLoginLockout::test_account_locks_after_5_failures        PASSED
tests/test_auth.py::TestLoginLockout::test_locked_account_rejects_login          PASSED
tests/test_auth.py::TestLoginLockout::test_account_unlocks_after_15_minutes      PASSED
tests/test_auth.py::TestLoginLockout::test_login_success_resets_counter          PASSED
tests/test_auth.py::TestAuthController::test_login_returns_200_on_success        PASSED
tests/test_auth.py::TestAuthController::test_login_returns_401_on_wrong_password PASSED
tests/test_auth.py::TestAuthController::test_login_returns_403_on_disabled       PASSED
tests/test_auth.py::TestAuthController::test_login_returns_423_on_locked         PASSED
tests/test_auth.py::TestAuthController::test_login_returns_400_on_empty_fields   PASSED
tests/test_auth.py::TestAuthController::test_login_returns_400_on_missing_fields PASSED
==================== 16 passed in 0.05s ====================
```

然后才声明：
> "Task 完成。验证：16 个测试全部通过，退出码 0。"

**要点 — 对比：**

| ❌ 没有此技能 | ✅ 有此技能 |
|--------------|-----------|
| AI 改完代码 → "Bug 已修复！" | AI 改完代码 → 运行 pytest |
| 实际没测 → 线上可能再炸 | 看到 "16 passed, 0 failed" → 才声明 |

> **一句话：嘴巴说话之前，先让命令行说话。**

---

### 第 8 幕：触发 requesting-code-review + receiving-code-review（代码审查）

**预期可见标志：** 派遣审查子代理，返回分级反馈

**可能的审查反馈示例：**

| 级别 | 反馈内容 | AI 的处理 |
|------|---------|----------|
| **Important** | `locked_until` 字段建议加数据库索引 | 立即添加索引注释/迁移 |
| **Minor** | 错误消息不要暴露剩余锁定秒数（安全风险） | 记录，不阻塞 |

**要点：**
> "注意 AI 收到 Important 级别反馈后没有直接说'好的马上改'，而是先对照代码验证建议是否合理，然后才实施。这就是 receiving-code-review 的核心——技术评估，不是盲从。"

---

### 第 9 幕：触发 finishing-a-development-branch（收尾）

**预期可见标志：** 弹出 4 选项菜单

```
所有任务完成，请选择：
1. 本地合并到 main
2. Push 并创建 Pull Request
3. 保留分支（稍后自行处理）
4. 丢弃本次工作
```

**操作：** 选择选项 1（本地合并）

**预期终端输出：**
```bash
$ pytest -v                    # 全局测试验证
$ git checkout main
$ git merge feat/login-lockout
$ git worktree remove .worktrees/login-lockout
$ git branch -d feat/login-lockout
```

**要点：**
> "收尾不是随便 merge 就完。finishing-branch 会先跑全量测试确认无回归，然后提供标准化选项，最后自动清理 worktree。选项 4（丢弃）还有二次确认防误操作。"

---

## 四、技能触发检查清单

演示过程中，逐项打勾确认每个技能都被可见触发：

| # | 技能 | 可见标志 | ✓ |
|---|------|---------|---|
| 1 | using-superpowers | AI 第一句提到"检查适用技能" | ☐ |
| 2 | brainstorming | AI 反问 4-5 个澄清问题 | ☐ |
| 3 | writing-plans | 生成含完整代码的 Plan 文件 | ☐ |
| 4 | using-git-worktrees | 终端看到 `git worktree add` + 基线测试全绿 | ☐ |
| 5 | executing-plans | 逐 Task 标记状态切换 | ☐ |
| 6 | test-driven-development | 终端看到 RED → GREEN 循环 | ☐ |
| 7 | systematic-debugging | 时区 Bug 触发四阶段调查 | ☐ |
| 8 | verification-before-completion | 运行 pytest 取证后才声明完成 | ☐ |
| 9 | requesting-code-review | 派遣审查子代理 | ☐ |
| 10 | receiving-code-review | 按级别处理反馈 | ☐ |
| 11 | finishing-a-development-branch | 弹出 4 选项 + 清理 worktree | ☐ |

---

## 五、演示前准备事项

1. **确认基线测试通过**
   ```bash
   cd demo-project && pytest -v
   # 应看到 11 passed, 0 failed
   ```

2. **初始化 Git 仓库**（如果尚未初始化）
   ```bash
   cd demo-project
   git init
   git add .
   git commit -m "init: 登录模块基线代码"
   ```

3. **确认 Superpowers 技能已安装**
   ```bash
   ls ~/.agents/skills/
   # 应看到 13 个技能目录
   ```

4. **开启新对话**（确保干净上下文）

5. **输入演示需求**
   > "用户登录失败太多次后要锁定账户"

## 

---

*整理时间：2026年4月22日*
*配套项目：demo-project/*
