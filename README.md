# Skill Claude Plugin

A Claude Code plugin that provides the `creating-claude-plugins` skill - a comprehensive guide for creating Claude plugins with correct directory structure, mandatory testing workflows, and prevention of common mistakes.

## What This Plugin Provides

### Skills

- **creating-claude-plugins**: Use when creating a Claude Code plugin, before writing any files. This skill:
  - Ensures correct directory structure (commands at root, not in .claude-plugin)
  - Enforces proper markdown format for components
  - Provides mandatory local testing workflow
  - Prevents wrong file placement and validation skipping

## Installation

### Option 1: Install from Local Marketplace (for testing)

1. Create a test marketplace structure:
```bash
# From parent directory of this repo
mkdir test-marketplace
mkdir test-marketplace/.claude-plugin

# Create marketplace manifest
cat > test-marketplace/.claude-plugin/marketplace.json << 'EOF'
{
  "name": "test-marketplace",
  "owner": {"name": "Test User"},
  "plugins": [{
    "name": "skill-claude-plugin",
    "source": "./skill-claude-plugin",
    "description": "Skill for creating Claude Code plugins"
  }]
}
EOF

# Move/copy this plugin into marketplace
mv skill-claude-plugin test-marketplace/
```

2. Install the plugin:
```bash
# Add the marketplace
/plugin marketplace add ./test-marketplace

# Install the plugin
/plugin install skill-claude-plugin@test-marketplace

# Restart Claude Code
```

### Option 2: Install from Git Repository (when published)

```bash
# This will be available once the plugin is published to a git repository
/plugin install skill-claude-plugin@<marketplace-name>
```

## Usage

Once installed, the `creating-claude-plugins` skill will be available automatically. Claude Code will use this skill when you ask it to create a plugin.

Example:
```
You: Create a new Claude plugin for my project
Claude: I'm using the creating-claude-plugins skill to help you create a plugin...
```

## Plugin Structure

This plugin follows the correct Claude Code plugin structure:

```
skill-claude-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/                   # Skills at root level (correct!)
│   └── creating-claude-plugins/
│       └── SKILL.md
└── README.md
```

## What the Skill Teaches

The `creating-claude-plugins` skill provides:

- **Correct plugin structure** - Commands, agents, skills, and hooks at root level (NOT inside .claude-plugin/)
- **Mandatory workflow** - Check alternatives → Create structure → Add components → Test locally → Verify
- **Local testing guide** - How to test plugins before distribution using marketplace structure
- **Common mistakes** - What NOT to do (wrong file locations, skipping testing, etc.)
- **Verification checklist** - Ensures plugins work before claiming "ready"

## Development

The `.claude/` directory is for local development and testing. It allows you to test the skill locally before installing it as a plugin.

## License

[Add your license here]

## Author

Alexander Opalic
