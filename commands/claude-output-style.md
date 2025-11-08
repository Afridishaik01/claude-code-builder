---
description: help to generate output stlyes use this as a reference # Output styles > Adapt Claude Code for uses beyond software engineering Output styles allow you to use Claude Code as any type of agent while keeping its core capabilities, such as running local scripts, reading/writing files, and tracking TODOs. ## Built-in output styles Claude Code's **Default** output style is the existing system prompt, designed to help you complete software engineering tasks efficiently. There are two additional built-in output styles focused on teaching you the codebase and how Claude operates: * **Explanatory**: Provides educational "Insights" in between helping you complete software engineering tasks. Helps you understand implementation choices and codebase patterns. * **Learning**: Collaborative, learn-by-doing mode where Claude will not only share "Insights" while coding, but also ask you to contribute small, strategic pieces of code yourself. Claude Code will add `TODO(human)` markers in your code for you to implement. ## How output styles work Output styles directly modify Claude Code's system prompt. * Non-default output styles exclude instructions specific to code generation and efficient output normally built into Claude Code (such as responding concisely and verifying code with tests). * Instead, these output styles have their own custom instructions added to the system prompt. ## Change your output style You can either: * Run `/output-style` to access the menu and select your output style (this can also be accessed from the `/config` menu) * Run `/output-style [style]`, such as `/output-style explanatory`, to directly switch to a style These changes apply to the [local project level](/en/settings) and are saved in `.claude/settings.local.json`. ## Create a custom output style To set up a new output style with Claude's help, run `/output-style:new I want an output style that ...` By default, output styles created through `/output-style:new` are saved as markdown files at the user level in `~/.claude/output-styles` and can be used across projects. They have the following structure: ```markdown  theme={null} --- name: My Custom Style description: A brief description of what this style does, to be displayed to the user --- # Custom Style Instructions You are an interactive CLI tool that helps users with software engineering tasks. [Your custom instructions here...] ## Specific Behaviors [Define how the assistant should behave in this style...] ``` You can also create your own output style Markdown files and save them either at the user level (`~/.claude/output-styles`) or the project level (`.claude/output-styles`). ## Comparisons to related features ### Output Styles vs. CLAUDE.md vs. --append-system-prompt Output styles completely "turn off" the parts of Claude Code's default system prompt specific to software engineering. Neither CLAUDE.md nor `--append-system-prompt` edit Claude Code's default system prompt. CLAUDE.md adds the contents as a user message *following* Claude Code's default system prompt. `--append-system-prompt` appends the content to the system prompt. ### Output Styles vs. [Agents](/en/sub-agents) Output styles directly affect the main agent loop and only affect the system prompt. Agents are invoked to handle specific tasks and can include additional settings like the model to use, the tools they have available, and some context about when to use the agent. ### Output Styles vs. [Custom Slash Commands](/en/slash-commands) You can think of output styles as "stored system prompts" and custom slash commands as "stored prompts".
argument-hint: [style-name] [--user|--project] [--description "..."]
---

# /claude-output-style

## Purpose
Generate custom output style files for Claude Code with proper structure and YAML frontmatter.

## Contract

**Inputs:**
- `$1` — STYLE_NAME (optional: name for the output style)
- `--user` — Save to user-level directory (~/.claude/output-styles)
- `--project` — Save to project-level directory (.claude/output-styles)
- `--description "..."` — Brief description of the output style

**Outputs:** `STATUS=<OK|FAIL> PATH=<path> SCOPE=<user|project>`

## Instructions

1. **Determine scope:**
   - If `--user` is provided: save to `~/.claude/output-styles/`
   - If `--project` is provided: save to `.claude/output-styles/`
   - Default: `--user` (user-level)

2. **Gather information:**
   - If STYLE_NAME not provided, ask user for the style name
   - If description not provided via `--description`, ask user what behavior they want
   - Style name should be title-cased (e.g., "My Custom Style")

3. **Generate output style file** using this template:

```markdown
---
name: {{STYLE_NAME}}
description: {{DESCRIPTION}}
---

# {{STYLE_NAME}} Instructions

You are an interactive CLI tool that helps users with software engineering tasks.

{{CUSTOM_INSTRUCTIONS}}

## Specific Behaviors

{{SPECIFIC_BEHAVIORS}}

## Key Principles

- {{PRINCIPLE_1}}
- {{PRINCIPLE_2}}
- {{PRINCIPLE_3}}
```

4. **Create the file:**
   - Convert style name to kebab-case for filename (e.g., "My Custom Style" → "my-custom-style.md")
   - Create target directory if it doesn't exist
   - Write the file
   - Print: `STATUS=OK PATH=<full-path> SCOPE=<user|project>`

5. **Inform user:**
   - Let them know the file was created
   - Remind them they can activate it with `/output-style [style-name]`
   - Mention they can edit the file directly to refine the instructions

## Examples

**Example 1: Basic usage**
```bash
/claude-output-style
# Claude will ask for style name and description interactively
```

**Example 2: Full specification**
```bash
/claude-output-style "Teaching Assistant" --project --description "Explains concepts step by step with examples"
# STATUS=OK PATH=.claude/output-styles/teaching-assistant.md SCOPE=project
```

**Example 3: User-level style**
```bash
/claude-output-style "Code Reviewer" --user --description "Focuses on thorough code review with best practices"
# STATUS=OK PATH=~/.claude/output-styles/code-reviewer.md SCOPE=user
```

## Notes

- Output styles modify Claude Code's system prompt completely
- Non-default styles exclude standard code generation instructions
- User-level styles are available across all projects
- Project-level styles are specific to the current project
- You can manually edit the generated files to refine instructions
