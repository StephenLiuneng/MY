---
name: wjx-execute
description: Implement the current, explicitly approved WJX OpenSpec plan in complete slices and keep its task progress accurate. Use for execution or resuming an approved change. Does not infer plan approval from existing documents or bypass project validation ownership.
---

# WJX Execute

先读 [共享约定](../wjx-dev/references/contract.md) 和 [CLI 与路径约定](../wjx-dev/references/openspec-cli.md)，直接按当前 apply instructions 执行下列任务流程。

## 实施前

- 确认原请求包含实施，并能定位当前方案的确认 B。没有确认时先读现有资料，展示待审方案并请求确认，不因文件存在、任务已经勾选或 change 名字相同而开始修改。
- 读取适用项目规则，确认 Git 工作区、用户已有改动和实际编译输入。通过 OpenSpec status 与 apply instructions 定位真实资料、任务和上下文，遵从工具报告的 blocked 状态，不绕过缺失材料。
- 方案在确认后发生重要改变时回到 [wjx-plan-to-doc](../wjx-plan-to-doc/SKILL.md) 处理受影响部分；只是继续未完成任务且方案未变时复用确认，不重开访谈。

## 按任务推进

- 以产生可观察行为的完整小步骤实施，沿用项目已有能力，保留用户改动。不把范围外的重构、删功能或换依赖混进当前需求。
- 涉及状态、回调或异步流程时遵从已确认设计的身份、失效和副作用条件，覆盖实际入口；发现设计缺口时按影响回到规划，不靠临时假设降低行为要求。
- 按当前项目选择适用的实现和检查工具。测试应证明用户行为或有效边界，复用已有定向检查，不为完成步骤数量制造测试。
- 更新任务前核对 CLI 返回的 `sourcePath` 与 `line` 仍指向该任务；有漂移就重新读取 instructions。仅完成的任务勾选，并重新读取进度确认结果。
- 必要的跨会话验证、构建或设备任务尚不具备执行条件时保持未完成，并记录所需交接。不能为了让 apply 循环清零而自行启动受限验证，或把这些任务从清单删除。
- 普通失败在当前授权范围内调查并修正；需要改变需求、重要设计或权限范围时，说明证据并交回相应确认点。

## 转入 Review

完成允许的实施和局部检查后，说明已改内容、任务进度、当前源码依据和待验事项。完整 WJX 流程继续进入 [wjx-review](../wjx-review/SKILL.md)，无需再问是否开始 Review；只请求实施时按原范围交接。修复 Review 发现的问题后回到该 Review 的受影响范围复查，避免重新启动整条流程。
