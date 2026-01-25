# Slipbot

Capture notes, ideas, quotes, and more while LLMs take care of the friction that comes with maintaining a second brain.

## What is Slipbot?

Slipbot is a command for agentic LLM applications (OpenCode, ClaudeCode, etc.) that eliminates the overhead of maintaining a second brain system. Instead of worrying about organization, tags, categories, or where things go, you just capture your thoughts and let the LLM handle everything else.

## How It Works

The workflow is simple:

1. Type `/note "your thought here"` in your agentic application
2. The LLM processes and organizes your note automatically
3. Your second brain grows without manual maintenance

That's it. No folders to organize, no tags to remember, no systems to maintain.

## Installation

### Requirements

You need an agentic application that can run commands:
- [OpenCode](https://opencode.ai)
- [ClaudeCode](https://claude.ai/code)
- Or another agentic system with command support

### Setup

1. Clone this repository or download the `.opencode/commands` directory
2. Place the command files in your agentic application's commands directory
3. Start your agentic application
4. Begin capturing notes with `/note "your content"`

## Usage

Basic note capture:
```
/note "Research idea: explore the relationship between retrieval practice and spaced repetition"
```

Capture quotes:
```
/note "The best time to plant a tree was 20 years ago. The second best time is now."
```

Quick thoughts:
```
/note "Need to investigate why the cache invalidation is slow on production"
```

The LLM handles categorization, linking, and organization based on the content and context of your notes.

## Why Slipbot?

Traditional second brain systems fail because of maintenance overhead:
- Deciding where notes go
- Creating and maintaining taxonomies
- Linking related notes manually
- Keeping everything organized

Slipbot removes all of that. Your only job is to get thoughts out of your head. The LLM does the rest.

## Status

Slipbot is currently a working prototype. It's functional and useful for daily note capture, but expect changes as the system evolves.

## License

GPL-3.0 - See [LICENSE](LICENSE) for details.

## Contributing

Issues and pull requests are welcome. This is an early-stage project, so there's plenty of room for improvement and experimentation.
