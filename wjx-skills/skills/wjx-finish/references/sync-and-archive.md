# 同步与归档

仅在请求包含收尾、当前范围的 Review 完成、核实问题解决、必要任务与验收完成后使用。先遵守 [CLI 与路径约定](../../wjx-dev/references/openspec-cli.md)。本步骤串行执行，不另行调用原版 Skills。

## 归档前核对

1. 刷新 status，确认 change、真实 `changeRoot`、`planningHome`、schema 与资料依赖；必要资料须已完成或明确跳过。
2. 读取 apply 的全部任务与不可读文件信息，再用 `openspec list --json` 找到唯一同名 change。任务计数须为非负整数且 completed 不大于 total；无法确定完整性时停止同步与归档。未配置任务跟踪的 schema 不强加任务文件，不能用 artifact 已存在推断实现完成。
3. 当前版本支持时可读取 `instructions archive --change "<name>" --json` 的 context/operationGuidance；该建议接口不支持时不阻塞，不能用其失败替代其他必须的状态、规则或校验结果。
4. 展示批准增量的同步范围；完整 WJX 的确认 B 已含正常收尾，不重复要求确认。新增范围、删除未授权要求或冲突仍需单独处理。

## 同步主规范

- 仅使用 status 的 `artifactPaths.specs.existingOutputPaths` 作为同步输入。列表为空或不存在时报告无增量，不从其他资料猜测；自定义 schema 未提供可识别的规范同步合同，且确实需要同步时先解决该限制，不假装已同步。
- capability 保留完整相对路径（例如 `billing/invoices`），主规范位于 `<planningHome.root>/openspec/specs/<capability-path>/spec.md`。验证输出和删除路径解析后仍在真实 specs 根内。
- 用户显式指定子集时只同步其列出的完整已有路径；子集未覆盖的本 change 增量不能被当作已完成而归档。
- 先读所有选中增量与现有主规范，列出冲突与增删改名；有阻塞先处理，不开始部分同步后掩盖失败。
- 写入前只取一次 `instructions specs --change "<name>" --json` 规则快照。命令失败或 JSON 无效时停止，不能当作无规则；有效响应缺 rules 才是无额外规则。对本次写入复用快照，不重复获取；规则只约束规范内容，不改变路径、权限或归档步骤。

按语义合并，不把 delta 文件直接覆盖主规范：

| 操作 | 合并规则 |
| --- | --- |
| ADDED | 新增要求；已存在时对照合并，避免重复块 |
| MODIFIED | 修改原要求的正文/场景；保留未涉及的内容及全部仍有效场景；找不到原要求时停止，不凭空创建 |
| REMOVED | 删除明确指定的要求块；不误删同名之外的行为或附加文档 |
| RENAMED | FROM 改为 TO，行为保持；已同步时核对 TO 存在且 FROM 不存在，名称冲突时停止 |

主规范不存在时，只能由 ADDED 创建；有 MODIFIED / RENAMED 则阻塞。REMOVED 无对象可删除时警示并保持原树；纯 REMOVED 且 `.openspec.yaml` 已有 `retire_capabilities: true`、主规范已缺失可视为已退役，否则不得据此创建空规范或声称同步成功。空增量同样不能凭空生成规范。

新规范包含 `# <capability> Specification`、`## Purpose`、`## Requirements`；Purpose 从增量原文复制，确实缺失才用 TBD 并明确待完善。已有规范标题、Purpose 和未涉及内容保持原样。要求使用 `### Requirement:`、场景使用 `#### Scenario:`；主规范不能残留 ADDED/MODIFIED/REMOVED/RENAMED 区块标题。

移除最后一个要求时，只有本次确实移除了原有要求、规范结构完整且除标题/Purpose/Requirements/要求及其场景示例外无其他自有内容、元数据明确 `retire_capabilities: true`、路径确在真实 specs 根内，才可删除整个 spec.md（目录空后才删目录）。缺任何条件先停止，不写空 Requirements；报告退役包含 Purpose 的删除。已有空规范不以此规则自动清理。

合并后执行同根/Store 的 `openspec validate --specs`，并逐项重新比较全部增量：新增存在、修改符合且其他场景保留、删除已消失、改名正确。失败或部分成功时 change 保持活跃，报告实际已写范围及剩余问题，不继续归档。

## 最后移动 change

确认所有适用增量已同步且必要检查通过后，按 status 的 `planningHome.changesDir` 解析 `archive` 目录；目标名为 `YYYY-MM-DD-<change-name>`，已有日期前缀时不再添加。目标已存在时停止，不覆盖或合并。

串行移动整个 `changeRoot`，保留 `.openspec.yaml` 和全部资料。不要在已经完成语义同步后再运行可能重复应用 delta 的默认 archive 命令；该步骤只做已验证 change 的目录移动。若 CLI 版本或项目提供另一种归档合同，先确认其不会重复同步，再使用。

完成后检查目标存在、原活动路径消失，刷新活动 change 列表并核对主规范结果。仅此时报告已归档。不得用 `--no-validate`、跳过失败、并行同步后立即移动或把待验项改为完成来强行收尾。
