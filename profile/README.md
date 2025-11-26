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

## Available Commands (27)

### Issue & Git Workflow

| Command | Description |
|---------|-------------|
| [/start-issue](https://github.com/claude-commands/command-start-issue) | Create git worktrees for GitHub issues |
| [/add-feature](https://github.com/claude-commands/command-add-feature) | Implement features from issues with tests and PR |
| [/fix-issue](https://github.com/claude-commands/command-fix-issue) | Fix bugs using TDD workflow |
| [/prune-worktree](https://github.com/claude-commands/command-prune-worktree) | Clean up merged worktrees |
| [/branch-cleanup](https://github.com/claude-commands/command-branch-cleanup) | Clean stale and merged git branches |

### Daily Workflow

| Command | Description |
|---------|-------------|
| [/standup](https://github.com/claude-commands/command-standup) | Generate standup notes from git commits |
| [/pr-summary](https://github.com/claude-commands/command-pr-summary) | Generate PR description from branch changes |
| [/weekly-summary](https://github.com/claude-commands/command-weekly-summary) | Generate weekly work summary from git activity |
| [/review-prs](https://github.com/claude-commands/command-review-prs) | Review PRs with AI-generated suggestions |
| [/my-prs](https://github.com/claude-commands/command-my-prs) | Check status of your open PRs across repos |

### Code Quality & Analysis

| Command | Description |
|---------|-------------|
| [/explain](https://github.com/claude-commands/command-explain) | Deep-dive code explanation with Mermaid diagrams |
| [/tech-debt](https://github.com/claude-commands/command-tech-debt) | Analyze codebase for technical debt and complexity |
| [/refactor](https://github.com/claude-commands/command-refactor) | AI-guided refactoring with safety checks |
| [/dead-code](https://github.com/claude-commands/command-dead-code) | Find unused code, exports, and dependencies |

### Testing

| Command | Description |
|---------|-------------|
| [/test-gen](https://github.com/claude-commands/command-test-gen) | Generate comprehensive tests with edge cases |
| [/test-coverage](https://github.com/claude-commands/command-test-coverage) | Analyze test coverage and generate missing tests |
| [/failing-tests](https://github.com/claude-commands/command-failing-tests) | Debug and fix failing tests |

### Documentation

| Command | Description |
|---------|-------------|
| [/api-docs](https://github.com/claude-commands/command-api-docs) | Generate API documentation from code |
| [/doc-sync](https://github.com/claude-commands/command-doc-sync) | Keep documentation in sync with code changes |

### Releases & Changelog

| Command | Description |
|---------|-------------|
| [/changelog](https://github.com/claude-commands/command-changelog) | Generate changelog from commits (Keep a Changelog format) |
| [/release](https://github.com/claude-commands/command-release) | Prepare release with version bump and changelog |

### Security & Dependencies

| Command | Description |
|---------|-------------|
| [/security-scan](https://github.com/claude-commands/command-security-scan) | Security vulnerability assessment and secrets detection |
| [/deps-check](https://github.com/claude-commands/command-deps-check) | Security, outdated, and unused dependency analysis |

### Debugging & Environment

| Command | Description |
|---------|-------------|
| [/debug](https://github.com/claude-commands/command-debug) | Intelligent error analysis and resolution |
| [/env-check](https://github.com/claude-commands/command-env-check) | Verify development environment setup |

### Onboarding & Context

| Command | Description |
|---------|-------------|
| [/onboard](https://github.com/claude-commands/command-onboard) | Quick project onboarding and architecture overview |

### AI Delegation

| Command | Description |
|---------|-------------|
| [/codex](https://github.com/claude-commands/command-codex) | Delegate tasks to OpenAI Codex CLI |

## Requirements

- [Claude Code](https://claude.ai/code) CLI
- [GitHub CLI](https://cli.github.com/) (`gh`) - authenticated
- Git

## Manual Installation

Prefer to install commands individually? Each repo includes installation instructions:

```bash
# Example: Install /standup
git clone git@github.com:claude-commands/command-standup.git ~/projects/claude-commands/command-standup
ln -sf ~/projects/claude-commands/command-standup/standup.md ~/.claude/commands/standup.md
```

## Contributing

Create a new command following the pattern:
- Repo: `command-{name}`
- Main file: `{name}.md` with frontmatter
- Include: `README.md` with usage docs
- Model: Always use `claude-opus-4-5-20251101`

See the [Command Writing Guidelines](https://github.com/claude-commands/.github) for best practices.

---

Made with Claude Code

---

**Disclaimer:** This project is not affiliated with, endorsed by, or sponsored by Anthropic. We're just developers who love Claude Code and want to make it even more powerful. All trademarks belong to their respective owners.
