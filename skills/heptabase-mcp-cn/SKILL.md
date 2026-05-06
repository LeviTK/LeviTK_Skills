---
name: heptabase-mcp-cn
description: 使用 MCP heptabase 工具在 Heptabase 中搜索、读取、分析与写入内容，包含处理用户粘贴的卡片/白板/PDF/媒体卡片链接（video/audio/image）。适用于需要检索卡片/白板/日记/PDF、获取对象全文、总结分析/深度思考用户已有内容，或将结果保存为卡片/追加到今日日记的任务。
---

# Heptabase MCP 中文技能（heptabase-mcp-cn）

## 概述

使用 MCP heptabase 发现、读取与整理内容，并按需求输出总结/分析/深度思考结果。需要详细参数和限制时，读取 `references/heptabase-mcp.md`。

## 工作流程

1. 明确目标与范围：主题、时间范围、是否涉及白板/日记/PDF。
2. 优先处理用户粘贴的 Heptabase 链接：
   - 多条链接按出现顺序逐一处理。
   - 链接样式参考：`/card/<uuid>`、`/whiteboard/<uuid>`、`/card/<date>`（例如 `2026-02-04`，表示 Journal card）。
   - 判定链接类型并直接获取：`/whiteboard/<uuid>` 用 `get_whiteboard_with_objects`；`/card/<uuid>` 默认按 `card` 处理。
   - 若用户在链接后给出类型提示（video/audio/image/pdf），按提示映射为 `videoCard`/`audioCard`/`imageCard`/`pdfCard`。
   - 无法确认是否为 PDF 时先询问；用户明确为 PDF 时按 `pdfCard` 流程处理。
   - 若检测到卡片/白板中嵌入其他卡片或白板，先仅获取并列出其标题，再询问是否展开正文（可给出展开建议）。
   - 输出正文时如内容很长，分批次输出并提前说明会继续。
   - 用户只给链接时默认输出正文；若明确要求总结/分析，再输出对应结果。
3. 发现相关对象：
   - 主题检索：`semantic_search_objects`，使用 1-3 个不同角度的查询。
   - 白板检索：`search_whiteboards`。
   - 日记范围：`get_journal_range`（超过 92 天需拆分）。
4. 获取完整内容：
   - 一般对象：`get_object`（避免 pdfCard）。
   - 白板：先搜索到 whiteboardId，再 `get_whiteboard_with_objects`。
   - PDF：若用户给定页码范围，直接 `get_pdf_pages`；否则 `search_pdf_content` 定位页码，再 `get_pdf_pages` 拉完整页。
5. 产出与写入：
   - 输出总结/分析/深度思考，并标注信息来源或时间范围。
   - 需要保存时：先读取 `references/Hep_Markdown.md` 确认语法，再使用 `save_to_note_card`（首行标题）、或 `append_to_journal`（追加今日日记）。

## 典型请求

- “帮我总结最近两周的日记要点，并给出行动建议。”
- “查找我关于 XXX 的笔记/卡片，做一次深度分析。”
- “请把这段结论保存为 Heptabase 卡片，标题用一句话概括。”
- “总结下这张卡片/这个白板/这个 PDF 链接的内容。”

## 注意事项

- 不要向用户暴露 whiteboardId 或返回的 XML/内部标记；对用户只用自然语言描述结果。
- 需要超过 100 页的 PDF 时先询问用户范围。
- 对嵌入内容只先列出标题并征求是否展开，避免默认拉取全部正文。
- 遇到 Auth required：提示用户在其 AI 服务的 MCP 设置中重新授权 `https://api.heptabase.com/mcp` 后重试。
- 遇到 502 等服务端错误：提示稍后重试，并询问是否能在浏览器正常打开该链接。
- 移动端 MCP 可能不稳定，必要时建议改用桌面或网页端。
- 不清楚范围或对象时先澄清，再检索。

## 资源

- `references/heptabase-mcp.md`：工具速查、参数与限制说明。需要细节时先读取。
- `references/Hep_Markdown.md`：Heptabase 的 Markdown 语法详解。
