---
title: "{{PROJECT_NAME}}"
description: "{{PROJECT_DESCRIPTION}}"
author: "{{OWNER_NAME}}"
date: {{DATE}}
lastmod: {{DATE}}
version: "0.1.0"
status: "development"
keywords:
  - {{KEYWORD_1}}
  - {{KEYWORD_2}}
canonical: "{{PROJECT_URL}}"
schema:
  type: "SoftwareSourceCode"
ai-content-policy: "extract-with-attribution"
ai-freshness: "monthly"
ai-attribution: "required"

intent:
  purpose: "Primary entry point and overview for the {{PROJECT_NAME}} repository"
  audience: "developers, contributors, AI agents"

related-files:
  - ONBOARDING.md
  - CLAUDE.md
  - LEARNINGS.md

update-instructions:
  source: "Repository structure and project documentation"
  method: |
    1. Update when repository structure changes
    2. Keep documentation links current
    3. Ensure quick start instructions remain accurate
    4. Update version when significant changes occur
  style-rules:
    - Use British English spelling (or change to your preference)
    - Avoid exaggerated language
    - Keep descriptions factual and professional
---

# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

**New to this project?** Start with [ONBOARDING.md](ONBOARDING.md) for a complete setup guide.

## Intent Repository

This repository follows the **Intent Repository** pattern where every file carries or inherits the metadata required for its own maintenance.

### Key Files

| File | Purpose | Authority |
|------|---------|-----------|
| `master-mx.yaml` | Enforced policies | Highest - cannot be overridden |
| `MX.yaml` | Repository defaults | Can be overridden by children |
| `Folder MX.yaml` | Folder-specific rules | Inherits from parent |
| `llms.txt` | AI navigation index | Informative only |

## Repository Structure

```
{{PROJECT_NAME}}/
├── .claude/                    # AI assistant configuration
├── .github/                    # GitHub workflows
├── mx-config/                     # Configuration files
│   └── system/                 # System documentation
├── docs/                       # Documentation
│   ├── architecture/           # Architecture Decision Records
│   ├── for-ai/                 # AI-optimised documentation
│   └── specifications/         # PRDs and specs
├── packages/                   # Implementation packages
├── scripts/                    # Build and automation scripts
├── src/                        # Source code
├── master-mx.yaml              # Enforced policies
├── MX.yaml                     # Repository defaults
├── CLAUDE.md                   # AI agent guidance
└── llms.txt                    # AI navigation index
```

## Quick Start

```bash
# Clone repository
git clone {{PROJECT_URL}}
cd {{PROJECT_NAME}}

# Install dependencies
npm install
```

## Documentation

- [ONBOARDING.md](ONBOARDING.md) - Setup guide for new contributors
- [CLAUDE.md](CLAUDE.md) - AI agent instructions
- [LEARNINGS.md](LEARNINGS.md) - Accumulated project learnings

## License

{{LICENSE_INFO}}

## Contact

- **Author:** {{OWNER_NAME}}
- **Email:** {{OWNER_EMAIL}}

---

## Template Credits

This MX Template Repository was created by:

- **Tom Cranstoun** - Principal Consultant at Digital Domain Technologies Ltd, creator of the Intent Repository pattern and Machine Experience (MX) methodology
- **Claude (Opus 4.5)** - Anthropic's AI assistant, collaborating on implementation and documentation

The Intent Repository pattern enables self-documenting repositories where every file carries or inherits the metadata required for its own maintenance.

- **Intent CMS Documentation:** https://github.com/digital-domain-technologies/intent-cms
- **Tom's Website:** https://allabout.network
- **Tom's LinkedIn:** https://www.linkedin.com/in/tom-cranstoun/
