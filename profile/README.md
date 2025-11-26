# Claude Commands

Slash commands for [Claude Code](https://claude.ai/code) - Anthropic's CLI coding assistant.

## Philosophy

**We hate typing. We hate confirming. We want AI that thinks like us and executes like it's us.**

These commands exist to make Claude Code as automated as possible. Instead of explaining what you want
step-by-step, just tell it what to do and let it run. The goal: Claude should know how you think and
execute with the full power of AI.

Less prompting. More doing.

## Getting Started

Install the `/claude-commands` manager, then use it to discover and install everything else:

```bash
# Clone to your preferred location
git clone git@github.com:claude-commands/command-claude-commands.git <clone-path>/command-claude-commands

# Symlink (use full path to cloned repo)
ln -s <clone-path>/command-claude-commands/claude-commands.md ~/.claude/commands/claude-commands.md
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

```text
/claude-commands              # Interactive menu
/claude-commands install      # Install all or select specific commands
/claude-commands add <name>   # Add a single command
/claude-commands remove <name># Remove a command
/claude-commands update       # Update all installed commands
/claude-commands list         # Show what's installed vs available
```

## Available Commands (47)

### Issue & Git Workflow

| Command | Description |
|---------|-------------|
| [/start-issue](https://github.com/claude-commands/command-start-issue) | Create git worktrees for GitHub issues |
| [/add-feature](https://github.com/claude-commands/command-add-feature) | Implement features from issues with tests and PR |
| [/fix-issue](https://github.com/claude-commands/command-fix-issue) | Fix bugs using TDD workflow |
| [/prune-worktree](https://github.com/claude-commands/command-prune-worktree) | Clean up merged worktrees |
| [/branch-cleanup](https://github.com/claude-commands/command-branch-cleanup) | Clean stale and merged git branches |
| [/merge-ready](https://github.com/claude-commands/command-merge-ready) | Find and merge PRs that are approved and passing CI |
| [/rebase-all](https://github.com/claude-commands/command-rebase-all) | Rebase multiple branches onto a target branch |
| [/cherry-pick-prs](https://github.com/claude-commands/command-cherry-pick-prs) | Cherry-pick commits from PRs to other branches |
| [/hotfix](https://github.com/claude-commands/command-hotfix) | Create and manage hotfix branches with release workflow |
| [/sync-fork](https://github.com/claude-commands/command-sync-fork) | Sync forked repository with upstream changes |

### Daily Workflow

| Command | Description |
|---------|-------------|
| [/standup](https://github.com/claude-commands/command-standup) | Generate standup notes from git commits |
| [/pr-summary](https://github.com/claude-commands/command-pr-summary) | Generate PR description from branch changes |
| [/weekly-summary](https://github.com/claude-commands/command-weekly-summary) | Generate weekly work summary from git activity |
| [/review-prs](https://github.com/claude-commands/command-review-prs) | Review PRs with AI-generated suggestions |
| [/my-prs](https://github.com/claude-commands/command-my-prs) | Check status of your open PRs across repos |
| [/git-stats](https://github.com/claude-commands/command-git-stats) | Git repository statistics and insights |
| [/suggest-reviewers](https://github.com/claude-commands/command-suggest-reviewers) | Suggest reviewers based on code ownership and expertise |

### Code Quality & Analysis

| Command | Description |
|---------|-------------|
| [/explain](https://github.com/claude-commands/command-explain) | Deep-dive code explanation with Mermaid diagrams |
| [/tech-debt](https://github.com/claude-commands/command-tech-debt) | Analyze codebase for technical debt and complexity |
| [/refactor](https://github.com/claude-commands/command-refactor) | AI-guided refactoring with safety checks |
| [/dead-code](https://github.com/claude-commands/command-dead-code) | Find unused code, exports, and dependencies |
| [/profile](https://github.com/claude-commands/command-profile) | Performance profiling and optimization suggestions |
| [/explain-diff](https://github.com/claude-commands/command-explain-diff) | Explain changes between commits, branches, or files |
| [/lint-fix](https://github.com/claude-commands/command-lint-fix) | Auto-fix linting issues across the codebase |
| [/todo-scan](https://github.com/claude-commands/command-todo-scan) | Find and track TODO/FIXME comments in codebase |

### Testing

| Command | Description |
|---------|-------------|
| [/test-gen](https://github.com/claude-commands/command-test-gen) | Generate comprehensive tests with edge cases |
| [/test-coverage](https://github.com/claude-commands/command-test-coverage) | Analyze test coverage and generate missing tests |
| [/failing-tests](https://github.com/claude-commands/command-failing-tests) | Debug and fix failing tests |
| [/mock-data](https://github.com/claude-commands/command-mock-data) | Generate realistic test data from types or schemas |

### Code Generation

| Command | Description |
|---------|-------------|
| [/scaffold](https://github.com/claude-commands/command-scaffold) | Generate project scaffolding following existing patterns |
| [/convert](https://github.com/claude-commands/command-convert) | Convert between formats, languages, and data structures |
| [/migration](https://github.com/claude-commands/command-migration) | Database migration helper with schema analysis |

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
| [/deps-upgrade](https://github.com/claude-commands/command-deps-upgrade) | Intelligent dependency upgrades with breaking change analysis |

### Debugging & Environment

| Command | Description |
|---------|-------------|
| [/debug](https://github.com/claude-commands/command-debug) | Intelligent error analysis and resolution |
| [/env-check](https://github.com/claude-commands/command-env-check) | Verify development environment setup |
| [/logs](https://github.com/claude-commands/command-logs) | Analyze log files for issues and patterns |

### Onboarding & Context

| Command | Description |
|---------|-------------|
| [/onboard](https://github.com/claude-commands/command-onboard) | Quick project onboarding and architecture overview |
| [/context-dump](https://github.com/claude-commands/command-context-dump) | Save and restore working context for later sessions |

### Project Setup

| Command | Description |
|---------|-------------|
| [/init-project](https://github.com/claude-commands/command-init-project) | Initialize new project with best practices |
| [/add-ci](https://github.com/claude-commands/command-add-ci) | Add CI/CD configuration to existing project |

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
# Clone to your preferred location
git clone git@github.com:claude-commands/command-standup.git <clone-path>/command-standup

# Symlink (use full path to cloned repo)
ln -s <clone-path>/command-standup/standup.md ~/.claude/commands/standup.md
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

**Disclaimer:** This project is not affiliated with, endorsed by, or sponsored by Anthropic. We're just
developers who love Claude Code and want to make it even more powerful. All trademarks belong to their
respective owners.
