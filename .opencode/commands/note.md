---
description: Capture a note
agent: build
---

- Note to capture: $1
- Content Type: $2
- Source: $3

# 1. Capture

**Purpose**: Accept an input and create a well-formed note file.

**Behavior**:
- Accepts raw text input
- Auto-detect content type unless provided. (eg., thought, quote, idea, journal, meeting, reference)
- Generate appropriate filename and frontmatter
- Asks minimal questions only when essential (e.g., source for quotes)
- Create the markdown file immediately

**Output**: Create a single markdown file in `/home/jrswab/notes/`

## Note Format

```yaml
---
title: "Knowledge Graph Design Thoughts"
date: 2026-01-25T14:30:22
type: idea
tags: [systems, notes, automation]
source: null
links:
  - id: "20260120-093045-compound-interest"
    type: related
    reason: "Both discuss emergent complexity"
---

Note contents here in markdown...

```

## On Tagging
- Broad, general, connections are not useful in the long run. It only cases the topic, or tag, to contain a mass amount of loosely connected notes.
- Only tag notes with objects or concepts within the note. Objects often found in the nouns of the sentence.
- Object based tags are more precise and uncover real connections.
- Object tags narrow down the search faster.

# 2. Link

**Purpose**: Maintain the knowledge graph by finding connections between notes.

**Behavior**:
- Run automatically after each capture
- Analyze new note content against existing notes
- Identify connection types:
  - **related**: Similar topic or theme
  - **extends**: Builds on or expands another note
  - **contradicts**: Opposing viewpoint or information
  - **references**: Mentions same person, book, concept
  - **supports**: Provides evidence for another note
- Update frontmatter with bidirectional links

## In Each Note's Frontmatter

```yaml
links:
  - id: "20260120-093045-compound-interest"
    type: related
    reason: "Both discuss exponential growth concepts"
  - id: "20260118-142233-warren-buffett"
    type: references
    reason: "Same author quoted"
```

# 3. Maintenance

**Purpose**: Keep the system healthy and organized for searching.

- Validate frontmatter consistency on the new note
- Suggest merging duplicate concepts

# 4. Update Knowledge Graph

**Goal:** Maintain the graph index for fast queries

- Graph file is located in `./.graph/index.json` for fast queries (rebuildable)
- Remove broken links from the graph (deleted notes)
- Rebuild graph index if corrupted

## Parts of the Graph Entry
- title: the title of the note.
   - This field can not be null.
- Source: If a source is provided by the user, add the source title, source type, and source author.
   - This field can be null.
- type: the note type.
   - This field can not be null.
- tags: the tags on the note.
   - This field can not be null.
- links: other notes with that have a relationship with this note.
   - This field can be null.
   - note: name of the linked note.
   - confidence: How confident you are that the notes relate. Do not add links if the confidence is less than `0.75`.
- last_updated: the timestamp in ISO 8601 at the time of updating the file
   - Use Eastern Time Zone offset from UTC.
   - This field can not be null.


## Example Graph
```json
{
  "notes": {
    "20260125-143022-money-works.md": {
      "title": "How Money Works",
      "source": {
        "title": "Get Rich or Die Tryin'",
        "type": "movie",
        "author": "Terence Winter"
      },
      "type": "idea",
      "tags": [
        "money",
        "wealth"
      ],
      "links": [
        {
          "note": "20260120-093045-compound-interest",
          "confidence": 0.992
        },
        {
          "note": "20260120-092025-what-are-banks",
          "confidence": 0.8
        }
      ]
    }
  },
  "last_updated": "2026-01-25T14:35:00"
}
```

