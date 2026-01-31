# Slipbot Skill

**Purpose:** Capture and organize notes, ideas, quotes, and journal entries with automatic tagging, linking, and knowledge graph maintenance.

## Configuration

- **Notes directory:** `sync/slipbox/`
- **Graph index:** `sync/slipbox/.graph/graph.json`
- **Timezone:** User's local timezone (check USER.md or system)

## Recognition Patterns

Recognize note capture from these triggers:

### Explicit
- `note: {content}`
- `remember this: {content}`
- `quote: {content}`

### Prefix-based
- `> {content}` → quote
- `! {content}` → idea
- `* {content}` → journal

### Context-based
- User is clearly sharing a thought to capture
- Asking you to "remember" or "save" something
- Sharing quotes, insights, or observations

## Note Types

Determine type from content:
- **quote** - Starts with `>` or explicitly marked, contains attributed text
- **idea** - Starts with `!` or marked, speculative/creative thinking
- **journal** - Starts with `*` or marked, personal reflection/log
- **note** - Default for everything else

## Workflow

### 1. Capture

When a note is recognized:

1. **Extract content and metadata**
   - Note content
   - Type (quote/idea/journal/note)
   - Source information (if provided)
   
2. **Generate filename**
   - Format: `YYYYMMDD-HHMMSS-slug.md`
   - Slug: lowercase, hyphenated, from title (max 4-5 words)
   - Example: `20260131-143022-compound-interest-notes.md`

3. **Check for existing source**
   - If source provided, search existing notes for matching source title (case insensitive)
   - Use existing source if found
   - Otherwise, use provided source as-is
   - **No external API calls** - trust user input

4. **Generate tags**
   - Extract specific objects/concepts (nouns)
   - Focus on: people, tools, techniques, systems, specific topics
   - **Avoid broad categories** like "productivity" or "ideas"
   - 2-5 tags per note
   - Examples: `[pomodoro-technique, Cal-Newport, deep-work]`

5. **Create markdown file**

```yaml
---
title: "Your Note Title"
date: 2026-01-31T14:30:22-05:00
type: note
tags: [specific, object, based, tags]
source:
  title: "Source Title"
  type: "book"
  author: "Author Name"
links: []
---

Note content here in markdown.
```

### 2. Link

After creating a note, find connections:

1. **Search existing notes**
   - Use semantic search if available
   - Look for related concepts, people, topics
   - Check for overlapping tags

2. **Determine connection type**
   - **related** - Similar topic or theme
   - **extends** - Builds on or expands another note
   - **contradicts** - Opposing viewpoint
   - **references** - Mentions same person/book/concept
   - **supports** - Provides evidence for another note

3. **Add bidirectional links**
   - Only add links with confidence ≥ 0.75
   - Update both notes' frontmatter
   - Include reason for connection

```yaml
links:
  - id: "20260120-093045-compound-interest"
    type: related
    reason: "Both discuss exponential growth concepts"
```

### 3. Update Graph

After capture and linking:

1. **Load graph index**
   - Read `sync/slipbox/.graph/graph.json`
   
2. **Add/update note entry**

```json
{
  "notes": {
    "20260131-143022-note-title.md": {
      "title": "Your Note Title",
      "source": {
        "title": "Source Title",
        "type": "book",
        "author": "Author Name"
      },
      "type": "note",
      "tags": ["tag1", "tag2"],
      "links": [
        {
          "note": "20260120-093045-other-note.md",
          "confidence": 0.85
        }
      ],
      "last_updated": "2026-01-31T14:35:00-05:00"
    }
  },
  "last_updated": "2026-01-31T14:35:00-05:00"
}
```

3. **Write updated graph**
   - Save back to `sync/slipbox/.graph/graph.json`

### 4. Maintenance

Optionally (when requested or periodically):

- **Validate frontmatter** - Ensure all notes have required fields
- **Remove broken links** - Check if linked notes still exist
- **Suggest merges** - Identify duplicate or very similar notes
- **Rebuild graph** - If corrupted, rebuild from note files

## Querying

Respond to natural queries:

- "Show me notes about X"
- "Find quotes from Y"
- "What notes link to Z?"
- "What have I written about A?"

**Approach:**
1. Search graph index first (fast)
2. Fall back to file search if needed
3. Present results with titles, dates, snippets
4. Offer to show full content if relevant

## Source Types

Common source types:
- book
- article
- podcast
- video
- movie
- paper
- talk
- conversation

## Best Practices

### Tagging
- **Be specific:** `[vim, neovim-config, lua]` not `[editors, tools]`
- **Use objects:** Focus on nouns (people, systems, techniques)
- **Keep narrow:** 2-5 tags per note
- **Consistency:** Check existing tags before creating new ones

### Linking
- **Quality over quantity:** Only link when genuinely related (≥0.75 confidence)
- **Explain connections:** Always include reason
- **Bidirectional:** Update both notes when linking

### Note Titles
- **Descriptive but concise:** 3-8 words
- **Avoid generic:** Not "Thoughts" or "Notes", be specific
- **Question format works:** "Why does X happen?" or "How to Y?"

## Error Handling

- **Duplicate filename:** Add timestamp increment (`-2`, `-3`, etc.)
- **Missing timezone:** Default to UTC, ask user to set in USER.md
- **Corrupted graph:** Rebuild from note files
- **Invalid frontmatter:** Fix and notify user

## User Feedback

Keep responses minimal:
- ✅ "Note captured: [title]"
- ✅ "Added 2 links to related notes"
- ❌ Don't narrate every step unless debugging

## Example Interaction

**User:** "note: The Feynman Technique is about teaching concepts to identify gaps in understanding"

**You:**
1. Create `20260131-163500-feynman-technique.md`
2. Tag: `[Feynman-technique, learning, teaching]`
3. Search for related notes (study techniques, learning methods)
4. Link to any existing notes about learning with confidence ≥ 0.75
5. Update graph index
6. Reply: "Note captured: Feynman Technique"

---

**When to apply this skill:** Whenever user shares content that should be captured for later reference or shows intent to save information.
