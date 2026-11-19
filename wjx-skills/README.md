# WJX Skills

适用于所有代码项目的个人开发流程。具体目录、技术栈、命名、构建和设备职责读取各项目 `AGENTS.md`。

导出日期：2026-11-19。`skills/` 中六个 WJX Skills 及其参考文件来自当前本地安装版本，导出时保持内容一致。

## 流程

```text
提出新需求 → 询问是否使用 WJX
  → wjx-askme → 需求共识确认
  → wjx-plan-to-doc → 具体方案确认
  → wjx-execute → wjx-review → wjx-finish
```

| Skill | 职责 |
| --- | --- |
| [wjx-dev](skills/wjx-dev/SKILL.md) | 总入口，选择流程、恢复进度并衔接阶段 |
| [wjx-askme](skills/wjx-askme/SKILL.md) | 代码调查与分轮追问，形成可确认的需求共识 |
| [wjx-plan-to-doc](skills/wjx-plan-to-doc/SKILL.md) | 创建或修订需求规范、技术设计和任务清单 |
| [wjx-execute](skills/wjx-execute/SKILL.md) | 按当前已确认方案实施并更新任务进度 |
| [wjx-review](skills/wjx-review/SKILL.md) | 调用 Open Code Review，核对需求与源码，复核发现的问题 |
| [wjx-finish](skills/wjx-finish/SKILL.md) | 完成允许的验证，满足必要验收条件后同步规范并归档 |

两个确认点分别对应需求共识和具体方案。完整流程在方案确认后连续实施、审查和验收；单独要求 Review 时只交付报告。提交、push、发布和设备操作仍遵从当前项目规则与用户授权。

## 安装与依赖

六个 `wjx-*` 目录需要一起安装，以保持相对引用有效。本包同时附带 [grilling](dependencies/grilling/SKILL.md) 的当前本地副本，供 ASKME 的访谈流程使用；它属于外部依赖，不是 WJX 自有技能。

在本目录执行以下命令安装到 Codex。已有同名技能时先备份，并确认要使用本导出版本；已有可用的 grilling 时可保留现有版本，省略最后一行。

```sh
skill_dest="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skill_dest"
cp -R skills/wjx-* "$skill_dest/"
cp -R dependencies/grilling "$skill_dest/"
```

依赖工具需在目标机器单独准备：

- **OpenSpec CLI**：负责文档、任务状态与规范管理，无需安装原版 OpenSpec Skills。本次使用 2.1.0 核对 CLI 能力；其他版本先检查实际命令帮助和兼容性。
- **Open Code Review CLI**：命令为 `ocr`，npm 包为 `@alibaba-group/open-code-review`。本次核对版本为 1.13.13；真实审查使用它自身已配置的 provider/model 和认证，不自动继承 Codex 登录。本包不包含模型配置、密钥或认证文件。

可用以下命令检查工具是否可用：

```sh
openspec --version
ocr version
ocr review --help
```

WJX 新项目初始化使用受支持的 `--tools none`，避免重新生成已删除的原版 OpenSpec Skills。已有项目和 Store 按 CLI 实际解析结果继续使用。

## 自动提示与手动调用

将 [AGENTS.snippet.md](AGENTS.snippet.md) 中的 WJX 规则合入实际生效的全局或项目 `AGENTS.md`，保留其中原有规则。仅复制技能目录不会自动安装这段触发规则。

规则会在新的业务功能、页面或明显能力扩展开始前询问是否使用 WJX；既有 Bug 修复、纯问答和局部文案/样式修改不主动触发整套流程。

也可以直接调用某个阶段，例如：

```text
用 $wjx-dev 处理这个新需求。
用 $wjx-askme 帮我查清并问透这个需求。
用 $wjx-review 调用 Open Code Review 审查本次改动，只报告问题。
```

## 导出验证范围

导出时检查六个 WJX Skills 的格式、相对引用与本地原文件一致性。OCR 的本地预览已验证 staged、unstaged 与 untracked 文件覆盖；未以此声称真实模型审查或业务运行验收通过。目标机器的依赖安装、模型连接和具体项目验证需在使用时确认。
