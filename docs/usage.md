# Slipbot Usage Guide

This guide covers common workflows and queries for using Slipbot with your AI assistant.

## Capturing Notes

### Basic Note

```
- The Pomodoro Technique uses 25-minute focused work intervals followed by 5-minute breaks.
```

Your AI will:
- Create a note file with timestamp
- Tag it with relevant concepts (Pomodoro-technique, focus)
- Link to related notes if any exist
- Update the knowledge graph

### Quote with Source

```
> The only way to do great work is to love what you do. ~ speech, Stanford Commencement 2005 by Steve Jobs
```

### Ideas

Prefix with `!`:

```
! What if we used event sourcing for the file processing pipeline?
```

### Journal Entries

Prefix with `*`:

```
* Today I realized that the bottleneck in our Excel ingestion was database operations in the hot path.
```

## Querying Your Knowledge Graph

### Find Related Notes

```
Show me notes about performance optimization
```

```
What have I written about Zettelkasten?
```

### Search by Source

```
Find quotes from Morgan Housel
```

```
Show me notes from "Thinking, Fast and Slow"
```

### Explore Connections

```
What notes link to my Lambda migration idea?
```

```
Show me all notes tagged with "compound-interest"
```

### Discovery

```
What topics do I write about most?
```

```
Which notes have the most connections?
```

## Maintenance

### Check Graph Health

```
Check my knowledge graph for broken links
```

```
Are there any duplicate notes I should merge?
```

### Rebuild Index

If the graph index gets corrupted:

```
Rebuild my knowledge graph from the note files
```

## Tips

### Capture Often

Don't wait for "complete" thoughts. Capture fragments and ideas as they come. Your AI will help connect them later.

### Review Periodically

Ask your AI to show you notes from a specific timeframe:

```
Show me notes from last week
```

```
What ideas did I capture in January?
```

### Trust the System

Don't worry about perfect organization upfront. The graph evolves as you capture more notes and connections emerge.

### Be Specific in Queries

Instead of:
```
Show me notes about work
```

Try:
```
Show me notes about deep work or focus techniques
```

## Advanced Workflows

### Building Arguments

When exploring a topic:

1. Capture notes with supporting evidence
2. Capture contradicting viewpoints
3. Ask your AI to show the network of related notes
4. Use the graph to build well-rounded understanding

### Project Notes

Capture project-specific notes:

```
- Lambda migration eliminated 10,000+ Sentry errors
```

Later:
```
Show me all notes about the Lambda migration
```

### Book Notes

As you read:

```
> Your limitation—it's only your imagination. ~ book, Zero to One by Peter Thiel
```

```
- Thiel argues that competition is for losers—monopolies drive innovation. ~ book, Zero to One by Peter Thiel
```

Then:
```
Show me my notes from Zero to One
```

## Integration with Other Systems

### Daily Logs

If you keep daily logs (like `memory/YYYY-MM-DD.md`), you can reference Slipbox notes:

```
See slipbox/20260131-143000-lambda-performance.md for details on the optimization
```

### Long-term Memory

Major insights from Slipbox can be promoted to `MEMORY.md` for permanent reference.

### Project Documentation

Link to relevant Slipbox notes from project docs:

```markdown
## Performance Optimization

See notes:
- [Compound Interest Optimization](../slipbox/20260120-093045-compound-interest.md)
- [Lambda Batching](../slipbox/20260131-143000-lambda-batching.md)
```

## Troubleshooting

### Note Not Created

Check that you used a recognized prefix:
- `>` for quotes
- `!` for ideas
- `*` for journal entries
- `-` for notes
- Use `~` to add source attribution (e.g., `> Quote text ~ book, Title by Author`)

### Links Not Working

Ask your AI to check graph integrity:
```
Validate my knowledge graph
```

### Can't Find a Note

Try different queries:
```
Search my notes for "Lambda"
```

```
Show me all notes from January
```

---

**Remember:** Slipbot is designed to reduce friction. If you find yourself spending time organizing, you're probably overthinking it. Capture thoughts, trust the AI to organize, and query when you need something.
