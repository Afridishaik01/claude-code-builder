---
description: Convert a project into a Claude Code plugin
argument-hint: [project-path]
---

# /create-plugin

## Purpose
Guide users through converting an existing project into a properly structured Claude Code plugin, following official documentation standards.

## Contract
**Inputs:** `[project-path]` — Optional path to project directory (defaults to current directory)
**Outputs:** `STATUS=<OK|FAIL> PLUGIN_PATH=<path>`

## Instructions

1. **Analyze the project structure:**
   - Identify existing components that could become plugin features
   - Check for slash commands, agents, skills, hooks, or MCP integrations
   - Review documentation files

2. **Create plugin structure:**
   - Create `.claude-plugin/` directory at project root
   - Generate `plugin.json` manifest with proper metadata:
     - name (lowercase, kebab-case)
     - description
     - version (semantic versioning)
     - author information

3. **Organize plugin components:**
   - `commands/` - Slash command markdown files
   - `agents/` - Agent definition markdown files
   - `skills/` - Agent Skills with SKILL.md files
   - `hooks/` - hooks.json for event handlers
   - `.mcp.json` - MCP server configurations (if applicable)

4. **Create marketplace structure for testing:**
   - Set up parent marketplace directory
   - Generate `.claude-plugin/marketplace.json`
   - Configure plugin source reference

5. **Generate documentation:**
   - Create/update README.md with:
     - Installation instructions
     - Usage examples
     - Component descriptions
     - Testing guidance

6. **Provide testing workflow:**
   - Local marketplace setup commands
   - Installation verification steps
   - Iteration and debugging guidance

## Reference Documentation

Follow the official Claude Code plugin structure:

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata
├── commands/                 # Custom slash commands (optional)
│   └── command-name.md
├── agents/                   # Custom agents (optional)
│   └── agent-name.md
├── skills/                   # Agent Skills (optional)
│   └── skill-name/
│       └── SKILL.md
├── hooks/                    # Event handlers (optional)
│   └── hooks.json
├── .mcp.json                # MCP servers (optional)
└── README.md                # Documentation
```

## Key Guidelines

- **Plugin manifest**: Use semantic versioning, clear descriptions
- **Commands**: Markdown files with frontmatter (description, argument-hint)
- **Skills**: Create subdirectories with SKILL.md files
- **Testing**: Use local marketplace for iterative development
- **Documentation**: Include installation, usage, and examples

## Constraints
- Must create valid plugin.json schema
- Follow kebab-case naming conventions
- Include proper frontmatter in all markdown files
- Maintain separation between plugin and marketplace manifests
- Output final STATUS line with plugin path

## Example Output
```
Created plugin structure at: ./my-plugin
Generated components:
  - .claude-plugin/plugin.json
  - commands/helper.md
  - README.md

Test marketplace created at: ./dev-marketplace

Next steps:
1. cd .. && claude
2. /plugin marketplace add ./dev-marketplace
3. /plugin install my-plugin@dev-marketplace

STATUS=OK PLUGIN_PATH=./my-plugin
```
