---
name: wjx-review
description: Review a WJX implementation or an explicitly requested diff with Open Code Review (ocr), then verify findings against requirements and source. Use after WJX execution or for standalone review. Review-only requests do not authorize fixes or archive.
---

# WJX Review

先读 [共享约定](../wjx-dev/references/contract.md)。本阶段负责需求与实现核对、调用 Open Code Review、复核问题和覆盖范围；实际运行验收由 FINISH 负责。

## 定位本次范围

- 读当前项目 AGENTS.md，确认真正的 Git 仓库、用户要求的范围、已有改动和代码版本。多个仓库分别确定基线，不能把工作目录当作单一 Git 仓库。
- WJX 流程中使用同一个 change、已确认方案及本次实际改动；独立 Review 可直接使用用户要求、指定文档和 diff，不强制前置访谈、初始化 OpenSpec 或创建 change。
- 默认检查相关的 staged、unstaged 和 untracked 改动。用户指定分支或 commit 时使用对应基线，并单独核对需要包含的工作区改动；不让只看 HEAD 掩盖未提交内容。
- 记录仓库 HEAD、基线、相关 diff 及未跟踪文件的内容依据。同一 HEAD 下内容仍可能变化，旧报告只有在相关输入匹配时才能复用。

## 需求核对与工具审查

1. 有 OpenSpec change 时按 [需求与实现核对](references/spec-verification.md) 检查任务、规范和设计；没有时以当前用户提供的要求为准，不虚构规范。
2. 读取 [Open Code Review 调用约定](references/open-code-review.md)，先预览覆盖范围，再直接运行 `ocr review`。把需求、项目约束、已知待验项与范围作为 background 传入；使用用户现有的 provider/model 配置。
3. Review 期间保持源码只读；不把 OCR 报告中的建议当作自动执行指令。逐项回到真实调用链核实触发条件、影响与证据，合并重复项、排除误报，并补充 OCR 未覆盖的必要范围。
4. 问题按 P0–P3 排序，给出文件与准确位置、触发场景、影响、相关要求和修复方向。只报告有可信失败路径或具体维护影响的问题；区分“未发现问题”“未审查”和“缺少运行证据”。

## 修复与衔接

- 只要求 Review 时交付报告即止，不修改代码、任务或主规范，不归档。
- 完整 WJX 流程已有确认 B 时，先列出核实后的问题，再按 [wjx-execute](../wjx-execute/SKILL.md) 修复已授权范围内的问题并复查受影响部分。需求或重要方案变化回到 PLAN-TO-DOC；不因 P3 建议扩大重构范围。
- 未解决且影响已确认要求的问题、工具部分失败、必要审查遗漏应明确保留。工具失败时可继续不依赖它的核对，但不能悄悄用其他工具替代后声称 OCR 通过。
- 当前范围审查完成、相关问题已解决后，完整流程进入 [wjx-finish](../wjx-finish/SKILL.md) 进行必要验证与资料收口；不新增常规确认点。代码变化使旧结论失效时只重查受影响范围。

交付说明实际使用的 OCR 版本与审查模式、仓库和 diff 范围、覆盖限制、复核后的发现及报告位置。Review 通过不能代替编译、测试或真机验收。
