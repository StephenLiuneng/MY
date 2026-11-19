---
name: wjx-plan-to-doc
description: Turn confirmed WJX requirements into reviewable OpenSpec proposal, specifications, design, and tasks, or revise those artifacts together. Use after discovery confirmation or for a requested plan revision. Stops for approval of the concrete plan before implementation.
---

# WJX Plan to Doc

先读 [共享约定](../wjx-dev/references/contract.md)。本阶段只创建或修订方案资料，不修改业务代码。

## 复用共识和设置

- 核对确认 A 覆盖的目标、范围、验收条件和资料写入位置；缺少实质性决策时回到 [wjx-askme](../wjx-askme/SKILL.md)，不要重问已经确认的内容。
- 只有共识但尚未允许写资料时，展示已知结论并补充该确认；不要从“我觉得可以”之类脱离上下文的句子推断授权。
- 确认实际仓库和 OpenSpec 根、schema、现有 change。仅在确认 A 已包含设置时执行必要的最小初始化；保留现有全局技能和项目规则。声明的 Store 有问题时先解决，不偷偷改成仓库内资料。
- 按 [创建与修订方案资料](references/artifacts.md) 直接使用 OpenSpec CLI。新需求创建 change；同一需求修订同一套资料，不重复访谈或创建第二个 change。

## 形成可实施的资料

遵从 CLI 返回的 schema、模板、文件路径与依赖顺序。默认 spec-driven 通常包括 proposal、增量 specs、design、tasks；其他 schema 按实际约定，不补造已明确跳过的材料。

- proposal 说明问题、触发场景、范围和影响；规范表达可观察行为及验收场景，包含当前需求涉及的异常与边界。
- design 基于真实代码链路说明改动位置、接口和重要取舍。只有会影响用户行为或长期维护的选择才需要比较方案，不为凑数制造替代方案。
- 涉及异步、状态或多入口时，定义状态所有者、业务身份、失效事件、允许副作用的条件和收口路径；UI、协议等专项约束读取当前项目规则和适用 Skills，不复制旧项目清单。
- tasks 划分可验证的实施步骤，并明确必要的验证任务、执行者和前提。需要指定会话或真实设备的项目，不能把待验事项写成当前会话已能执行的承诺。
- 沿用同一个 change，规范、设计与任务彼此一致。合理实施细节可记录建议，但未决定的重要行为不能伪装成用户已批准要求。

## 检查并请求确认 B

1. 检查资料之间是否有矛盾、遗漏或范围扩大，执行适用的 OpenSpec 结构校验和差异检查。资料验证不触发宿主构建或 Run。
2. 在聊天中自包含展示方案摘要：目标与范围、当前链路及证据、关键设计、受影响文件或模块、实施顺序、验证办法和待决事项，并链接真实资料。
3. 明确询问是否按这版方案开始实施，然后停下等待答复。即使最初要求“直接帮我开发”，也不能跳过用户选择的方案确认点。

收到当前版本的明确实施确认后，完整流程转交 [wjx-execute](../wjx-execute/SKILL.md)。若用户提出修订，更新同一套资料、展示受影响部分，再确认修改后的方案；不要求重新确认未变的需求。
