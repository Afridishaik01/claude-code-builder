# Claude Code Toolkit

> Create skills, subagents, hooks, commands, and plugins for Claude Code

A comprehensive toolkit plugin that helps you create and manage Claude Code customizations with best practices built-in.

## What's Inside

This plugin provides slash commands to create:

- **Skills** - Model-invoked capabilities that Claude discovers automatically (`/create-skill`)
- **Subagents** - Delegated AI agents with specialized roles (`/create-subagent`)
- **Commands** - User-invoked slash commands for workflows (`/create-command`)
- **Hooks** - Event-triggered automations (`/create-hook`)
- **Plugins** - Distributable Claude Code packages (`/create-plugin`)

## Available Commands

### `/create-skill`
Create a new Claude Code skill with proper structure and best practices.

Skills are automatically invoked by Claude based on context. Perfect for extending Claude's capabilities with domain knowledge, processes, or specialized workflows.

**Usage:** `/create-skill`

### `/create-subagent`
Create a new subagent with specialized expertise and tool permissions.

Subagents handle delegated tasks in separate threads. Ideal for code review, debugging, security analysis, and other focused roles.

**Usage:** `/create-subagent`

### `/create-command`
Create a new slash command for explicit user invocation.

Commands are manually triggered prompts for frequently-used workflows. Great for shortcuts, templates, and deliberate actions.

**Usage:** `/create-command`

### `/create-hook`
Analyze your project and create hooks for automation.

Hooks trigger on events like file edits or tool usage. Useful for linting, formatting, type-checking, and security scanning.

**Usage:** `/create-hook`

### `/create-plugin`
Convert a `.claude/` directory into a distributable plugin.

Package your customizations for sharing across projects or with your team.

**Usage:** `/create-plugin`

## Installation

### Via Plugin Marketplace

```bash
# Add marketplace containing this plugin
/plugin marketplace add <marketplace-url>

# Install the plugin
/plugin install claude-code-toolkit@<marketplace-name>
```

### Local Installation

```bash
# Clone or download this repository
cd ~/your-plugins
git clone <repository-url>

# Create a local marketplace
mkdir my-marketplace
mkdir my-marketplace/.claude-plugin

# Create marketplace manifest
cat > my-marketplace/.claude-plugin/marketplace.json << 'EOF'
{
  "name": "my-marketplace",
  "owner": {"name": "Your Name"},
  "plugins": [{
    "name": "claude-code-toolkit",
    "source": "./claude-code-toolkit",
    "description": "Create skills, subagents, hooks, commands, and plugins"
  }]
}
EOF

# Move plugin into marketplace
mv claude-code-toolkit my-marketplace/

# Add marketplace and install
/plugin marketplace add ./my-marketplace
/plugin install claude-code-toolkit@my-marketplace
```

## Usage

After installation, simply invoke any of the creation commands:

```bash
# Create a new skill
/create-skill

# Create a new subagent
/create-subagent

# Create a new command
/create-command

# Create a hook
/create-hook

# Convert .claude directory to plugin
/create-plugin
```

Each command will guide you through the creation process with questions about:
- Name and purpose
- Scope (project vs personal)
- Tool permissions
- Configuration options

All commands follow Claude Code best practices and include comprehensive testing instructions.

## Quick Decision Guide

**Not sure what to create?**

- **Skill**: Want Claude to automatically discover and use a capability based on context
- **Subagent**: Need a specialized AI agent for a focused role (code review, debugging, etc.)
- **Command**: Want a shortcut for a frequently-used prompt you explicitly invoke
- **Hook**: Want automation that triggers on events (file edits, tool usage, etc.)
- **Plugin**: Want to package and share your customizations

## Structure

```
claude-code-toolkit/
├── .claude-plugin/
│   └── plugin.json           # Plugin manifest
├── commands/                 # Creation commands
│   ├── create-skill.md       # Skill creation guide
│   ├── create-subagent.md    # Subagent creation guide
│   ├── create-command.md     # Command creation guide
│   ├── create-hook.md        # Hook creation guide
│   └── create-plugin.md      # Plugin creation guide
└── README.md
```

## Features

- **Best practices built-in**: Each command follows official Claude Code documentation
- **Interactive guidance**: Commands ask questions to gather all needed information
- **Comprehensive testing**: Every creation includes detailed testing instructions
- **Scope flexibility**: Create project-level (shared) or personal customizations
- **Tool safety**: Proper tool restrictions and permission management
- **Documentation**: Clear explanations of when and why to use each feature

## Requirements

- Claude Code CLI installed
- Basic familiarity with Markdown and YAML

## Contributing

Contributions welcome! If you find issues or have suggestions:

1. Check existing issues
2. Create a detailed bug report or feature request
3. Submit pull requests with clear descriptions

## License

[Add your license here]

## Version History

- **2.0.0** - Complete toolkit transformation with all creation commands
- **1.0.0** - Initial plugin creator version

## Author

**Alexander Opalic**

A comprehensive toolkit for Claude Code customization.
