# Slipbot Updates for MoltBot/Clawdbot

## Summary

Converted Slipbot from OpenCode-specific tool to a general-purpose AI assistant skill for MoltBot, Clawdbot, and compatible systems.

## What Changed

### Removed
- `.opencode/commands/note.md` - OpenCode-specific command file

### Added
- `skill/SKILL.md` - Comprehensive AI assistant instructions
- `docs/usage.md` - User guide for capturing and querying notes
- `examples/` - Three example notes showing format
  - `20260120-093045-compound-interest.md` (note)
  - `20260118-142233-warren-buffett-quote.md` (quote with bidirectional links)
  - `20260125-160000-zettelkasten-ai.md` (idea)

### Updated
- `README.md` - Rewritten for MoltBot/Clawdbot users
- `.gitignore` - Updated to exclude user data

## Key Changes

### 1. Source Validation
**Before:** Planned to query Google Books API  
**After:** No external APIs - uses provided source info and checks existing notes

**Rationale:** Simpler, faster, no external dependencies for personal knowledge management

### 2. Directory Structure
**Before:** `/home/jrswab/notes/`  
**After:** `sync/slipbox/` with graph at `sync/slipbox/.graph/graph.json`

**Rationale:** 
- Works with Syncthing for cross-device sync
- Clear, descriptive naming ("slipbox" = Zettelkasten term)
- Graph in subdirectory keeps things organized

### 3. Activation
**Before:** `/note` command in OpenCode  
**After:** Natural language recognition

**Patterns:**
- `note: {content}`
- `quote: {content}`
- `remember this: {content}`
- Prefix-based: `>` (quote), `!` (idea), `*` (journal)
- Context-aware recognition

### 4. AI Assistant Integration
**Before:** OpenCode-specific  
**After:** Works with any AI assistant that can:
- Read/write files
- Search existing notes
- Maintain JSON graph index

## File Structure

```
slipbot/                              # Repository (commit this to GitHub)
├── README.md                         # User-facing documentation
├── LICENSE                           # GPL-3.0
├── .gitignore                        # Excludes user data
├── CHANGES.md                        # This file
├── skill/
│   └── SKILL.md                      # AI assistant instructions
├── docs/
│   └── usage.md                      # How to use guide
└── examples/
    ├── 20260118-142233-warren-buffett-quote.md
    ├── 20260120-093045-compound-interest.md
    └── 20260125-160000-zettelkasten-ai.md

sync/slipbox/                         # User data (not in repo)
├── .graph/
│   └── graph.json                    # Knowledge graph index
└── *.md                              # User's notes (created as captured)
```

## Ready to Commit

The repository in `/home/moltbot/sync/slipbot/` is ready for you to commit to GitHub.

## What Happens Next

When you or other users clone this repo:
1. AI assistant reads `skill/SKILL.md` to learn how Slipbot works
2. User syncs files via Syncthing (or manually manages `sync/slipbox/`)
3. AI recognizes note capture patterns and handles everything automatically

No configuration needed - just start capturing notes.

## Testing

You can test immediately:
1. Tell me: `note: This is a test of Slipbot`
2. I'll create the file in `sync/slipbox/`
3. Check that the note was created with proper frontmatter
4. Try querying: "Show me my Slipbot test note"

---

**Note:** The `sync/slipbox/` directory with your actual notes is separate from the repository. Only the tools/docs are in git.
