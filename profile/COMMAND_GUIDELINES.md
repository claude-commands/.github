# Command Writing Guidelines

A comprehensive guide to creating Claude Code slash commands for the claude-commands project.

## Introduction

Claude Code slash commands are markdown files that expand into prompts when invoked. They let you automate
repetitive workflows, encode best practices, and extend Claude Code's capabilities.

**Philosophy:** Less prompting. More doing.

These commands exist to make Claude Code as automated as possible. Instead of explaining what you want
step-by-step, just tell it what to do and let it run.

This guide covers everything from your first command to publishing in the claude-commands org.

## Quick Start (5-minute command)

Create your first command in under 5 minutes:

### 1. Create the file

```bash
mkdir -p ~/.claude/commands
touch ~/.claude/commands/hello.md
```

### 2. Add minimal content

```markdown
---
description: Say hello and show system info
---

Say hello to the user and show them:
1. Current date and time: !date
2. Current directory: !pwd
3. A friendly greeting

Keep it brief and friendly.
```

### 3. Test it

Open Claude Code and type `/hello`. Your command will execute immediately.

That's it! You've created a working slash command.

## Complete Walkthrough: Building `/project-stats`

Let's build a real command from scratch, adding features incrementally.

### Step 1: Define the Goal

We want a command that shows project statistics: file counts, line counts, and detected languages.

### Step 2: Create the File

```markdown
---
description: Show project statistics
---

Analyze the current project and report:
- Total files and directories
- Lines of code by language
- Project size

Use tree and wc commands to gather stats.
```

### Step 3: Add Argument Handling

Commands that accept arguments should handle the empty case:

```markdown
---
description: Show project statistics
argument-hint: <path>
---

**If `$ARGUMENTS` is empty or not provided:**

Analyze the current directory.

---

**If `$ARGUMENTS` is provided:**

Analyze the path: $ARGUMENTS

---

**For either case, report:**

1. Total files and directories
2. Lines of code by language
3. Project size

Use tree, wc, and file detection to gather stats.
```

### Step 4: Add Tool Selection

Restrict tools for safety:

```markdown
---
description: Show project statistics
argument-hint: <path>
model: claude-opus-4-5-20251101
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
---
```

### Step 5: Add Interactivity

Ask what stats the user wants:

```markdown
---
description: Show project statistics
argument-hint: <path>
model: claude-opus-4-5-20251101
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
  - AskUserQuestion
---

**If `$ARGUMENTS` is empty or not provided:**

Analyze the current directory.

---

**If `$ARGUMENTS` is provided:**

Analyze the path: $ARGUMENTS

---

Ask the user what statistics they want:
- Quick overview (file counts only)
- Detailed (lines of code by language)
- Full report (everything including largest files)

Then gather and display the requested statistics.
```

### Step 6: Polish with Workflow Steps

Show users what will happen:

```markdown
---
description: Show project statistics
argument-hint: <path>
model: claude-opus-4-5-20251101
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
  - AskUserQuestion
---

**If `$ARGUMENTS` is empty or not provided:**

**Usage:** `/project-stats [path]`

**Example:** `/project-stats src/`

**What this does:**
1. Scans directory structure
2. Counts files by type
3. Calculates lines of code
4. Identifies languages used

Analyzing current directory...

---

**If `$ARGUMENTS` is provided:**

Analyzing: $ARGUMENTS

---

**Workflow:**

1. Ask user for detail level (quick/detailed/full)
2. Scan directory with tree
3. Count lines by file type
4. Generate formatted report

Display results in a clean, readable format.
```

### Step 7: Test Locally

1. Save to `~/.claude/commands/project-stats.md`
2. Run `/project-stats` in Claude Code
3. Test with arguments: `/project-stats src/`
4. Verify all paths work correctly

### Step 8: Prepare for Publishing

