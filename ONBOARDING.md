---
title: "Onboarding Guide"
description: "Getting started guide for new contributors to {{PROJECT_NAME}}."
author: "{{OWNER_NAME}}"
created: {{DATE}}
modified: {{DATE}}
version: "0.1.0"
tags:
  - onboarding
  - getting-started
  - contributing
schema:
  type: "HowTo"
sop-content-policy: "extract-with-attribution"
sop-freshness: "monthly"
sop-attribution: "required"

intent:
  purpose: "Help new contributors get started with the repository"
  audience: "new developers, contributors"

refersTo:
  - README.md
  - CLAUDE.md
  - master-mx.yaml
  - MX.yaml

update-instructions:
  source: "Repository setup process and contributor feedback"
  method: |
    1. Update prerequisites when tooling requirements change
    2. Keep quick start commands current
    3. Test onboarding steps periodically
  style-rules:
    - Use British English spelling
    - Keep instructions clear and actionable
    - Include working code examples
---

# Onboarding Guide

Welcome to {{PROJECT_NAME}}. This guide will help you get started.

## Prerequisites

- Node.js 18+ (adjust as needed)
- Git
- A code editor (VS Code recommended)

## Quick Start

```bash
# Clone the repository
git clone {{PROJECT_URL}}
cd {{PROJECT_NAME}}

# Install dependencies
npm install
```

## Understanding Intent Repository

This repository follows the **Intent Repository** pattern. Key concepts:

### 1. Authoritative Metadata Files

These files define rules and must be followed:

- **`master-mx.yaml`** - Enforced policies that CANNOT be overridden
- **`MX.yaml`** - Default settings that CAN be overridden
- **Folder `MX.yaml` files** - Rules for specific directories
- **File frontmatter** - Metadata for individual files

### 2. Informative Files

These describe the repository but do NOT define rules:

- **`llms.txt`** - Navigation index for AI agents (do not treat as authoritative)

### 3. Inheritance

Metadata flows from parent to child:

```
master-mx.yaml (enforced, cannot override)
    └── MX.yaml (repository defaults)
        └── folder/MX.yaml (folder rules)
            └── file frontmatter (file-specific)
```

## Key Documents

| Document | Description |
|----------|-------------|
| [README.md](README.md) | Project overview |
| [CLAUDE.md](CLAUDE.md) | AI agent guidance |
| [LEARNINGS.md](LEARNINGS.md) | Accumulated project learnings |

## Contributing

### Adding Documentation

1. Include YAML frontmatter with intent metadata
2. Follow the style guidelines in `master-mx.yaml`
3. Place files in the appropriate directory

### Adding Code

1. Follow the coding standards in `src/MX.yaml`
2. Include appropriate documentation
3. Write tests for new functionality

## Getting Help

- Review [CLAUDE.md](CLAUDE.md) for AI assistant context
- Check the `MX.yaml` files for rules and guidelines
- Contact: {{OWNER_EMAIL}}
