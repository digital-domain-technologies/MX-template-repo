---
title: "Learnings"
description: "Battle-tested rules from actual mistakes and discoveries in {{PROJECT_NAME}}."
author: "{{OWNER_NAME}}"
created: {{DATE}}
modified: {{DATE}}
version: "0.1.0"
tags:
  - learnings
  - best-practices
  - mistakes
schema:
  type: "HowTo"
sop-content-policy: "extract-with-attribution"
sop-freshness: "weekly"
sop-attribution: "required"

intent:
  purpose: "Capture institutional knowledge and prevent repeated mistakes"
  audience: "all contributors"

refersTo:
  - CLAUDE.md
  - master-mx.yaml

update-instructions:
  source: "Team experiences and discovered issues"
  method: |
    1. Add new learnings as they are discovered
    2. Date entries when timing context is useful
    3. Group related learnings under appropriate sections
    4. Include both DO and DON'T guidance
  style-rules:
    - Use British English spelling
    - Keep entries concise and actionable
    - Include context for why the learning matters
---

# Learnings

Battle-tested rules from actual mistakes and discoveries. Add entries as you learn.

---

## Intent Repository

### DO: Check `master-mx.yaml` before making changes

The master file contains enforced policies. Understand what cannot be overridden before you start.

### DO: Use inheritance to reduce repetition

Define rules once at the appropriate level. Only add file-level metadata for exceptions.

### DON'T: Treat `llms.txt` as authoritative

It's informative only. Use `MX.yaml` files for actual rules.

---

## Documentation

### DO: Include YAML frontmatter in all markdown files

Every markdown file should carry its own update instructions and metadata.

### DON'T: Count items in documentation

Avoid "12 features" or "three benefits". Numbers become outdated when content changes.

---

## Git Workflow

### DO: Check `pwd` before git operations

In multi-package repositories, always verify your current directory.

### DO: Write meaningful commit messages

Explain why, not just what. The commit message is part of the repository's self-documentation.

---

*Add new learnings as you discover them. Date entries if useful for context.*
