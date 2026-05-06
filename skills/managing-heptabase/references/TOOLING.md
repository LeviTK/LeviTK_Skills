# Heptabase Tooling Reference

Use the tools available in the current agent runtime. Tool names vary by environment, but the workflow stays the same: discover relevant objects, fetch full content, then answer or write.

## MCP-style tools

If the environment provides Heptabase MCP tools, prefer them for direct access.

| Capability | Typical tool pattern |
|------------|----------------------|
| Search objects | `semantic_search_objects` |
| Read an object | `get_object` |
| Read journals | `get_journal_range` |
| Append to journal | `append_to_journal` |
| Save a note card | `save_to_note_card` |
| List tags | `list_tags` |
| Read cards under a tag | `get_tag_cards` |
| Search whiteboards | `search_whiteboards` |
| Read a whiteboard | `get_whiteboard_with_objects` |
| Search a PDF | `search_pdf_content` |
| Read PDF pages | `get_pdf_pages` |

## CLI-style tools

If a Heptabase CLI is available, use it for local scripted workflows such as listing cards, editing Markdown content, managing tags, or browsing AI Tutor resources. Prefer existing CLI commands over hand-built API calls.

## Fallbacks

If no Heptabase integration is available:

1. Explain that direct access is unavailable in the current runtime.
2. Ask the user to paste the relevant card, journal entry, PDF excerpt, or export.
3. Continue with analysis, rewriting, extraction, or organization based on the provided content.

## Safety

- Do not guess unseen card contents.
- Do not fabricate object IDs, titles, dates, or page numbers.
- Do not overwrite existing knowledge base content unless the user explicitly requests replacement.
- Avoid saving sensitive information unless the user clearly asks to store it.
