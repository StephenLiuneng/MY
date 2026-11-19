---
name: wjx-askme
description: Clarify an unsettled coding feature through grilling decision interviews and evidence gathering. Use for WJX discovery or when the user asks to question a requirement before planning. Produces a shared understanding for confirmation, not project files or code.
---

# WJX AskMe

先读 [共享约定](../wjx-dev/references/contract.md)。本阶段将查事实与问决策放在同一个循环中，共用一份结论。

读取当前安装的 `grilling`，按依赖分轮追问；代码调查、技术选项比较与未知项识别按下文直接执行，不依赖原版 explore Skill。需要读取已有 OpenSpec 资料时使用 [CLI 与路径约定](../wjx-dev/references/openspec-cli.md)。

## 建立问题与证据

- 理解用户目标，读取当前项目规则、相关代码和可获得的资料。已有 OpenSpec 根时，按需读取相关主规范、change 和配置；没有根也可以先调查，不在此时初始化。
- 对每个影响目标或验收的未决问题，区分“可查证的事实”与“用户需要做出的决定”。事实从源码、文档、测试、日志或工具调查，不让用户替 AI 查文件。
- 代码事实足以回答的问题直接给出结论与位置。证据缺失或互相冲突时保留不确定性，不用推测填满需求。只加载与当前问题有关的资料。
- 在当前环境允许且值得分工时，可委派独立的只读事实调查；用户决策仍由主会话汇总提出，调查未完成的前提不会被当成已知事实。

## 调查与追问交替

1. 按决策依赖展开当前需求：上游未决定时，不先问依赖它的细节。
2. 每轮集中询问当前可以独立回答的业务决定，遵循 grilling 的问题格式，给出有证据支持的推荐及其理由。不能查到的产品目标、范围和取舍由用户决定。
3. 用户回答后更新已定结论，调查新出现的技术问题，再进入下一轮。代码调查与技术选项比较持续服务于这些决策，不单独重启 explore 访谈。
4. 已回答且未受新事实影响的问题不再问；能由已定要求推导的常规实现细节交给方案阶段。只展开影响本次范围或验收的分支，不无限扩展假设需求。

## 确认 A

关键决策已明确后，简要列出目标、范围与不做事项、重要业务决定、验收条件、相关事实与证据，以及仍存在的限制。存在影响实施的实质性未决项时先解决或明确缩小范围，不能称为已达成共识。

对要求继续规划的任务，确认真实目标根目录，并明确提出：“以上需求理解是否正确，是否据此在指定位置生成 OpenSpec 需求、设计和任务资料？”未初始化时同时说明初始化位置和最小范围。等待明确答复后转交 [wjx-plan-to-doc](../wjx-plan-to-doc/SKILL.md)。

用户只要求讨论或压力测试时，交付结论即可。确认 A 前不写项目文件；普通问题的回答不代替最终共识确认。用户已提供同一需求的明确确认及可定位结论时直接复用，不重新访谈。
