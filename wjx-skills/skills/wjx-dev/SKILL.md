---
name: wjx-dev
description: Coordinate WJX's personal feature workflow across code projects. Use when a new feature needs a workflow choice, when the user chooses the WJX workflow, or when continuing one of its stages. Route discovery, planning, execution, Open Code Review, and acceptance without repeating settled decisions.
---

# WJX Dev

这是个人开发流程的总入口，适用于所有代码项目。先读 [共享约定](references/contract.md)，再只加载当前阶段所需的 Skill。

## 选择与续接

- 对新的业务功能、页面或明显的能力扩展，若用户尚未选择工作方式，先询问一次：“这个新需求是否使用 WJX 开发流程？会先澄清需求并请你确认，再写方案请你确认，之后执行、验证和归档。”提供“使用 WJX 流程”和“按现有方式处理”两个选项。
- 等待选择期间可只读调查，不写方案、代码或 OpenSpec 配置。用户拒绝后按当前项目常规方式完成本次需求，不继续自动触发本套阶段。
- 用户已经选用 WJX、直接调用某个 WJX Skill，或正在继续同一个 WJX 需求时，不再询问工作方式。明确要求原版 OpenSpec、其他流程或直接修复时遵从用户选择。
- 纯问答、问题诊断、既有 Bug 修复、局部文案或样式调整不主动推荐整套流程；用户主动选用时可以使用。
- 从当前聊天、用户指定的交接材料和同一个 change 恢复进度。先确认真正的代码仓库、OpenSpec 根目录、当前资料和已有确认，不能因换聊天而重建 change，也不能把文件存在当作已经确认。

## 阶段路由

| 当前情况 | 加载 | 完成后的去向 |
| --- | --- | --- |
| 需求或重要取舍未达成共识 | [wjx-askme](../wjx-askme/SKILL.md) | 确认点 A：需求共识与写方案范围 |
| 需求已确认，需要创建或修订方案 | [wjx-plan-to-doc](../wjx-plan-to-doc/SKILL.md) | 确认点 B：审阅具体方案后允许实施 |
| 当前方案已确认实施 | [wjx-execute](../wjx-execute/SKILL.md) | 完成可执行任务后进入 review |
| 代码已实现，需要审查或复查 | [wjx-review](../wjx-review/SKILL.md) | OCR 审查与需求核对，修复后复查受影响范围 |
| 当前实现已审查，需要验证或继续收尾 | [wjx-finish](../wjx-finish/SKILL.md) | 验证完成并满足条件后同步、归档 |

完整顺序：ASKME → 确认 A → PLAN-TO-DOC → 确认 B → EXECUTE → REVIEW → FINISH。

两个确认点必须针对可审阅的结果；已覆盖当前版本的明确确认不再重问。只请求某一阶段时完成该阶段即可，不把阶段调用扩展成整套开发授权。实现后发现需求或重要方案变化，回到受影响的阶段，保留已经确认且仍有效的内容。

## 对用户交接

每次交接简要说明正在使用的 change、已完成内容、下一阶段，以及确实需要用户决定或确认的事项。不要要求用户背诵底层 OpenSpec 命令。必要验证待其他会话或设备执行时，清楚交接所需证据，保留 change 活跃。
