---
description: Publish Claude Code plugin to marketplace
argument-hint: [marketplace-name]
---

# /publish-claude-plugin

## Purpose
Publish the current Claude Code plugin to a marketplace by reading plugin metadata from .claude-plugin/plugin.json and automating the publication process.

## Contract
**Inputs:** `[marketplace-name]` — Optional marketplace name to publish to
**Outputs:** `STATUS=<OK|FAIL> [key=value ...]`

## Instructions
1. **Validate plugin structure:**
   - Check if `.claude-plugin/plugin.json` exists
   - If not found: Print `STATUS=FAIL ERROR="No plugin.json found at .claude-plugin/plugin.json"` and exit
   - Parse plugin.json and extract `name` and `version` fields

2. **Extract plugin metadata:**
   - Read plugin name from `plugin.json`
   - Read version from `plugin.json`
   - Validate both fields are present and non-empty

3. **Prepare for publication:**
   - Verify all required plugin files are present
   - Check git status (should be clean or committed)
   - If marketplace-name provided, use it; otherwise ask user to select/provide marketplace

4. **Execute publication:**
   - Tag the git repository with version from plugin.json
   - Push to remote repository
   - Update marketplace manifest if local marketplace
   - Print: `STATUS=OK PLUGIN={{name}} VERSION={{version}} MARKETPLACE={{marketplace}}`

## Constraints
- Idempotent and deterministic
- Must have valid .claude-plugin/plugin.json
- Git repository should be in clean state
- Minimal console output (STATUS line only)

## Example
```bash
/publish-claude-plugin my-marketplace
# Output: STATUS=OK PLUGIN=claude-code-builder VERSION=1.0.0 MARKETPLACE=my-marketplace
```
