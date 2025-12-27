# Claude Code Configuration

My Claude Code settings, agents, and project configurations.

## Structure

```
├── global/                    # Global settings (~/.claude/)
│   ├── CLAUDE.md             # Global instructions
│   ├── settings.json         # Permissions & model config
│   ├── settings.local.json   # Local overrides
│   └── agents/               # Custom subagents
│       ├── code-reviewer.md
│       ├── debugger.md
│       ├── refactorer.md
│       └── test-writer.md
└── projects/                  # Project-specific CLAUDE.md files
    ├── Autonomous-coding-CLAUDE.md
    ├── Email-replier-CLAUDE.md
    └── KaiSign-Extension-CLAUDE.md
```

## Installation

Copy global settings to your home:
```bash
cp -r global/agents ~/.claude/
cp global/settings.json ~/.claude/
cp global/CLAUDE.md ~/
```

## Agents

| Agent | Purpose |
|-------|---------|
| `code-reviewer` | Review code for bugs, security, best practices |
| `debugger` | Trace code paths, identify root causes |
| `refactorer` | Clean up code structure |
| `test-writer` | Generate unit/integration tests |
