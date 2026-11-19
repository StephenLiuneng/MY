# 创建与修订方案资料

先遵守 [CLI 与路径约定](../../wjx-dev/references/openspec-cli.md) 和共享约定的确认 A；本阶段不写业务代码。

## 新 change

1. 需求已有共识后选择简短的 kebab-case 名称。先检查已有 change；同一需求复用，不覆盖同名目录。用 `openspec new change "<name>"` 保留 CLI 生成的元数据与默认 schema。
2. 读取 `status --change "<name>" --json`。从 `applyRequires` 出发，沿 artifacts 的 `requires` 递归计算实施所需的全部产物；不要因为 tasks 已存在就忽略其缺失依赖。集合外资料不主动扩展。
3. 依赖顺序逐项获取 `instructions "<artifact-id>" --change "<name>" --json`，读取 `instruction`、`template`、`context`、`rules` 以及最新磁盘依赖。用真实代码事实填写模板，不能把调查和设计留成泛泛的实施待办。
4. 仅创建确认范围内、schema 要求且尚缺的资料。状态 `skipped` 或 instructions 的 `skipped: true` 必须保持跳过。只有产物自身 instruction 明确为条件性且本需求不适用时才说明理由后略过；不自行把 specs 判为可选。条件性依赖已合理略过时，按其 instruction 继续后续资料。
5. 将 glob 解析为明确且位于 `changeRoot` 内的实际路径。若 instruction 指定另一个生成工具，先确认它能遵守目标路径和当前授权再调用。写完逐项检查文件并刷新 status，直到所需资料全部存在或按规则跳过。

## 同一 change 的修订

- 先读本次受影响的资料及其关联资料，检查需求、设计与任务双向一致性。后续任务的变化也可能影响 proposal/specs；不机械只改依赖图下游。
- 编辑 `artifactPaths.<id>.existingOutputPaths` 中的实际文件。新增缺失资料按上面的生成规则；已有部分文件的 glob 产物也可能需要新增另一项，不能把 `done` 误当成所有能力都有文档。
- 补充新文件前刷新 status/instructions，确认仍在本次范围、不是 skipped、必要依赖可读、路径不越界且没有已有文件；保留其他人的修改。
- 同一需求直接修订同一套资料；用户授权的措辞、进度或一致性修正不新增确认门槛。改变目标、行为或重要方案时，重新确认受影响部分，展示具体修订后取得确认 B 才继续实施。
- 已完成任务因方案变化而不再满足时，说明需要重做的内容并准确更新进度，不能保留不真实的完成标记。真正另一个需求才建新 change。

## 规范与验证

- 默认 spec-driven 的规范使用 `### Requirement:`、`#### Scenario:`，以可观察行为表达要求。使用 ADDED / MODIFIED / REMOVED / RENAMED 增量区分添加、修改、删除和改名。
- MODIFIED 包含该要求完整的新正文和所有仍需保留的场景；不因只描述新场景而丢失原有场景。改名不等于改变行为；删除需有当前已确认的范围依据。
- 用当前 CLI 支持的 change validate 检查格式，同时人工核对需求、方案、任务和必要验收的一致性。说明真实文件、变更范围与校验结果，再请求确认 B；产物存在不等于已获实施授权。
