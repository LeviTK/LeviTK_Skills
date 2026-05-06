---
name: heptabase-cli-cn
description: 通过 Heptabase CLI 创建、读取和编辑笔记、日记、标签、卡片，列出白板并管理白板上的卡片，以及浏览 AI Tutor 目标、课程和课时。当用户要求管理 Heptabase 知识库、搜索卡片、处理日记、标签或白板，或读取 AI Tutor 内容时使用。
allowed-tools: Bash(heptabase *) Bash(jq *)
metadata:
  heptabase-cli-version-range: "0.2.x"
---

## 前置条件

- 已通过桌面应用安装 CLI。在 macOS/Linux 上命令为 `heptabase`；Windows 会为 cmd/PowerShell 安装 `heptabase.cmd`，并为 POSIX shell 安装 `heptabase` shim。
- 使用前必须通过 `heptabase --version` 检查版本兼容性。如果已安装的 CLI 版本超出本技能兼容范围（`0.2.x`），必须停止操作，并请用户先更新 Heptabase 桌面应用或此技能包后再继续。

## 命令发现

运行 `heptabase help` 查看所有可用的顶层命令。该帮助信息始终保持最新。每个命令都支持 `--help` 查看详细用法：

```bash
heptabase help
heptabase note --help
heptabase note create --help
```

## 常用配方

针对高频请求，可直接使用以下命令作为快速配方。对于不常用的参数，或命令执行失败时，请运行 `heptabase help` 或 `<command> --help` 来确认正确语法。

- **最近的卡片：** `heptabase card list --sort createdTime --direction descending --limit 20`
- **今日日记：** `heptabase journal read $(date +%Y-%m-%d)`
- **按关键词搜索卡片：** `heptabase card list -q "<keyword>" --limit 20`
- **列出白板上的卡片：** `heptabase whiteboard cards <whiteboardId>`
- **向白板添加卡片：** `heptabase whiteboard add-card --whiteboard-id <whiteboardId> --card-id <cardIdOrDate>`

## 所有输出均为 JSON

每个命令都会向 stdout 输出 JSON。可以使用 `jq` 解析，也可以通过管道传给其他工具。

## 故障排查

- **桌面应用必须正在运行。** CLI 会与应用内的本地服务器通信。如果应用已关闭，所有命令都会失败。运行 `heptabase start` 启动应用，并等待其就绪。
- **变更操作会串行执行。** 写入操作（创建、保存、追加、移入废纸篓、恢复、添加/移除标签、向白板添加/移除卡片）会一次只执行一个，以避免冲突。读取操作可以并发执行。
- **请求体大小限制。** 服务器会拒绝大于 1 MB 的请求体。
- **请求超时。** 如果请求发送请求体的耗时超过 10 秒，服务器会判定超时。

## 已知限制

- **不支持自动启用本地服务器或自动安装 CLI。** 如果本地 CLI 服务器被禁用，或 CLI 连接配置缺失，此技能无法自行修复；请先让用户在桌面端设置中启用 Local CLI Server 并安装 CLI。
- **不支持二进制/媒体上传工作流。** 此技能用于对笔记、日记、标签、卡片执行 JSON/文本操作，以及读取 AI Tutor 内容；不适用于文件上传或媒体处理 API。
- **暂不支持创建、编辑或删除白板。** 可以列出白板，并对其中的卡片进行添加、列出或移除操作，但不能创建、重命名、移动或删除白板。
- **暂不支持读取文件。** 无法通过 `fileId` 读取文件（例如图片、视频）。
- **暂不支持读取 PDF 卡片。** 无法读取 PDF 卡片或其解析后的内容。

## 警告

- **必须将 CLI 作为唯一的数据访问路径。** 绝不要通过本地数据库文件、应用存储、缓存文件、内部端点或任何其他非 CLI 机制直接读取、写入或修改 Heptabase 应用数据。如果 CLI 不支持用户请求的操作，应停止并说明该操作暂不受支持。
