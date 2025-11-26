# Claude Commands

Slash commands for [Claude Code](https://claude.ai/code) - Anthropic's CLI coding assistant.

## Philosophy

**We hate typing. We hate confirming. We want AI that thinks like us and executes like it's us.**

These commands exist to make Claude Code as automated as possible. Instead of explaining what you want step-by-step, just tell it what to do and let it run. The goal: Claude should know how you think and execute with the full power of AI.

Less prompting. More doing.

## Getting Started

Install the `/claude-commands` manager, then use it to discover and install everything else:

```bash
mkdir -p ~/projects/claude-commands ~/.claude/commands && \
git clone git@github.com:claude-commands/command-claude-commands.git ~/projects/claude-commands/command-claude-commands && \
ln -sf ~/projects/claude-commands/command-claude-commands/claude-commands.md ~/.claude/commands/claude-commands.md
```

Then run `/claude-commands` in Claude Code.

### Why Start Here?

The `/claude-commands` manager:
- **Discovers** all available commands from this org automatically
- **Installs** commands with proper symlinks in one step
- **Updates** all your installed commands at once
- **Removes** commands cleanly when you're done

No need to manually track repos or remember installation steps for each command.

### Managing Commands

```
/claude-commands              # Interactive menu
/claude-commands install      # Install all or select specific commands
/claude-commands add <name>   # Add a single command
/claude-commands remove <name># Remove a command
/claude-commands update       # Update all installed commands
/claude-commands list         # Show what's installed vs available
```

## Available Commands

Browse the `command-*` repositories in this org, or run `/claude-commands list` to see descriptions.

Commands are organized by workflow:

**Issue Workflow**
- [command-start-issue](https://github.com/claude-commands/command-start-issue) - Create git worktrees for issues
- [command-add-feature](https://github.com/claude-commands/command-add-feature) - Implement features with tests and PR
- [command-fix-issue](https://github.com/claude-commands/command-fix-issue) - Fix bugs using TDD workflow
- [command-prune-worktree](https://github.com/claude-commands/command-prune-worktree) - Clean up merged worktrees

**AI Delegation**
- [command-codex](https://github.com/claude-commands/command-codex) - Delegate tasks to OpenAI Codex

*More commands are being added regularly. Run `/claude-commands list` to see the latest.*

## Requirements

- [Claude Code](https://claude.ai/code) CLI
- [GitHub CLI](https://cli.github.com/) (`gh`) - authenticated
- Git

## Manual Installation

Prefer to install commands individually? See each repo's README for instructions.

## Contributing

Create a new command following the pattern:
- Repo: `command-{name}`
- Main file: `{name}.md` with frontmatter
- Include: `README.md` with usage docs

See the [Command Writing Guidelines](https://github.com/claude-commands/.github) for best practices.

---

Made with Claude Code

---

**Disclaimer:** This project is not affiliated with, endorsed by, or sponsored by Anthropic. We're just developers who love Claude Code and want to make it even more powerful. All trademarks belong to their respective owners.
