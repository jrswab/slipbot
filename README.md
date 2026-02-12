# Slipbot

![slipbot](slipbot.png)

**Agentic Zettelkasten skill definitions for AI Agents.** Captures notes, quotes, ideas, and journals via prefix syntax. AI handles YAML frontmatter generation, object-based tagging, bidirectional linking with typed connections, and JSON knowledge graph maintenance. Includes importers for Kindle, Instapaper, and Logseq.

## What is Slipbot?

Slipbot is a set of skill definitions that turn any compatible AI agent into an automated [Zettelkasten](https://en.wikipedia.org/wiki/Zettelkasten) (slip-box) manager. It eliminates the overhead of maintaining a personal knowledge graph -- instead of worrying about organization, tags, or where notes go, you capture thoughts naturally and let your AI agent handle everything else.

The `skills/` directory contains structured SKILL.md files that teach your AI assistant how to capture, organize, link, and maintain notes. Any AI agent that can read markdown skill definitions and perform file operations can use Slipbot.

Your job: **Think and capture.**  
Agent's job: **Organize, link, and maintain.**

## How It Works

The workflow is simple:

1. Share a thought with your AI assistant using simple prefixes:
   - `-` for notes: `- Research idea about spaced repetition`
   - `>` for quotes: `> The best time to plant a tree was 20 years ago ~ proverb, Chinese Proverb`
   - `!` for ideas: `! What if we built a knowledge graph that maintains itself?`
   - `*` for journal entries: `* Today's stand-up went really well`
   - `~` for source attribution: `- Content here ~ book, Title by Author`

2. Your AI processes and organizes the note automatically

3. Your second brain grows without manual maintenance

That's it. No folders to organize, no tags to remember, no systems to maintain.

## Quick Start

### Requirements

- Any AI agent/assistant that supports loading skill definitions from markdown files and can read/write local files
- (Optional) [Syncthing](https://syncthing.net/) for multi-device file sync

### Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/jrswab/slipbot.git
   ```
2. Point your AI agent at the `skills/` directory so it loads the SKILL.md files
3. Start capturing notes using the prefix syntax below

Your AI assistant will:
- Automatically recognize when you're capturing a note
- Create properly formatted markdown files in `slipbox/`
- Generate object-based tags from your content
- Link related notes with bidirectional connections
- Maintain the JSON knowledge graph index for fast queries

## Usage

### Basic Note Capture

```
- Research idea: explore the relationship between retrieval practice and spaced repetition
```

### Capture Quotes

```
> The best time to plant a tree was 20 years ago. The second best time is now. ~ proverb, Chinese Proverb
```

### Ideas

Prefix with `!` for automatic idea detection:
```
! What if we used event sourcing for the file processing pipeline?
```

### Journal Entries

Prefix with `*` for automatic journal entry detection:
```
* Today's stand-up went really well. The team is aligned on the Lambda migration.
```

### With Source Attribution

Use `~` to add source information:

```
> All models are wrong, but some are useful. ~ article, Robustness in Statistics by George Box
```

Your AI will check existing notes first, then use the provided source information.

## Importers

Slipbot includes skill definitions for importing notes from external sources. Each importer parses the source format, shows a summary for confirmation, and then feeds each note through the standard Slipbot workflow (tagging, linking, graph update).

### Kindle Importer

Imports your reading notes from Kindle HTML/XHTML notebook exports. Extracts the book title and author automatically. Only imports your **Notes** (personal annotations) -- highlights of the book text are skipped.

```
- Applications should not allow unsigned JWTs ~ book, The JWT Handbook by Sebastian E Peyrott
```

### Instapaper Importer

Imports your notes from Instapaper highlight exports. Parses the article title and URL from the header. Only imports your **own notes** (plain text lines) -- original article highlights (`>` lines) are skipped.

```
- To learn faster we need faster feedback loops ~ article, How to Learn Faster
```

### Logseq Importer

Imports notes from Logseq pages with `key:: value` properties. Each bullet becomes an individual slipbox note. Nested bullets are flattened with parent context to remain standalone. All Logseq tags are stripped -- Slipbot generates its own tags based on content.

```
- Rewriting ideas helps decide their importance ~ Book, Digital Zettelkasten by David Kadavy
```

## Querying Your Knowledge Graph

Ask your AI assistant naturally:
- "Show me notes about spaced repetition"
- "Find quotes from George Box"
- "What notes link to the Lambda migration idea?"
- "What have I written about performance optimization?"

The AI searches the graph index first for speed, then falls back to file search if needed. See [docs/usage.md](docs/usage.md) for the full querying guide, including search by source, exploring connections, and discovery queries.

## Repository Structure

```
slipbot/
├── skills/
│   ├── slipbot/
│   │   └── SKILL.md                # Core note capture & management
│   ├── kindle-importer/
│   │   └── SKILL.md                # Kindle HTML export importer
│   ├── instapaper-importer/
│   │   └── SKILL.md                # Instapaper export importer
│   └── logseq-importer/
│       └── SKILL.md                # Logseq page importer
├── docs/
│   └── usage.md                    # Extended usage guide
├── README.md
└── LICENSE
```

## Note Storage (User Data)

Notes are stored in a `slipbox/` directory relative to where your agent operates:

```
slipbox/
├── 20260131-041700-note-title.md
├── 20260131-042000-another-note.md
├── missing.md                       # Tracks broken link references
└── .graph/
    └── graph.json                   # Knowledge graph index
```

## Knowledge Graph

Slipbot maintains a JSON knowledge graph at `slipbox/.graph/graph.json` that indexes all notes for fast querying. Each entry stores the note's title, type, source, tags, and links.

The graph is automatically updated on every note capture. If the graph becomes corrupted, your AI agent can rebuild it from the note files. Broken links are detected during validation and tracked in `slipbox/missing.md` for cleanup.

## Note Format

Each note is a markdown file with YAML frontmatter:

```yaml
---
title: "Knowledge Graph Design Thoughts"
date: 2026-01-25T14:30:22-05:00
type: idea
tags: [systems, notes, automation]
source:
  title: "Thinking, Fast and Slow"
  type: "book"
  author: "Daniel Kahneman"
links:
  - id: "20260120-093045-compound-interest"
    type: related
    reason: "Both discuss emergent complexity"
---

Note contents here in markdown...
```

- **Filenames** use the format `YYYYMMDD-HHMMSS-slug.md` (e.g., `20260131-143022-compound-interest.md`)
- **Titles** are generated by the AI: descriptive, 3-8 words, avoiding generic labels
- **Source** is set to `null` when no source is provided via `~`
- **Types**: `note`, `quote`, `idea`, `journal`

## How Linking Works

Your AI assistant automatically:
- Analyzes new note content against existing notes
- Identifies connection types:
  - **related**: Similar topic or theme
  - **extends**: Builds on or expands another note
  - **contradicts**: Opposing viewpoint or information
  - **references**: Mentions same person, book, concept
  - **supports**: Provides evidence for another note
- Updates frontmatter with bidirectional links, including a `reason` for each connection
- Validates links and tracks broken references in `slipbox/missing.md`

Quality over quantity -- links are only created when notes are genuinely related.

## Tagging Philosophy

Slipbot uses object-based tagging:
- **2-3 tags per note** -- enough for connections, not so many they lose meaning
- Tags are specific objects or concepts found in the note
- Not broad categories like "productivity" or "ideas"
- Focus on nouns: specific people, tools, techniques, systems
- Consistency is enforced by checking existing tags before creating new ones

**Example:**
- Bad: `[productivity, work, improvement]`
- Good: `[pomodoro-technique, deep-work, Cal-Newport]`

## Why Slipbot?

Traditional second brain systems fail because of maintenance overhead:

- Deciding where notes go
- Creating and maintaining taxonomies
- Linking related notes manually
- Keeping everything organized

Slipbot removes all of that. Your only job is to get thoughts out of your head. Your AI does the rest.

## Status

Slipbot is actively maintained.

## Contributing

Issues and pull requests are welcome. This is an evolving project built for the AI assistant community.

## License

GPL-3.0 - See [LICENSE](LICENSE) for details.
