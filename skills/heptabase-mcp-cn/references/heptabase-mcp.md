# Heptabase MCP 工具速查

## 写入

### mcp__heptabase__save_to_note_card
- 功能：在 Heptabase 主空间创建新笔记卡片。
- 用法：传入完整内容文本，首行作为卡片标题。
- 适用：保存总结/分析结果或结构化笔记。

### mcp__heptabase__append_to_journal
- 功能：向今日日记追加内容（若不存在则自动创建）。
- 用法：传入追加文本内容。

## 日记

### mcp__heptabase__get_journal_range
- 参数：startDate, endDate（YYYY-MM-DD）。
- 规则：包含起止日期；单次最多 92 天，超出需拆分多次调用。

## 搜索与对象

### mcp__heptabase__semantic_search_objects
- 参数：queries（列表），resultObjectTypes（列表）。
- 策略：使用 1-3 组不同角度查询；返回预览内容。
- 后续：对相关结果用 `get_object` 获取全文；结果可能引用白板。

### mcp__heptabase__get_object
- 参数：objectId, objectType。
- 支持类型：card, journal, videoCard, audioCard, imageCard, highlightElement, textElement, videoElement, imageElement, chat, chatMessage, chatMessagesElement, section。
- 注意：不用于 pdfCard；如对象返回有 hasMore，继续拉取完整内容。

### mcp__heptabase__search_whiteboards
- 参数：keywords（列表）。
- 特点：OR 逻辑，关键词越多覆盖越广。
- 注意：返回 XML 含白板 ID；对用户只描述白板名称，不暴露 ID。
- 后续：用 `get_whiteboard_with_objects` 获取完整白板对象。

### mcp__heptabase__get_whiteboard_with_objects
- 参数：whiteboardId（由 search_whiteboards 或 semantic_search_objects 获取）。
- 返回：白板结构、对象及连接关系；卡片/元素可能仅部分内容。
- 后续：若需对象全文，用 `get_object`。

## PDF

### mcp__heptabase__search_pdf_content
- 参数：pdfCardId, keywords（列表）。
- 前置：先通过 `semantic_search_objects` 或 `get_object` 获取 pdfCardId。
- 特点：BM25 关键词匹配，OR 逻辑，模糊匹配。
- 返回：最多 80 个相关分块及其上下文。
- 后续：用 `get_pdf_pages` 拉取对应页码的完整内容。

### mcp__heptabase__get_pdf_pages
- 参数：pdfCardId, startPageNumber, endPageNumber（页码从 1 开始）。
- 规则：包含起止页；需要显著超过 100 页时先向用户确认范围。
