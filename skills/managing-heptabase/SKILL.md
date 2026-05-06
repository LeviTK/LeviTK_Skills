---
name: managing-heptabase
description: Manages Heptabase knowledge base content by searching, reading, analyzing, creating, and updating cards, journals, tags, whiteboards, PDFs, and media cards. Use when the user asks to work with Heptabase, personal knowledge notes, journals, tags, whiteboards, AI Tutor content, or pasted Heptabase links.
---

# Managing Heptabase

Use this skill to work with a user's Heptabase knowledge base through whichever Heptabase integration is available in the current agent environment.

## Workflow

1. Identify the target object type: card, journal, tag, whiteboard, PDF, media card, highlight, or AI Tutor content.
2. Choose the narrowest available tool for the request:
   - Use semantic search for topic discovery.
   - Use exact object reads when the user provides a Heptabase link or object ID.
   - Use journal range reads for date-based journal questions.
   - Use tag or whiteboard listing tools when the user asks about organization.
3. Read the full object content before summarizing, rewriting, extracting decisions, or making updates.
4. For PDFs, search for relevant pages first, then fetch complete page ranges before producing detailed answers.
5. When writing to Heptabase, confirm the destination implied by the user: new note card, existing card, today's journal, a specific date's journal, tag, or whiteboard.
6. Keep edits scoped to the user's requested content. Do not reorganize unrelated cards, tags, or whiteboards unless explicitly asked.
7. Report what was read or changed, and mention any objects that could not be found.

## Link handling

When the user pastes a Heptabase URL:

1. Extract the object identifier from the URL.
2. Determine whether the URL points to a card, whiteboard, PDF, media card, journal, or another object type.
3. Fetch the object directly when the environment provides a direct object-read tool.
4. If direct fetching is unavailable, search by title, nearby text, or visible object metadata from the URL.

## Writing guidelines

- Prefer appending to journals instead of overwriting existing journal content.
- For note cards, use clear Markdown with an H1 title on the first line when the tool expects it.
- Preserve the user's language unless they ask for translation.
- Separate blocks with blank lines for readability.
- Do not include private tool logs, hidden reasoning, or unrelated search results in saved notes.

## Common tasks

| Request | Recommended approach |
|---------|----------------------|
| “Search my Heptabase for X” | Run semantic or keyword search, then read the most relevant objects fully. |
| “Summarize this card” | Fetch the full card or media transcript before summarizing. |
| “What did I write last week?” | Retrieve the journal range for the requested dates. |
| “Save this insight” | Create a new note card or append to today's journal, depending on the user's wording. |
| “Find this in a PDF” | Search PDF content first, then fetch complete pages around the best matches. |
| “Organize these notes” | Inspect the relevant tags or whiteboards before proposing or applying changes. |

## Tooling reference

See [TOOLING.md](references/TOOLING.md) for integration-specific guidance and fallback options.
