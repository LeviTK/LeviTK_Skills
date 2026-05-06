# Heptabase 工具参考

使用当前代理运行环境中可用的工具。不同环境下工具名可能不同，但工作流程一致：先发现相关对象，再拉取完整内容，最后回答或写入。

## MCP 风格工具

如果环境提供 Heptabase MCP 工具，应优先使用它们进行直接访问。

| 能力 | 常见工具模式 |
|------|--------------|
| 搜索对象 | `semantic_search_objects` |
| 读取对象 | `get_object` |
| 读取日记 | `get_journal_range` |
| 追加到日记 | `append_to_journal` |
| 保存笔记卡 | `save_to_note_card` |
| 列出标签 | `list_tags` |
| 读取标签下的卡片 | `get_tag_cards` |
| 搜索白板 | `search_whiteboards` |
| 读取白板 | `get_whiteboard_with_objects` |
| 搜索 PDF | `search_pdf_content` |
| 读取 PDF 页面 | `get_pdf_pages` |

## CLI 风格工具

如果有 Heptabase CLI，可将其用于本地脚本化工作流，例如列出卡片、编辑 Markdown 内容、管理标签或浏览 AI Tutor 资源。优先使用现成 CLI 命令，而不是手写 API 调用。

## 兜底方案

如果当前环境没有 Heptabase 集成：

1. 说明当前运行环境无法直接访问。
2. 请用户粘贴相关卡片、日记条目、PDF 摘录或导出内容。
3. 基于用户提供的内容继续做分析、改写、提取或整理。

## 安全要求

- 不要猜测未读取到的卡片内容。
- 不要编造对象 ID、标题、日期或页码。
- 除非用户明确要求替换，否则不要覆盖已有知识库内容。
- 除非用户明确要求保存，否则避免写入敏感信息。
