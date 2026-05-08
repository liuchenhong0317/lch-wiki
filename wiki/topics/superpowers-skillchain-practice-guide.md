<!--
 @AI-Generated: true
 @AI-Model: GitHub Copilot
 @Summary: 累计AI新增88行/修改0行/删除0行; 总行数88行
 @AI-LastModified: 2026-04-27 11:13:37
-->

---
title: Superpowers 技能链实操指南
created: 2026-04-27
updated: 2026-04-27
tags: [专题, Superpowers, 实操, Agent模式, 培训]
sources: [Superpowers技能培训课堂讲义.md, Superpowers技能链实操跟练手册.md]
type: topic
---

# Superpowers 技能链实操指南

本文将两份 Superpowers 培训材料整合为可直接执行的课堂实操 SOP，用于 AI 编程培训中的演示、跟练与评估。

> 来源：[[sources/Superpowers技能培训课堂讲义|Superpowers 技能培训课堂讲义]]
> 来源：[[sources/Superpowers技能链实操跟练手册|Superpowers 技能链实操跟练手册]]

---

## 一、实操目标

通过一个可复现的开发场景，让学员理解并实践以下能力：

1. 识别何时触发 [[concepts/superpowers-skills|Superpowers 技能体系]]
2. 按流程执行“澄清需求 → 写计划 → 实现 → 验证 → 评审 → 收尾”
3. 将“三大铁律”内化为日常开发门禁

---

## 二、适用对象与场景

| 对象 | 典型使用场景 | 训练重点 |
|------|--------------|----------|
| 新手开发者 | 从“直接写代码”转向流程化开发 | 触发顺序与执行纪律 |
| 团队骨干 | 建立团队统一 AI 开发范式 | 质量门禁与审查闭环 |
| 培训讲师 | 课堂演示与实操考核 | 可复用脚本与评分标准 |

---

## 三、前置环境

- 平台：[[entities/github-copilot|GitHub Copilot]] + [[entities/vscode|VS Code]]
- 技能：[[entities/superpowers|Superpowers]] 相关技能已安装
- 项目：准备一个包含基线测试的 demo 项目（建议 Python/Node 任一）

最小检查项：

1. `git status` 工作区干净
2. 基线测试可通过
3. 能正常在对话中触发技能

---

## 四、标准实操流程（课堂版）

### Step 1：输入模糊需求

示例：`用户登录失败太多次后要锁定账户`

目标：触发流程入口而不是直接编码。

### Step 2：需求澄清与规格化

围绕“失败阈值、锁定时长、成功后计数清零、提示语与状态码”等关键点进行澄清，并形成可执行规格。

### Step 3：将规格拆解为任务计划

按 Task 粒度拆解步骤，要求每步包含：

- 目标文件
- 先失败测试
- 最小实现
- 验证命令

### Step 4：隔离环境执行

使用 worktree 或独立分支执行计划，先跑基线测试，再逐 Task 推进。

### Step 5：问题定位与修复

遇到异常时坚持根因调查，不进行猜测式修改。

### Step 6：完成前验证与代码审查

在声明完成前必须运行验证命令；随后执行审查反馈闭环。

### Step 7：分支收尾

根据团队策略进行本地合并或 PR 流程，并清理工作区。

---

## 五、课堂时间建议（90 分钟）

| 阶段 | 时长 | 产出 |
|------|------|------|
| 流程讲解 | 15 分钟 | 技能链全景认知 |
| 演示 1 轮 | 25 分钟 | 一次完整链路示范 |
| 学员跟练 | 35 分钟 | 小组完成同题实践 |
| 复盘评估 | 15 分钟 | 问题清单 + 改进项 |

---

## 六、验收清单（可评分）

### A. 触发与流程（40 分）

- 是否先进行需求澄清
- 是否先有计划再执行
- 是否按阶段推进而非跳步

### B. 质量门禁（40 分）

- 是否严格执行先失败测试
- 是否先找根因再修复
- 是否先验证命令再声明完成

### C. 输出质量（20 分）

- 任务记录清晰可追溯
- 审查反馈处理完整
- 收尾动作规范

---

## 七、与现有知识页的关系

- 技能原理：[[concepts/superpowers-skills|Superpowers 技能体系]]
- 技能标准：[[concepts/copilot-skills|Copilot Skills]]
- 平台实体：[[entities/superpowers|Superpowers]]、[[entities/github-copilot|GitHub Copilot]]、[[entities/vscode|VS Code]]
- 课堂原始材料：[[sources/Superpowers技能培训课堂讲义]]、[[sources/Superpowers技能链实操跟练手册]]

---

## 八、培训落地建议

1. 每次培训固定一个“模糊需求”，便于横向比较班级效果。
2. 将“是否提供验证证据”设为一票否决项。
3. 课后把优秀实操对话沉淀为新的专题页，持续完善培训 Wiki。