1. Create repo structure (see [Repository Setup](#repository-setup))
2. Write README with installation instructions
3. Lint markdown: `npx markdownlint-cli2 "**/*.md"`

## Command Anatomy

### Frontmatter Reference

Every command starts with YAML frontmatter:

| Field | Required | Purpose | Example |
|-------|----------|---------|---------|
| `description` | **Yes** | Shows in `/help`, enables discovery | `"Generate changelog from commits"` |
| `argument-hint` | No | Shows in autocomplete | `<issue-number>` |
| `model` | No | Model to use (always use Opus 4.5) | `claude-opus-4-5-20251101` |
| `allowed-tools` | No | Restrict available tools | `[Bash, Read, Edit]` |
| `disable-model-invocation` | No | Prevent programmatic invocation | `false` |

**Example frontmatter:**

```yaml
---
description: Create git worktree for a GitHub issue
argument-hint: <issue-number>
model: claude-opus-4-5-20251101
allowed-tools:
  - Bash
  - Read
  - Write
  - AskUserQuestion
---
```

### Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `$ARGUMENTS` | All arguments as a single string | `/cmd foo bar` → `"foo bar"` |
| `$1`, `$2`, etc. | Positional arguments | `/cmd foo bar` → `$1="foo"`, `$2="bar"` |
| `!command` | Inline bash execution | `!date` executes and substitutes output |

### Model Selection

**Always use Opus 4.5** (`claude-opus-4-5-20251101`) for all commands. It is faster and more accurate than
Sonnet for command execution.

## The Argument Pattern

Every command that accepts arguments **MUST** handle the empty case. This is critical for good UX.

**Pattern template:**

```markdown
---
description: Your command description
argument-hint: <your-arg>
---

**If `$ARGUMENTS` is empty or not provided:**

Display usage information:

**Usage:** `/your-command <arg>`

**Example:** `/your-command example-value`

**What this command does:**
1. Step one
2. Step two
3. Step three

Ask the user: "Please provide [what you need]"

---

**If `$ARGUMENTS` is provided:**

[Your normal execution flow using $ARGUMENTS]
```

**Why this matters:**

- Users often invoke commands without reading docs first
- Clear usage info teaches them the correct syntax
- Asking for input keeps the workflow moving

## Common Patterns

### Git/GitHub Integration

Most workflow commands interact with git and GitHub:

```markdown
**Prerequisites check:**
1. Verify we're in a git repository: !git rev-parse --git-dir
2. Check GitHub CLI is authenticated: !gh auth status
3. Ensure working directory is clean: !git status --porcelain

**Common operations:**
- Get current branch: !git branch --show-current
- List open PRs: !gh pr list
- Get issue details: !gh issue view $1
- Create branch: !git checkout -b feature/$1
```

### Multi-Step Workflows

Break complex operations into numbered steps:

```markdown
**Workflow:**

1. **Analyze** - Read the issue and understand requirements
2. **Plan** - Determine files to modify and approach
3. **Implement** - Make the changes
4. **Test** - Run relevant tests
5. **Commit** - Create atomic commit with conventional message
6. **PR** - Open pull request with summary

Before each destructive step, confirm with user.
```

### Project Type Detection

Adapt behavior based on the project:

```markdown
**Detect project type:**

Check for these files to determine project type:
- `go.mod` → Go project
- `package.json` → Node.js/TypeScript
- `Cargo.toml` → Rust
- `pyproject.toml` or `requirements.txt` → Python
- `Gemfile` → Ruby

Adapt commands and paths based on detected type.
```

### Interactive Commands

Use `AskUserQuestion` for decisions:

```markdown
When multiple approaches are valid, ask the user:
- Which implementation style do they prefer?
- Should we include tests?
- What level of detail in the output?

Keep questions focused and provide clear options.
```

## Tool Selection

### Recommended Tools by Use Case

| Use Case | Recommended Tools |
|----------|-------------------|
| Read-only analysis | `Read`, `Glob`, `Grep`, `Bash` |
| Code modification | Above + `Edit`, `Write` |
| Interactive workflows | Above + `AskUserQuestion` |
| Git/GitHub operations | `Bash` (for git/gh commands) |
| Web research | `WebSearch`, `WebFetch` |

### Tool Restrictions

Use `allowed-tools` to limit what a command can do:

```yaml
# Read-only command - can't modify files
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep

# Full access for code generation
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
```

**When to restrict:**

- Analysis commands should be read-only
- Dangerous operations should require explicit tools
- Simpler tool sets = faster, more focused execution

## Writing Style Guide

### Do

- Use imperative mood: "Create the file" not "Creating the file"
- Show realistic examples: `/start-issue 123` not `/start-issue <number>`
- Explain workflow steps upfront so users know what's coming
- Keep instructions concise but complete
- Include error handling for common failures

### Don't

- Add unnecessary confirmations (philosophy: less prompting)
- Use placeholder values in examples
- Write walls of text - break into numbered steps
- Assume tools are available without checking

## Repository Setup

### Naming Convention

- **Repository:** `command-{name}` (e.g., `command-standup`)
- **Main file:** `{name}.md` (e.g., `standup.md`)
- **Organization:** [github.com/claude-commands](https://github.com/claude-commands)

### Required Files

```text
command-{name}/
├── {name}.md    # The command itself
└── README.md    # Installation and usage docs
```

Note: Markdownlint configuration lives at the repository root level, not per-command.

### README Template

```markdown
# /{name}

One-line description of what this command does.

## Installation

Clone and symlink:

\`\`\`bash
git clone git@github.com:claude-commands/command-{name}.git ~/path/to/command-{name}
ln -s ~/path/to/command-{name}/{name}.md ~/.claude/commands/{name}.md
\`\`\`

Or use the [/claude-commands](https://github.com/claude-commands/command-claude-commands) manager.

## Usage

\`\`\`text
/{name}              # Basic usage
/{name} <arg>        # With argument
\`\`\`

## What It Does

1. Step one
2. Step two
3. Step three

## Requirements

- [Claude Code](https://claude.ai/code)
- [GitHub CLI](https://cli.github.com/) (if using GitHub features)
```

## Testing Your Command

### Local Testing Workflow

1. **Create/edit** your command in `~/.claude/commands/`
2. **Test basic invocation:** Run the command with no arguments
3. **Test with arguments:** Verify argument handling works
4. **Test edge cases:** Empty directories, missing files, etc.
5. **Verify tool access:** Ensure allowed-tools is correct

### Common Issues

| Issue | Cause | Fix |
|-------|-------|-----|
| Command not in autocomplete | Missing `description` | Add description to frontmatter |
| Arguments not passed | Syntax error | Check `$ARGUMENTS` or `$1` usage |
| Tool not available | Not in allowed-tools | Add tool to frontmatter or remove restriction |
| Command too slow | Model not specified | Add `model: claude-opus-4-5-20251101` |

### Debugging Tips

- Test frontmatter parsing: Remove body, verify metadata shows in `/help`
- Check variable expansion: Add debug output like `Arguments received: $ARGUMENTS`
- Verify bash execution: Test `!command` syntax with simple commands first

## Publishing Checklist

Before publishing a command to the claude-commands org:

- [ ] Repository named `command-{name}`
- [ ] Main file named `{name}.md`
- [ ] Frontmatter includes `description`
- [ ] Empty argument case handled (if command takes arguments)
- [ ] Model set to `claude-opus-4-5-20251101`
- [ ] `allowed-tools` specified (if restricting)
- [ ] README.md with installation instructions
- [ ] Realistic usage examples included
- [ ] Markdown linted: `npx markdownlint-cli2 "**/*.md"`
- [ ] Tested locally with various inputs

## Examples Gallery

Study these commands for patterns:

### Simple (No Arguments)

**`/standup`** - Generates standup notes from recent git activity

- No arguments needed
- Read-only (git log analysis)
- Single-purpose, focused output

### With Arguments

**`/start-issue`** - Creates git worktree for a GitHub issue

- Takes issue number as argument
- Handles empty argument case with usage info
- Integrates git and GitHub CLI

### Interactive

**`/refactor`** - AI-guided refactoring with safety checks

- Asks user about scope and approach
- Confirms before making changes
- Uses AskUserQuestion for decisions

### Complex Multi-Step

**`/add-feature`** - Implements feature from issue with tests and PR

- Full TDD workflow
- Multiple phases (analyze, implement, test, PR)
- Heavy git/GitHub integration

## Troubleshooting

### Command Not Appearing in Autocomplete

**Cause:** Missing or malformed `description` in frontmatter

**Fix:** Ensure your frontmatter has a valid description:

```yaml
---
description: What your command does
---
```

### Arguments Not Being Passed

**Cause:** Using wrong variable syntax

**Fix:** Use `$ARGUMENTS` for full string or `$1`, `$2` for positional:

```markdown
Full arguments: $ARGUMENTS
First argument: $1
Second argument: $2
```

### Tools Not Available

**Cause:** `allowed-tools` doesn't include needed tool

**Fix:** Either add the tool or remove the restriction:

```yaml
allowed-tools:
  - Bash
  - Read
  - Edit  # Add missing tool
```

### Markdown Parsing Issues

**Cause:** Invalid YAML or markdown syntax

**Fix:**

1. Validate YAML frontmatter (proper indentation, quotes)
2. Run `npx markdownlint-cli2 yourfile.md`
3. Check for unclosed code blocks

---

## Getting Help

- Use `/create-command` to scaffold new commands with best practices
- Browse [existing commands](https://github.com/claude-commands) for patterns
- Open an issue for questions or suggestions

---

Made with Claude Code
