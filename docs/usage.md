# Slipbot Usage Guide

This guide covers common workflows and queries for using Slipbot with your AI assistant.

## Capturing Notes

### Basic Note

```
note: The Pomodoro Technique uses 25-minute focused work intervals followed by 5-minute breaks.
```

Your AI will:
- Create a note file with timestamp
- Tag it with relevant objects (Pomodoro-technique, time-management, focus)
- Link to related notes if any exist
- Update the knowledge graph

### Quote with Source

```
quote: "The only way to do great work is to love what you do." - Steve Jobs, Stanford Commencement 2005
```

Or use the `>` prefix:

```
> The only way to do great work is to love what you do. - Steve Jobs
```

### Ideas

Prefix with `!` or use explicit marking:

```
! What if we used event sourcing for the file processing pipeline?
```

### Journal Entries

Prefix with `*`:

```
* Today I realized that the bottleneck in our Excel ingestion was database operations in the hot path.
```

### Natural Capture

Just tell your AI naturally:

```
Remember this: Cal Newport's Deep Work concept pairs well with the Pomodoro Technique.
```

```
I want to save this thought: The best abstractions are discovered, not designed upfront.
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

Tag project-specific notes:

```
note: Lambda migration eliminated 10,000+ Sentry errors - tags: [Lambda, serverless, data-platform, Gloo]
```

Later:
```
Show me all notes about the Lambda migration
```

### Book Notes

As you read:

```
quote: "Your limitation—it's only your imagination." - Source: Zero to One, Peter Thiel
```

```
note: Thiel argues that competition is for losers—monopolies drive innovation. - Source: Zero to One
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

Check that you used a recognized pattern:
- `note: ...`
- `quote: ...`
- Prefix with `>`, `!`, or `*`
- Or tell your AI explicitly to remember something

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
