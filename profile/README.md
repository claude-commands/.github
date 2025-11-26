# Claude Commands

A collection of slash commands for [Claude Code](https://claude.ai/code) - Anthropic's CLI coding assistant.

## Available Commands

| Command | Description | Install |
|---------|-------------|---------|
| [command-add-feature](https://github.com/claude-commands/command-add-feature) | Implement features from GitHub issues with tests and PR | `/add-feature 123` |
| [command-fix-issue](https://github.com/claude-commands/command-fix-issue) | Fix bugs using TDD workflow | `/fix-issue 456` |
| [command-start-issue](https://github.com/claude-commands/command-start-issue) | Create git worktrees for issues | `/start-issue 789` |
| [command-prune-worktree](https://github.com/claude-commands/command-prune-worktree) | Clean up completed worktrees | `/prune-worktree` |
| [command-codex](https://github.com/claude-commands/command-codex) | Delegate tasks to OpenAI Codex CLI | `/codex <prompt>` |

## Quick Start

```bash
# Clone to your preferred location
git clone git@github.com:claude-commands/command-add-feature.git <clone-path>/command-add-feature

# Symlink (use full path to cloned repo)
ln -s <clone-path>/command-add-feature/add-feature.md ~/.claude/commands/add-feature.md
```

## Installation Pattern

Each command is a separate repo you can clone and symlink:

1. **Clone** the repo to your preferred location
2. **Symlink** the `.md` file to `~/.claude/commands/`
3. **Use** the command in Claude Code with `/{command-name}`

## Updating Commands

```bash
# Update all commands (adjust path to your clone location)
for dir in <clone-path>/command-*/; do
  (cd "$dir" && git pull)
done
```

## Configuration

Some commands support configuration via environment variables:

```bash
# Set project prefix for worktree commands
export WORKTREE_PREFIX="my-project"
```

See individual command READMEs for details.

## Requirements

- [Claude Code](https://claude.ai/code) CLI
- `gh` CLI for GitHub integration
- Git

## Contributing

Want to add your own commands? Fork any command repo as a template, or create a new one following the pattern:

- Repo name: `command-{name}`
- Main file: `{name}.md` with frontmatter
- Include: `README.md` with installation and usage

---

Made with Claude Code
