---
description: Create new slash commands with standardized structure
argument-hint: [name] [purpose]
allowed-tools: Bash(mkdir:*), Bash(tee:*), Bash(test:*)
---

# /create-command

## Purpose
Generate properly structured slash command files for Claude Code.

## Contract

**Inputs:**
- `$1` — COMMAND_NAME (lowercase, kebab-case, verb-first)
- `$2` — PURPOSE (command description)

**Outputs:**
- `STATUS=<WROTE> PATH=<path>`

## Instructions

1. **Validate inputs:**
   - Command name: lowercase, kebab-case only
   - Purpose: non-empty string

2. **Generate file content** using this template:
```markdown
---
description: {{PURPOSE}}
argument-hint: [args...]
---

# /{{COMMAND_NAME}}

## Purpose
{{PURPOSE}}

## Contract
**Inputs:** `$ARGUMENTS` — command arguments
**Outputs:** `STATUS=<OK|FAIL> [key=value ...]`

## Instructions
1. Validate inputs
2. Execute primary action
3. Print STATUS line

## Constraints
- Idempotent and deterministic
- No network tools by default
- Minimal console output (STATUS line only)
```

3. **Output:**
   - Show preview in fenced markdown block
   - Create `.claude/commands/` dir and write file atomically
   - Print: `STATUS=WROTE PATH=.claude/commands/{{COMMAND_NAME}}.md`

## Example
```bash
/create-command analyze-deps "Analyze dependencies for outdated packages"
# Output: STATUS=WROTE PATH=.claude/commands/analyze-deps.md
```