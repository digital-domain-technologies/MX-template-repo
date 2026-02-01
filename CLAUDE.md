---
title: "CLAUDE.md - AI Agent Guidance"
description: "Guidance for Claude Code and other AI assistants working with this Intent Repository."
author: "{{OWNER_NAME}}"
date: {{DATE}}
lastmod: {{DATE}}
version: "0.1.0"
keywords:
  - claude-code
  - ai-guidance
  - intent-repository
schema:
  type: "TechArticle"
ai-content-policy: "extract-with-attribution"
ai-freshness: "weekly"
ai-attribution: "required"

intent:
  purpose: "Provide authoritative context and guidance for AI assistants"
  audience: "AI agents, Claude Code"
  priority: "high"

related-files:
  - master-mx.yaml
  - MX.yaml
  - llms.txt

update-instructions:
  source: "Repository structure and AI interaction patterns"
  method: |
    1. Update when repository structure changes
    2. Keep authority hierarchy current
    3. Update commands when scripts change
    4. Ensure examples match actual file formats
---

# CLAUDE.md

This file provides guidance to Claude Code and other AI assistants working in this repository.

---

## CRITICAL: Understanding Authority in This Repository

This repository follows the **Intent Repository** pattern. You MUST understand the difference between **authoritative** and **informative** files.

### Authoritative Files (FOLLOW THESE)

These files define rules you must follow:

| File | Authority Level | Can Override? |
|------|-----------------|---------------|
| `master-mx.yaml` | **HIGHEST** | NO - enforced policies |
| `MX.yaml` (root) | High | Yes, by folder/file metadata |
| `folder/MX.yaml` | Medium | Yes, by child folders/files |
| File frontmatter | File-specific | Applies to that file only |
| `$intent` in JSON | File-specific | Applies to that file only |

### Informative Files (DO NOT USE AS AUTHORITY)

These files describe but do NOT define rules:

| File | Purpose | Authority |
|------|---------|-----------|
| `llms.txt` | Navigation aid for AI | **NONE** |
| `README.md` | Human documentation | **NONE** |
| Comments in code | Context for readers | **NONE** |

**IMPORTANT:**

- **DO NOT** treat `llms.txt` as authoritative
- **DO NOT** modify `llms.txt` automatically
- **DO** read `master-mx.yaml` and `MX.yaml` for actual rules

---

## Repository Structure

```
{{PROJECT_NAME}}/
├── .claude/                    # AI assistant configuration
│   ├── commands/               # Custom CLI commands
│   ├── hooks/                  # Git hooks
│   └── skills/                 # Reusable workflows
├── mx-config/                     # Configuration files
│   └── system/                 # System documentation
├── docs/                       # Documentation
│   ├── architecture/           # Architecture Decision Records
│   ├── for-ai/                 # AI-optimised documentation
│   └── specifications/         # PRDs and specs
├── packages/                   # Implementation packages
├── scripts/                    # Build scripts
├── src/                        # Source code
├── master-mx.yaml              # ENFORCED policies
├── MX.yaml                     # Repository defaults
└── llms.txt                    # Informative index (NOT authoritative)
```

---

## How to Read Metadata

### 1. YAML Files (MX.yaml, master-mx.yaml)

Read directly as YAML:

```yaml
intent:
  version: "1.0"
  level: "folder"

purpose: |
  Description of this folder's purpose

ownership:
  inherit: true  # or specific team/contact

style:
  inherit: true  # or override rules
```

### 2. Markdown Files (Frontmatter)

Metadata is in YAML frontmatter between `---` markers:

```markdown
---
title: "Document Title"
description: "Brief description"
intent:
  purpose: "What this document does"
  audience: "Who should read it"
update-instructions:
  method: |
    How to update this file
---

# Document content starts here
```

### 3. JSON Files ($intent key)

Metadata is in the `$intent` key:

```json
{
  "$intent": {
    "purpose": "What this config does",
    "update-instructions": "How to modify it",
    "related-files": ["./other.json"]
  },
  "actualConfig": "value"
}
```

