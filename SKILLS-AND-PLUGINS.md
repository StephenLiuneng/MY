# Skills 与插件清单

记录个人选用的 Skill、插件和 MCP 工具，方便查阅用途；此列表不是全部已安装工具的清单，也不代表各工具的运行依赖已完成配置。

| 名称 | 类型 / 标识 | 说明 | 使用条件 |
| --- | --- | --- | --- |
| watch | Skill：`watch` | 分析本地视频或视频 URL，通过 yt-dlp 获取视频与字幕，使用 ffmpeg 提取画面，结合带时间戳的字幕或转录总结内容。支持指定时间段和关键时间点。 | 需要 yt-dlp、ffmpeg；无字幕时可使用配置好的 Groq / OpenAI Whisper 转录，届时会向对应服务发送音频。 |
| Figwright | 本地 MCP：`figwright`；配套 Skills：`figma-codegen`、`figma-build` | 双向连接 Figma 与代码：读取节点、布局、间距、颜色、字体、组件、图片与动效信息，也可创建或修改设计。生成代码时可匹配项目已有组件和设计变量。 | 目标文件需在 Figma 中打开并运行 Figwright 插件；先检查 `ping`，多文件时用 `list_files`、`use_file` 选择目标。 |
| REA（Reverse Engineer Anything） | Skill：`reverse-engineer-anything`；可配合 REA CLI / MCP | 分析原生二进制、安装包、托管程序集、Electron / JavaScript 应用、固件和浏览器目标，支持反编译、版本比较、运行时取证与 AgentEnv 环境导出。适合基于已发布产物或运行行为研究应用。 | 安装 Skill 不等于已注册 REA MCP 或安装分析引擎；实际能力取决于 CLI / MCP 版本与对应引擎。普通源码仓库分析无需启动 REA。 |
| Open Code Review（OCR） | 插件：`open-code-review-codex`；Skills：`open-code-review`、`open-code-review-delegate` | 审查未提交改动、指定提交、PR 或分支差异，生成定位到代码行的问题报告。原生模式使用独立配置的模型服务；委派模式由 OCR 组织文件与规则，再使用宿主 Agent 的模型审查。 | 需要 OCR CLI；原生模式需配置支持的模型服务，委派模式无需独立 OCR 模型凭据。修复代码需要另行提出要求。 |

## 项目链接

- [REA](https://github.com/morluto/rea)
- [Open Code Review](https://github.com/alibaba/open-code-review)
