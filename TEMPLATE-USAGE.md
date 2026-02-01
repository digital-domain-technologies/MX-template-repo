---
title: "Template Usage Guide"
description: "How to use this MX Template Repository to create a new Intent Repository-compliant project."
author: "Tom Cranstoun"
date: 2026-01-30
lastmod: 2026-01-30
version: "1.0.0"
keywords:
  - template
  - intent-repository
  - mx
  - setup
schema:
  type: "HowTo"
ai-content-policy: "extract-with-attribution"
ai-freshness: "monthly"

intent:
  purpose: "Guide users through setting up a new project from this template"
  audience: "developers, AI agents setting up new projects"

update-instructions:
  method: |
    1. Update when template structure changes
    2. Keep placeholder list current
    3. Test instructions periodically
---

# Template Usage Guide

This repository is an **MX Template** - a starting point for creating Intent Repository-compliant projects.

## Quick Start

### 1. Clone or Use as Template

```bash
# Option A: Clone directly
git clone https://github.com/digital-domain-technologies/MX-template-repo.git my-project
cd my-project
rm -rf .git
git init

# Option B: Use GitHub's "Use this template" button
# Then clone your new repository
```

### 2. Replace Placeholders

Search and replace these placeholders throughout the repository:

| Placeholder | Replace With | Example |
|-------------|--------------|---------|
| `{{PROJECT_NAME}}` | Your project name | `my-awesome-project` |
| `{{PROJECT_DESCRIPTION}}` | Brief description | `A tool for processing data` |
| `{{PROJECT_TEAM}}` | Team name | `platform-team` |
| `{{OWNER_NAME}}` | Maintainer name | `Jane Developer` |
| `{{OWNER_EMAIL}}` | Contact email | `jane@example.com` |
| `{{PROJECT_URL}}` | Repository URL | `https://github.com/org/repo` |
| `{{DATE}}` | Current date | `2026-01-30` |
| `{{KEYWORD_1}}` | Relevant keyword | `data-processing` |
| `{{KEYWORD_2}}` | Relevant keyword | `automation` |
| `{{LICENSE_INFO}}` | License details | `MIT License` |

**Quick replace command:**

```bash
# macOS/Linux
find . -type f \( -name "*.md" -o -name "*.yaml" -o -name "*.json" -o -name "*.txt" \) \
  -exec sed -i '' 's/{{PROJECT_NAME}}/my-project/g' {} +
```

### 3. Customise Policies

Edit `master-mx.yaml` to set your project's enforced policies:

```yaml
enforced:
  style:
    language: "en-GB"  # or "en-US"
  security:
    secrets-detection: true
```

Edit `MX.yaml` to set your project's defaults:

```yaml
project:
  name: "Your Project Name"
  description: "Your project description"
```

### 4. Remove Template Files

```bash
# Remove this usage guide
rm TEMPLATE-USAGE.md

# Remove template instruction blocks from master-mx.yaml and MX.yaml
# (Look for "TEMPLATE INSTRUCTIONS" sections)
```

### 5. Initialise Git

```bash
git add .
git commit -m "Initial commit from MX template"
git remote add origin <your-repo-url>
git push -u origin main
```

## What's Included

### Repository Structure

```
MX-template-repo/
├── .claude/                    # AI assistant configuration
├── .github/                    # GitHub workflows
├── .vscode/                    # VS Code settings
├── mx-config/system/              # System documentation
├── docs/                       # Documentation structure
│   ├── architecture/           # ADRs
│   ├── for-ai/                 # AI-optimised docs
│   └── specifications/         # PRDs and specs
├── packages/                   # Monorepo packages
├── scripts/                    # Build scripts
├── src/                        # Source code
├── master-mx.yaml              # Enforced policies
├── MX.yaml                     # Repository defaults
├── CLAUDE.md                   # AI guidance
├── llms.txt                    # AI navigation index
└── [documentation files]
```

### Key Files

| File | Purpose |
|------|---------|
| `master-mx.yaml` | Enforced policies - edit to set your rules |
| `MX.yaml` | Repository defaults - edit to set your defaults |
| `CLAUDE.md` | AI agent guidance - comprehensive instructions |
| `llms.txt` | Navigation index for AI (informative only) |
| `.mxignore` | Files excluded from intent processing |

### Folder MX.yaml Files

Every folder has an `MX.yaml` file defining its purpose and rules:

- `.claude/MX.yaml`
- `.github/MX.yaml`
- `mx-config/MX.yaml`
- `mx-config/system/MX.yaml`
- `docs/MX.yaml`
- `docs/architecture/MX.yaml`
- `docs/for-ai/MX.yaml`
- `docs/specifications/MX.yaml`
- `packages/MX.yaml`
- `scripts/MX.yaml`
- `src/MX.yaml`

## For AI Agents

If you are an AI agent setting up a new project from this template:

1. **Clone the template** to the target location
2. **Ask the user** for values to replace placeholders
3. **Perform search/replace** for all placeholders
4. **Remove `TEMPLATE-USAGE.md`** after setup
5. **Remove template instruction blocks** from `master-mx.yaml` and `MX.yaml`
6. **Verify** all placeholders are replaced: `grep -r "{{" .`
7. **Initialise git** and create initial commit

## Intent Repository Pattern

This template implements the Intent Repository pattern where:

- Every file carries or inherits metadata for its own maintenance
- `master-mx.yaml` defines enforced policies
- `MX.yaml` files define inheritable defaults
- Markdown files use YAML frontmatter
- JSON files use `$intent` keys
- `llms.txt` is informative only (not authoritative)

For full documentation:
https://github.com/digital-domain-technologies/intent-cms

## Support

- **Pattern documentation:** https://github.com/digital-domain-technologies/intent-cms
- **Template issues:** https://github.com/digital-domain-technologies/MX-template-repo/issues