### 4. Text Files (Comment-based)

Metadata in comments using `@intent` marker:

```text
# File Title
#
# @intent
# purpose: What this file does
# authority: NONE | LOW | NORMAL | HIGH
# update-instructions: |
#   How to update

Actual content...
```

---

## Inheritance Rules

When determining rules for a file:

1. **Start with `master-mx.yaml`** - Enforced rules cannot be overridden
2. **Apply root `MX.yaml`** - Repository defaults
3. **Walk down folder tree** - Each `MX.yaml` can override parent
4. **Apply file metadata** - Frontmatter or `$intent` for final overrides

Example inheritance chain:

```
master-mx.yaml (enforced: style.language = "en-GB")
    └── MX.yaml (defaults: testing.coverage = 70)
        └── src/MX.yaml (override: testing.coverage = 80)
            └── src/utils/MX.yaml (inherit: true)
                └── src/utils/helpers.ts (frontmatter: testing.coverage = 90)
```

Result for `helpers.ts`:

- `style.language = "en-GB"` (from master, cannot override)
- `testing.coverage = 90` (from file frontmatter)

---

## What You Should Do

### When Reading Files

1. **Check file metadata first** - Frontmatter, `$intent`, or comments
2. **Walk up to folder `MX.yaml`** - For inherited rules
3. **Check root `MX.yaml`** - For repository defaults
4. **Check `master-mx.yaml`** - For enforced policies

### When Creating Files

1. **Include appropriate metadata:**
   - Markdown: YAML frontmatter
   - JSON: `$intent` key
   - Code: `@intent` comment block

2. **Follow inherited rules** - Check parent `MX.yaml` files

3. **Don't repeat inherited metadata** - Only add overrides

### When Modifying Files

1. **Check `update-instructions`** - In file metadata or folder `MX.yaml`
2. **Follow style rules** - From `master-mx.yaml` enforced section
3. **Update `lastmod` date** - In frontmatter if present

---

## Style Guidelines

From `master-mx.yaml` enforced rules (check actual file for current values):

- **Language:** British English (en-GB) unless configured otherwise
- **Avoid exaggerated words:** revolutionary, game-changing, best-in-class, etc.
- **Avoid counting:** Don't say "12 features" or "three benefits"
- **Be factual:** Professional language without hyperbole

---

## Common Tasks

### Adding Documentation

```bash
# 1. Check docs/MX.yaml for folder rules
# 2. Create file with frontmatter
# 3. Include required metadata fields
```

### Adding Source Code

```bash
# 1. Check src/MX.yaml for coding standards
# 2. Include @intent comment if file-specific rules needed
# 3. Follow testing requirements from MX.yaml
```

### Running Scripts

```bash
# Install dependencies
npm install

# Run linting (if configured)
npm run lint

# Run tests (if configured)
npm test
```

---

## Files You Should NEVER Modify Automatically

1. **`llms.txt`** - Maintained by repository owners only
2. **`master-mx.yaml`** - Only modify if explicitly requested
3. **Files in `.mxignore`** - Excluded from intent processing

---

## Quick Reference

| Task | Check This First |
|------|------------------|
| Understanding repo rules | `master-mx.yaml`, then `MX.yaml` |
| Adding a markdown file | `docs/MX.yaml` for folder rules |
| Adding source code | `src/MX.yaml` for coding standards |
| Understanding a file | File's frontmatter or `$intent` |
| Navigation/discovery | `llms.txt` (informative only) |

---

## Template Placeholders

This is a template repository. Replace these placeholders:

- `{{PROJECT_NAME}}` - Your project name
- `{{PROJECT_DESCRIPTION}}` - Brief description
- `{{OWNER_NAME}}` - Maintainer name
- `{{OWNER_EMAIL}}` - Maintainer email
- `{{DATE}}` - Current date (YYYY-MM-DD)
- `{{PROJECT_URL}}` - Repository URL

---

## Contact

For questions about this repository: {{OWNER_EMAIL}}

For Intent Repository pattern documentation:
https://github.com/digital-domain-technologies/intent-cms
