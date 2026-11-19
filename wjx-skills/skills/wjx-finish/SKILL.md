---
name: wjx-finish
description: Complete authorized validation of a reviewed WJX change, resolve acceptance failures, and synchronize and archive only when required acceptance is complete. Use for WJX delivery or resuming pending acceptance; route code review to wjx-review and respect validation-only scope.
---

# WJX Finish

先读 [共享约定](../wjx-dev/references/contract.md)。本阶段复用当前 Review 结果，负责实际验证与资料收口；Review、运行验收与规范同步各自的结果不能互相替代。

## 核对当前实现

1. 确认本次范围是完整收尾、只验证还是只 Review；定位同一个仓库、change、已确认方案及当前 HEAD 和相关 diff。
2. 完整收尾时复用同一范围且匹配当前源码的 [wjx-review](../wjx-review/SKILL.md) 结果；缺失或已失效时先完成对应审查。不要机械重跑全部 OCR。只要求 Review 则交给该阶段并在报告后停止；只要求验证则保持验证范围。
3. 检查未解决问题、任务状态和待验事项。完整收尾请求允许按 [wjx-execute](../wjx-execute/SKILL.md) 修复已批准范围内的问题，随后复查受影响内容并重跑必要检查；只验证请求不自动授权修复。影响需求或重要设计的修改回到 PLAN-TO-DOC。

## 实际验证

- 按已确认方案的必要验收项和项目规则选择检查。先确认是否被指定执行构建、测试、安装、Run 或设备验收；遵从资源占用和磁盘要求。不能因 skill 名叫 finish 就自授验证职责。
- 复用证据前核对源码版本、相关 diff、构建输入和运行对象；源码已变、仅有旧产物或证据无法对应时，该项仍待验证。
- 区分结构检查、源码审查、编译链接、自动化测试和真实运行证据。只报告实际执行与观察到的结果；方案不需要的可选材料或场景标记不适用，不扩大必要验收范围。
- 确认所有适用且必要的验收任务后再勾选相应任务。缺少设备、执行职责或外部条件时，完成仍可执行的检查，给出明确待验项和交接依据，保留 change 活跃。

## 同步和归档

仅当当前请求包含收尾、相关问题已经解决、必要任务和验证完成时进入。完整流程在确认 B 后已经包含满足条件的同步与归档；单独的验证或 Review 请求不包含。

- 按 [同步与归档](references/sync-and-archive.md) 直接执行当前 CLI 状态检查、增量合并、校验和目录归档，复用同一次规范规则快照，不重复同步。
- 先展示本次已批准增量的同步范围。按已确认的完整流程执行，避免重复问同一授权；出现额外需求删除、未覆盖范围或真实冲突时单独确认。
- 同步须完成并验证成功后才能归档，不能后台并行同步后立即移动目录。同步失败、主规范不一致、必要验收未完成或归档目标冲突时停止归档，不跳过错误或降低要求。
- 归档后确认主规范同步结果、实际归档位置和活动变更状态。收尾不自动包含 Git 提交、push、发布或通知他人。

## 交付

遵循项目交付格式，说明实现结果、关键证据、Review 与实际验证、未验证限制及资料位置。归档成功才写已归档；仍有必要验收待完成时明确写待验证，并给出下次可以继续使用的仓库、change 和待验内容。
