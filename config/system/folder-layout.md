---
title: "Folder Layout"
description: "Single source of truth for the repository structure."
author: "{{OWNER_NAME}}"
date: {{DATE}}
lastmod: {{DATE}}
version: "0.1.0"
keywords:
  - folder-structure
  - repository-layout
schema:
  type: "TechArticle"
ai-content-policy: "extract-with-attribution"
ai-freshness: "monthly"

intent:
  purpose: "Document the repository structure as single source of truth"
  audience: "developers, AI agents"

related-files:
  - ../../MX.yaml
  - ../../README.md

update-instructions:
  source: "Actual repository structure"
  method: |
    1. Update when directories are added or removed
    2. Keep in sync with actual folder structure
    3. Verify with `find . -type d` command
---

# Folder Layout

Single source of truth for the repository structure.

```
{{PROJECT_NAME}}/
├── .claude/                    # Claude Code AI assistant configuration
│   ├── MX.yaml                 # Folder metadata
│   ├── commands/               # Custom CLI commands
│   ├── hooks/                  # Pre/post commit hooks
│   └── skills/                 # Reusable workflows
│
├── .github/                    # GitHub configuration
│   ├── MX.yaml                 # Folder metadata
│   └── workflows/              # GitHub Actions CI/CD
│
├── .vscode/                    # VS Code settings (in .mxignore)
│
├── mx-config/                     # Configuration files
│   ├── MX.yaml                 # Folder metadata
│   └── system/                 # System documentation
│       ├── MX.yaml             # Folder metadata
│       └── folder-layout.md    # This file
│
├── docs/                       # Documentation
│   ├── MX.yaml                 # Folder metadata
│   ├── architecture/           # Architecture Decision Records
│   │   └── MX.yaml
│   ├── for-ai/                 # AI-optimised documentation
│   │   └── MX.yaml
│   └── specifications/         # PRDs and specs
│       └── MX.yaml
│
├── packages/                   # Implementation packages
│   └── MX.yaml                 # Folder metadata
│
├── scripts/                    # Build and automation scripts
│   └── MX.yaml                 # Folder metadata
│
├── src/                        # Source code
│   └── MX.yaml                 # Folder metadata
│
├── .gitignore                  # Git exclusions
├── .mxignore                   # Intent metadata exclusions
├── master-mx.yaml              # Repository master (ENFORCED)
├── MX.yaml                     # Repository defaults
├── CLAUDE.md                   # AI agent guidance
├── LEARNINGS.md                # Project learnings
├── llms.txt                    # LLM index (INFORMATIVE ONLY)
├── ONBOARDING.md               # New contributor guide
├── package.json                # npm configuration
└── README.md                   # Project overview
```

## Directory Purposes

### `.claude/`

Claude Code AI assistant configuration. Contains commands, hooks, and skills.

### `mx-config/`

Shared configuration files. System documentation in `system/` subdirectory.

### `docs/`

All project documentation:

- `architecture/` - Architecture Decision Records
- `for-ai/` - Documentation optimised for AI agents
- `specifications/` - PRDs and technical specs

### `packages/`

Implementation packages for monorepo structure.

### `scripts/`

Build, deployment, and automation scripts.

### `src/`

Source code for the project.
