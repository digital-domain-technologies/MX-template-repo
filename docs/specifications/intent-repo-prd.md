---
title: "Product Requirements Document: Intent Repository"
description: "PRD for a repository structure where code, configuration, and documentation carry their own maintenance context through hierarchical metadata inheritance."
author: "Tom Cranstoun"
date: 2026-01-30
lastmod: 2026-01-30
version: "0.1.0"
status: "Draft"
keywords:
  - intent-repository
  - intent-cms
  - metadata-inheritance
  - developer-tools
  - machine-experience
  - mx
  - self-documenting-code
canonical: "https://allabout.network/docs/intent-repo-prd.html"
schema:
  type: "TechArticle"
  articleSection: "Product Documentation"
ai-content-policy: "extract-with-attribution"
ai-freshness: "monthly"
ai-attribution: "required"

data-lake:
  query-id: "dlq-2026-01-30-intent-repo-prd"
  connector: "mx-content-store"
  linked-assets:
    - "intent-cms-prd"
    - "intent-cms-blog-post"
    - "mx-style-guide"
  refresh-trigger: "on-linked-asset-change"

update-instructions:
  source: "Internal product documentation and stakeholder requirements"
  method: |
    1. Review current Intent Repository implementations
    2. Update requirements based on developer feedback
    3. Ensure alignment with Intent CMS and MX principles
    4. Update version number and lastmod date
    5. Keep implementation details (MX.yaml structure, inheritance rules) as internal documentation only
  style-rules:
    - Never count items (e.g. "12 requirements", "three phases")
    - Use factual, professional language without exaggeration
    - Avoid words like: comprehensive, revolutionary, sophisticated, powerful, advanced, essential, crucial, perfect, complete, extensive, excellent, outstanding, amazing, incredible
    - Use British English spelling
  structure:
    - Standard PRD sections: Overview, Problem, Solution, Requirements, Architecture, Milestones
    - Keep technical implementation details minimal—focus on what, not how
    - Include success metrics
---

# Product Requirements Document: Intent Repository

**Version:** 0.1.0  
**Status:** Draft  
**Author:** Tom Cranstoun  
**Date:** 30 January 2026

---

## Executive Summary

Intent Repository extends Intent CMS principles to code repositories. Every file—code, configuration, documentation, assets—carries or inherits the metadata required for its own maintenance. Folder-level metadata creates inheritance hierarchies where shared rules flow down and specific overrides stay local.

The result: repositories that are self-documenting at every level, where any agent (human or AI) can understand, maintain, and contribute to any file without requiring external documentation or institutional knowledge.

---

## Problem Statement

### Current State

Code repositories contain implicit knowledge that isn't captured anywhere:

- Why was this architectural decision made?
- What style rules apply to this folder?
- How should this configuration file be updated when dependencies change?
- What's the relationship between this module and that service?
- Who owns this code and what's the review process?

This knowledge lives in:

- README files that go stale
- Wiki pages nobody updates
- Tribal knowledge that leaves when people do
- Git blame archaeology that requires detective work
- Slack conversations lost to history

### Developer Pain Points

**Onboarding friction.** New developers spend weeks understanding implicit conventions before they can contribute safely.

**AI assistant limitations.** Code assistants lack context about project-specific rules, ownership, and relationships. They generate syntactically correct but contextually wrong code.

**Inconsistent contributions.** Without embedded rules, different developers apply different standards to different parts of the codebase.

**Stale documentation.** Documentation lives separately from code and drifts out of sync.

**Lost context on handover.** When teams change or projects transfer, critical knowledge disappears.

### Business Impact

- Extended onboarding time for new developers
- Increased code review cycles catching style and convention violations
- Technical debt from inconsistent implementation patterns
- AI tools underutilised due to missing context
- Knowledge loss during team transitions

---

## Solution Overview

### Intent Repository

A repository structure where:

- **Folder-level metadata** defines rules, ownership, and context for everything within that folder
- **File-level metadata** provides specific instructions for individual files
- **Inheritance** flows from parent folders to children—shared rules apply broadly, specific overrides apply locally
- **Sidecar files** carry metadata for formats that cannot embed it
- **Validation** ensures metadata remains consistent and complete

### Key Principles

**Inheritance over repetition.** Define rules once at the appropriate level; let children inherit.

**Proximity over centralisation.** Metadata lives next to the code it describes, not in a separate documentation system.

**Machine-readable over prose.** Structured metadata that agents can parse and act upon, not just human-readable text.

**Graceful degradation.** Files without metadata inherit from parents; repositories without metadata still function as normal repositories.

---

## Functional Requirements

### FR-1: Folder-Level Metadata

**FR-1.1** Each folder may contain a metadata file defining rules for that folder and its descendants.

**FR-1.2** Folder metadata must support:

- Style rules (formatting, naming conventions, patterns)
- Ownership (team, individuals, contact information)
- Review requirements (approval process, required reviewers)
- Testing requirements (coverage thresholds, required test types)
- Documentation requirements (what must be documented, format)
- Dependency rules (allowed dependencies, version constraints)
- Build and deployment context (environment, targets, pipelines)

**FR-1.3** Folder metadata must support inheritance modifiers:

- Inherit all (default behaviour)
- Override specific rules
- Extend rules (add to inherited set)
- Block inheritance (stop rules flowing to this subtree)

**FR-1.4** The system must resolve inheritance by walking up the folder tree to the repository root.

### FR-2: File-Level Metadata

**FR-2.1** Individual files may contain or reference metadata specific to that file.

**FR-2.2** File metadata must support:

- Purpose and description
- Update instructions (how to modify this file)
- Source references (where data comes from for generated files)
- Related files (what this file connects to)
- Override rules (exceptions to folder-level rules)

**FR-2.3** File metadata must be embeddable in formats that support it:

- Comments in code files (JS, CSS, HTML, Python, etc.)
- Frontmatter in markdown
- Metadata fields in JSON, YAML, XML
- XMP/EXIF in images
- Document properties in PDFs

**FR-2.4** Files that cannot embed metadata must use sidecar files.

### FR-3: Sidecar Files

**FR-3.1** Sidecar files must use a consistent naming convention that associates them with their parent file.

**FR-3.2** Sidecar files must contain the same metadata structure as embedded metadata.

**FR-3.3** The system must automatically associate sidecar files with their parent files.

**FR-3.4** Operations on parent files (move, rename, delete) must handle sidecars appropriately.

**FR-3.5** Sidecar files must be usable for any file type, including those that support embedded metadata (for cases where embedding is undesirable).

### FR-4: Inheritance Resolution

**FR-4.1** When resolving metadata for a file, the system must:

1. Check for file-level metadata (embedded or sidecar)
2. Walk up the folder tree, collecting folder metadata
3. Merge metadata according to inheritance rules
4. Return the fully resolved metadata for that file

**FR-4.2** More specific metadata must override more general metadata (file beats folder, child folder beats parent folder).

**FR-4.3** The system must detect and report inheritance conflicts.

**FR-4.4** The system must support querying effective metadata for any path.

### FR-5: Metadata for Common File Types

**FR-5.1** JavaScript/TypeScript files: metadata in JSDoc-style comments or leading comment block.

**FR-5.2** CSS/SCSS/Less files: metadata in leading comment block.

**FR-5.3** HTML files: metadata in HTML comment or meta tags.

**FR-5.4** Python files: metadata in module docstring or leading comment.

**FR-5.5** Markdown files: metadata in YAML frontmatter.

**FR-5.6** JSON files: metadata in reserved key (e.g., `_meta` or `$intent`).

**FR-5.7** YAML files: metadata in reserved key or document header.

**FR-5.8** Image files: metadata in XMP/EXIF or sidecar.

**FR-5.9** Binary files: metadata in sidecar only.

**FR-5.10** Minified files: metadata in sidecar (source files carry embedded metadata).

### FR-6: Validation

**FR-6.1** The system must validate metadata against a defined schema.

**FR-6.2** The system must detect missing required metadata at each level.

**FR-6.3** The system must detect orphaned sidecars (sidecars without parent files).

**FR-6.4** The system must detect inheritance conflicts.

**FR-6.5** Validation must be runnable as:

- CLI command
- Pre-commit hook
- CI/CD pipeline step
- IDE integration

**FR-6.6** Validation must report:

- Files missing required metadata
- Invalid metadata format
- Schema violations
- Inheritance conflicts
- Orphaned sidecars
- Coverage statistics

### FR-7: Querying and Reporting

**FR-7.1** Query effective metadata for any file path.

**FR-7.2** Query all files matching specific metadata criteria (e.g., "all files owned by team X").

**FR-7.3** Query inheritance chain for any path (show where each rule comes from).

**FR-7.4** Generate coverage report (percentage of files with metadata).

**FR-7.5** Generate ownership report (who owns what).

**FR-7.6** Generate dependency graph based on metadata relationships.

### FR-8: Integration with Development Tools

**FR-8.1** Git hooks for validation on commit.

**FR-8.2** CI/CD integration for validation on pull request.

**FR-8.3** IDE extensions for:

- Viewing effective metadata for current file
- Editing metadata with schema validation
- Navigating to related files
- Showing inheritance chain

**FR-8.4** AI assistant integration:

- Provide effective metadata as context for code generation
- Validate generated code against metadata rules
- Suggest metadata for new files based on location

### FR-9: Ignore Patterns

**FR-9.1** The repository root must support an ignore file that specifies paths excluded from intent metadata processing.

**FR-9.2** The ignore file must inherit from .gitignore—any path ignored by Git is automatically ignored by Intent Repository.

**FR-9.3** The ignore file must support additional patterns beyond .gitignore for intent-specific exclusions.

**FR-9.4** Ignored paths must:

- Not be scanned for metadata
- Not appear in coverage reports
- Not trigger validation errors for missing metadata
- Not be indexed by the query engine

**FR-9.5** The ignore file must support the same pattern syntax as .gitignore.

**FR-9.6** The system must resolve ignore patterns before processing any folder or file.

### FR-10: Local Machine Configuration

**FR-10.1** The Intent Repository pattern must extend beyond repositories to local machine configuration.

**FR-10.2** The inheritance hierarchy must be:

1. Machine-level master (system-wide defaults)
2. Device-level master (per-drive/volume defaults)
3. User-level defaults (home directory)
4. Workspace-level defaults (project folders)
5. Repository-level master (repository-wide policies that cannot be overridden)
6. Repository root (repository defaults)
7. Folder-level (walking down the tree)
8. File-level

**FR-10.3** Machine-level master metadata must:

- Apply to all users and all drives on the machine
- Define organisation-wide policies when deployed centrally
- Be located in a system configuration path

**FR-10.4** Device-level master metadata must:

- Apply to all content on a specific drive or volume
- Support different policies for different storage (e.g., external drives, network mounts)
- Be located at the root of each drive/volume

**FR-10.5** User-level metadata must support:

- User-specific defaults (home directory)
- Project workspace overrides
- Per-folder customisation

**FR-10.6** Repository-level master metadata must:

- Define repository-wide policies that cannot be overridden by folders or files
- Enforce architectural decisions, security requirements, and compliance rules
- Be located at the repository root with a distinct filename
- Take precedence over folder and file metadata for specified rules

**FR-10.7** Local machine metadata must be kept separate from repository metadata—local settings do not commit to repositories.

**FR-10.8** When resolving metadata, the system must merge in the order specified in FR-10.2, with more specific levels overriding more general levels, except for rules marked as non-overridable in master files.

**FR-10.9** Local machine metadata must support user-specific overrides that do not affect other users of the same repository.

**FR-10.10** The system must clearly indicate when resolved metadata includes values from machine, device, user, repository master, or repository levels.

**FR-10.11** The system must support querying the full inheritance chain to show where each value originates.

**FR-10.12** Master files (machine, device, repository) must support marking specific rules as:

- Overridable (default behaviour, children can override)
- Non-overridable (enforced, children cannot override)
- Extendable (children can add to but not remove from)

### FR-11: Sub-Repository Boundaries

**FR-11.1** When a repository contains sub-repositories (nested repositories with their own master-mx.yaml), inheritance must stop at the sub-repository boundary.

**FR-11.2** Each sub-repository must establish its own inheritance chain starting from its own master-mx.yaml.

**FR-11.3** Sub-repository detection must identify boundaries by the presence of a master-mx.yaml file.

**FR-11.4** The inheritance chain for a file in a sub-repository must be:

1. Machine-level master
2. Device-level master
3. User-level defaults
4. Workspace-level defaults
5. Sub-repository master (not parent repository master)
6. Sub-repository root MX.yaml
7. Folder-level within sub-repository
8. File-level

**FR-11.5** Parent repository policies must not leak into sub-repositories unless explicitly referenced.

**FR-11.6** Sub-repositories may optionally reference parent repository metadata using explicit inheritance declarations.

**FR-11.7** The system must clearly indicate sub-repository boundaries when displaying inheritance chains.

**FR-11.8** Monorepo structures with multiple packages must each be treated as sub-repositories if they contain their own master-mx.yaml.

**FR-11.9** Sub-repositories without a master-mx.yaml must inherit from the nearest ancestor master-mx.yaml (parent repository or higher).

### FR-12: Multi-Repository Hub Authority

**FR-12.1** In multi-repository projects where repositories are managed together but stored separately, a hub repository may define authority over child repositories.

**FR-12.2** The hub repository must contain a hub-mx.yaml that declares authority over specified child repositories.

**FR-12.3** Hub authority policies cannot be overridden by child repositories—the hub has ultimate authority over its declared children.

**FR-12.4** The inheritance chain for a file in a child repository of a hub must be:

1. Machine-level master
2. Device-level master
3. User-level defaults
4. Workspace-level defaults
5. Hub authority (enforced, cannot be overridden)
6. Child repository master
7. Child repository root MX.yaml
8. Folder-level within child repository
9. File-level

**FR-12.5** Child repositories must explicitly declare their hub relationship to receive hub policies.

**FR-12.6** Hub policies take precedence over all child repository policies, including child master-mx.yaml enforced rules.

**FR-12.7** The hub-mx.yaml must specify:

- List of child repositories under its authority
- Policies that apply to all children
- Per-child policy overrides where needed

**FR-12.8** Child repositories may define their own enforced policies, but these cannot contradict hub policies.

**FR-12.9** Conflicts between hub and child policies must resolve in favour of the hub.

**FR-12.10** The system must clearly indicate when resolved metadata includes hub-enforced values that cannot be overridden.

**FR-12.11** Hub authority must work across repository boundaries, supporting:

- Repositories on the same machine
- Repositories on different machines (via hub reference URL or path)
- Repositories in different version control systems

**FR-12.12** Child repositories must be able to verify hub authority through cryptographic signatures or trusted paths.

---

## Non-Functional Requirements

### NFR-1: Performance

**NFR-1.1** Metadata resolution must complete in under 50ms for any file path.

**NFR-1.2** Full repository scan must complete in under 30 seconds for repositories with up to 100,000 files.

**NFR-1.3** Validation must be fast enough for pre-commit hooks (under 5 seconds for changed files).

### NFR-2: Compatibility

**NFR-2.1** Must work with any Git hosting platform (GitHub, GitLab, Bitbucket, etc.).

**NFR-2.2** Must not require changes to standard Git workflows.

**NFR-2.3** Must not interfere with existing tooling (linters, formatters, bundlers).

**NFR-2.4** Repositories without intent metadata must function normally.

### NFR-3: Scalability

**NFR-3.1** Must support monorepos with millions of files.

**NFR-3.2** Must support deep folder hierarchies (100+ levels).

**NFR-3.3** Must handle large metadata files efficiently.

### NFR-4: Maintainability

**NFR-4.1** Metadata format must be human-readable and editable.

**NFR-4.2** Schema must be versioned and support migration.

**NFR-4.3** Tooling must be open source.

### NFR-5: Security

**NFR-5.1** Metadata must not contain secrets (validation must flag potential secrets).

**NFR-5.2** Metadata execution (if any) must be sandboxed.

**NFR-5.3** Sidecar files must follow same access controls as parent files.

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                      Consumer Layer                              │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐       │
│  │   CLI    │  │   IDE    │  │  CI/CD   │  │    AI    │       │
│  │  Tools   │  │Extensions│  │ Pipeline │  │Assistant │       │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘       │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Intent Repo Core                            │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  Metadata   │  │ Inheritance │  │ Validation  │             │
│  │   Parser    │  │  Resolver   │  │   Engine    │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   Query     │  │   Report    │  │   Schema    │             │
│  │   Engine    │  │  Generator  │  │  Registry   │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                      File System Layer                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Repository Files                      │   │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐    │   │
│  │  │ Folder  │  │Embedded │  │ Sidecar │  │  Code   │    │   │
│  │  │Metadata │  │Metadata │  │  Files  │  │  Files  │    │   │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘    │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

### Components

**Consumer Layer:** Tools and integrations that use intent metadata—CLI, IDE extensions, CI/CD pipelines, AI assistants.

**Intent Repo Core:**

- **Metadata Parser:** Extracts metadata from folder files, embedded comments, frontmatter, and sidecars.
- **Inheritance Resolver:** Walks the folder tree and merges metadata according to inheritance rules.
- **Validation Engine:** Checks metadata against schemas and reports violations.
- **Query Engine:** Finds files matching metadata criteria.
- **Report Generator:** Produces coverage, ownership, and dependency reports.
- **Schema Registry:** Manages metadata schema versions and migrations.

**File System Layer:** The actual repository files—folder metadata, files with embedded metadata, sidecar files, and code files.

**Local Machine Layer:** User-level metadata outside repositories that provides personal defaults and overrides.

---

## Example Repository Structure

```
# Machine level (system-wide)
/etc/intent/master-mx.yaml       # Linux/macOS
C:\ProgramData\intent\master-mx.yaml  # Windows

# Device level (per-drive/volume)
/Volumes/ExternalDrive/master-mx.yaml  # macOS external drive
D:\master-mx.yaml                      # Windows secondary drive
/mnt/network-share/master-mx.yaml      # Network mount

# User level (outside repositories)
~/.mx-config/intent/
├── MX.yaml                      # User-level defaults
└── .mxignore                    # User-level ignores

# Workspace level
~/projects/
├── MX.yaml                      # Workspace-level defaults (optional)
└── my-project/                  # Repository starts here
    ├── .gitignore
    ├── .mxignore
    ├── master-mx.yaml           # Repository master (non-overridable policies)
    ├── MX.yaml                  # Repository root (overridable defaults)
    └── ...

# Inheritance chain example:
# /etc/intent/master-mx.yaml           (machine master)
#   └── /home/user/.mx-config/intent/MX.yaml  (user defaults)
#       └── /home/user/projects/MX.yaml    (workspace defaults)
#           └── repo/master-mx.yaml        (repo master - enforced)
#               └── repo/MX.yaml           (repo defaults)
#                   └── repo/src/MX.yaml   (folder)
#                       └── repo/src/utils/MX.yaml  (folder)
#                           └── file.ts    (file metadata)

# Sub-repository boundary example (monorepo):
# repo/master-mx.yaml                  (parent repo master)
# repo/packages/
#   └── package-a/
#       ├── master-mx.yaml             (sub-repo master - NEW inheritance root)
#       ├── MX.yaml                    (sub-repo defaults)
#       └── src/MX.yaml                (inherits from package-a, NOT parent repo)
#   └── package-b/
#       └── (no master-mx.yaml)        (inherits from parent repo/master-mx.yaml)

# Repository structure
repository/
├── .gitignore                   # Standard Git ignore
├── .mxignore                    # Intent ignore (inherits from .gitignore)
├── master-mx.yaml               # Repository master (enforced policies)
├── MX.yaml                      # Root-level defaults (overridable)
├── src/
│   ├── MX.yaml                  # Source code rules (inherits from root)
│   ├── components/
│   │   ├── MX.yaml              # Component-specific rules
│   │   ├── Button.tsx           # Embedded metadata in JSDoc
│   │   ├── Button.test.tsx
│   │   └── Button.module.css    # Embedded metadata in comment
│   ├── utils/
│   │   ├── MX.yaml              # Utility rules
│   │   ├── format.ts
│   │   └── validate.ts
│   └── generated/
│       ├── MX.yaml              # Generated code rules (block inheritance of style rules)
│       ├── api-client.ts        # Embedded metadata with generation source
│       └── api-client.ts.mx     # Sidecar for additional context
├── assets/
│   ├── MX.yaml                  # Asset rules
│   ├── logo.svg                 # Embedded metadata
│   ├── hero.jpg                 # Cannot embed—uses sidecar
│   └── hero.jpg.mx              # Sidecar for hero.jpg
├── docs/
│   ├── MX.yaml                  # Documentation rules
│   └── api.md                   # Frontmatter metadata
├── packages/                    # Monorepo packages
│   ├── core/                    # Sub-repository with own master
│   │   ├── master-mx.yaml       # Sub-repo master (inheritance boundary)
│   │   ├── MX.yaml              # Sub-repo defaults
│   │   └── src/
│   │       ├── MX.yaml          # Inherits from core/, not parent repo
│   │       └── index.ts
│   └── utils/                   # Package without master (inherits from parent)
│       ├── MX.yaml              # Inherits from repo/master-mx.yaml
│       └── src/
│           └── helpers.ts
└── mx-config/
    ├── MX.yaml                  # Config rules
    ├── webpack.config.js        # Embedded metadata
    └── tsconfig.json            # Reserved key metadata
```

---

## Success Metrics

### Adoption Metrics

- Percentage of repositories with intent metadata enabled
- Percentage of folders with folder-level metadata
- Percentage of files with effective metadata (inherited or direct)
- Number of developers using IDE extensions

### Quality Metrics

- Validation pass rate in CI/CD
- Reduction in style-related PR comments
- Reduction in "how does this work" questions
- Time to resolve inheritance for any path

### Efficiency Metrics

- Developer onboarding time (time to first meaningful commit)
- AI assistant accuracy (correct context usage rate)
- Documentation freshness (metadata lastmod vs file lastmod)

### Business Metrics

- Reduction in code review cycles
- Reduction in onboarding support requests
- Increase in AI-assisted contributions

---

## Milestones

### Phase 1: Core Infrastructure

- Define metadata schema for folder and file levels
- Implement metadata parser for common file types
- Build inheritance resolver
- Create CLI for querying effective metadata

### Phase 2: Validation and Reporting

- Implement validation engine
- Create schema registry
- Build coverage and ownership reports
- Add CI/CD integration

### Phase 3: Developer Tooling

- Build VS Code extension
- Implement Git pre-commit hooks
- Create JetBrains IDE plugin
- Add GitHub/GitLab integration for PR checks

### Phase 4: AI Integration

- Define context format for AI assistants
- Build integration with common AI coding tools
- Implement metadata-aware code generation validation
- Create feedback loop for metadata suggestions

### Phase 5: Advanced Features

- Cross-repository metadata references
- Metadata versioning and migration tools
- Visual inheritance explorer
- Integration with Intent CMS and Intent Data Lake

---

## Relationship to Intent CMS and Intent Data Lake

Intent Repository applies the same principles as Intent CMS to code:

| Intent CMS | Intent Repository |
|------------|-------------------|
| Content assets | Code files |
| YAML frontmatter | Folder metadata + embedded comments |
| Sidecar.mx files | Sidecar files for strict formats |
| Intent Data Lake | Repository-level metadata index |
| Update instructions | Maintenance context |
| Style rules | Code style and convention rules |

The Intent Data Lake can index Intent Repositories alongside content, creating a unified view of all organisational assets—content, code, and configuration—with their relationships and maintenance context.

---

## Open Questions

- How do we handle metadata in vendored/third-party code?
- Should generated code inherit metadata from its generator or its location?
- How do we version folder metadata independently of code changes?
- What's the migration path for existing repositories?
- How do we handle metadata conflicts in merge scenarios?
- Should metadata be included in or excluded from code coverage calculations?

---

## Appendix A: llms.txt - Informative Index File

### Purpose

The `llms.txt` file is an **informative index** that helps AI agents and LLMs understand and navigate the repository. It follows an emerging standard for providing machine-readable repository overviews.

### Key Characteristics

**FR-A.1** The `llms.txt` file is **informative only**—it describes the repository but does not define authoritative rules or policies.

**FR-A.2** AI agents and tools **must not** treat `llms.txt` as a source of authority. It exists to aid discovery and navigation, not to govern behaviour.

**FR-A.3** The `llms.txt` file **should not** be modified by automated agents. It is maintained by repository owners to reflect the current state of the repository.

**FR-A.4** Authoritative metadata comes from:

- `master-mx.yaml` for enforced policies
- `MX.yaml` files for inherited defaults and rules
- File-level frontmatter or `$intent` keys for file-specific metadata

### Content Guidelines

The `llms.txt` file should include:

- Repository purpose and description
- Key concepts and terminology
- Important file locations
- Navigation structure overview
- Author and contact information

### Relationship to Intent Metadata

| File | Role | Authority |
|------|------|-----------|
| `llms.txt` | Informative index for discovery | None—descriptive only |
| `master-mx.yaml` | Enforced repository policies | Highest—cannot be overridden |
| `MX.yaml` | Inherited defaults | Can be overridden by children |
| File frontmatter | File-specific metadata | Applies to that file only |

### Example

```text
# Project Name - LLM Index
#
# @intent
# purpose: Index file for LLM/AI agent navigation
# note: This file is INFORMATIVE ONLY - not authoritative
# authority: none - see master-mx.yaml and MX.yaml for rules

This file helps AI agents understand and navigate this repository.

## Repository Purpose
[Description of what the repository does]

## Key Files
- master-mx.yaml - Enforced policies (AUTHORITATIVE)
- MX.yaml - Repository defaults (AUTHORITATIVE)
- README.md - Human-readable overview
- CLAUDE.md - AI agent guidance

## Navigation
[Directory structure overview]
```

---

## Appendix B: Ignore File Example (.mxignore)

```gitignore
# .mxignore
# Inherits all patterns from .gitignore automatically

# Additional intent-specific ignores
# (These paths exist in Git but should not have intent metadata)

# Third-party vendored code
vendor/
third_party/

# Legacy code pending migration
src/legacy/

# Auto-generated lock files
package-lock.json
yarn.lock
pnpm-lock.yaml

# IDE and editor files
.idea/
.vscode/
*.swp

# Test fixtures that intentionally lack metadata
test/fixtures/invalid/
```

---

## Appendix C: Local Machine Configuration Example

```yaml
# /etc/intent/master-mx.yaml (Linux/macOS)
# C:\ProgramData\intent\master-mx.yaml (Windows)
# Machine-level master - applies to all users and drives

intent:
  version: "1.0"
  level: "machine"

organisation:
  name: "Acme Corp"
  domain: "acme.com"

policies:
  # Organisation-wide security policies
  security:
    secrets-detection: true
    secrets-action: "block"  # block, warn, ignore
  
  # Compliance requirements
  compliance:
    require-ownership: true
    require-licence-headers: true
    approved-licences:
      - "MIT"
      - "Apache-2.0"
      - "BSD-3-Clause"
  
  # AI assistant policies
  ai:
    allow-code-generation: true
    require-human-review: true
    context-sharing: "internal-only"  # internal-only, public, none

defaults:
  # Default ownership for all content on this machine
  ownership:
    organisation: "Acme Corp"
```

```yaml
# /Volumes/ClientProjects/master-mx.yaml
# Device-level master - applies to all content on this drive

intent:
  version: "1.0"
  level: "device"

device:
  name: "Client Projects Drive"
  type: "external"
  classification: "confidential"

policies:
  # Stricter policies for client work
  security:
    encryption-required: true
    secrets-action: "block"
  
  # Client confidentiality
  sharing:
    external-sharing: false
    ai-context-sharing: "none"
  
  # Backup requirements
  backup:
    required: true
    frequency: "daily"

defaults:
  # All projects on this drive are client work
  ownership:
    type: "client-project"
  
  review:
    required-approvals: 2
```

```yaml
# ~/.mx-config/intent/MX.yaml
# User-level defaults applied to all repositories

intent:
  version: "1.0"
  level: "user"

user:
  name: "Developer Name"
  email: "dev@example.com"

defaults:
  # Default ownership when not specified in repo
  ownership:
    contact: "dev@example.com"
  
  # Preferred tools
  style:
    formatter: "prettier"
    linter: "eslint"
  
  # AI assistant preferences
  ai:
    context-level: "full"  # or "summary", "minimal"
    suggestions: true

overrides:
  # Personal overrides that never commit to repos
  review:
    # Skip approval requirements for local testing
    local-bypass: true
  
  validation:
    # Warn instead of error during development
    strict-mode: false
```

```yaml
# ~/projects/MX.yaml
# Workspace-level defaults for all projects in this folder

intent:
  version: "1.0"
  level: "workspace"

defaults:
  # All projects here belong to this team
  ownership:
    team: "platform-team"
  
  # Shared build configuration
  build:
    node-version: "20"
    package-manager: "pnpm"
```

```yaml
# repository/master-mx.yaml
# Repository master - enforced policies that cannot be overridden

intent:
  version: "1.0"
  level: "repository-master"

enforced:
  # These rules CANNOT be overridden by folders or files
  
  security:
    # All code must pass security scanning
    require-security-scan: true
    blocked-patterns:
      - "eval("
      - "dangerouslySetInnerHTML"
    secrets-detection: true
    secrets-action: "block"
  
  compliance:
    # Licence requirements for this repository
    licence: "MIT"
    require-licence-headers: true
    header-template: |
      Copyright (c) 2026 Acme Corp
      SPDX-License-Identifier: MIT
  
  architecture:
    # Enforced architectural boundaries
    restricted-imports:
      - from: "src/ui/**"
        cannot-import: "src/database/**"
      - from: "src/shared/**"
        cannot-import: "src/features/**"
  
  testing:
    # Minimum coverage that cannot be lowered
    min-coverage: 70
    required-types:
      - "unit"

defaults:
  # These CAN be overridden by folders or files
  
  style:
    formatter: "prettier"
    linter: "eslint"
  
  testing:
    # Default coverage (can be raised, not lowered below enforced.testing.min-coverage)
    coverage-threshold: 80
  
  review:
    required-approvals: 1
```

```yaml
# repository/MX.yaml
# Repository root - default settings (can be overridden)

intent:
  version: "1.0"
  level: "repository"

ownership:
  team: "core-team"
  contacts:
    - name: "Tech Lead"
      email: "lead@example.com"

defaults:
  documentation:
    required: true
    format: "jsdoc"
  
  review:
    required-approvals: 2  # Raises the master default of 1
    auto-assign: true
```

```yaml
# repository/packages/core/master-mx.yaml
# Sub-repository master - establishes new inheritance boundary
# Parent repo policies do NOT apply here unless explicitly inherited

intent:
  version: "1.0"
  level: "sub-repository-master"
  boundary: true  # Marks inheritance boundary

parent:
  # Optional: explicitly inherit specific policies from parent
  inherit-from: "../../master-mx.yaml"
  inherit-rules:
    - "enforced.security"      # Inherit security policies
    - "enforced.compliance"    # Inherit compliance policies
  # All other parent policies are NOT inherited

enforced:
  # Sub-repo specific enforced policies
  architecture:
    no-external-dependencies: true
    allowed-imports:
      - "@internal/shared"
      - "lodash"
  
  testing:
    # Higher coverage requirement than parent
    min-coverage: 90
    required-types:
      - "unit"
      - "integration"

defaults:
  ownership:
    team: "core-library-team"
    contact: "core@example.com"
  
  review:
    required-approvals: 3  # Stricter than parent
```

```yaml
# hub-repository/hub-mx.yaml
# Hub authority - CANNOT be overridden by child repositories

intent:
  version: "1.0"
  level: "hub"

hub:
  name: "Acme Platform"
  description: "Central authority for all Acme platform repositories"

children:
  # List of repositories under this hub's authority
  repositories:
    - name: "frontend-app"
      path: "../frontend-app"  # Local path
      url: "git@github.com:acme/frontend-app.git"
    - name: "backend-api"
      path: "../backend-api"
      url: "git@github.com:acme/backend-api.git"
    - name: "shared-libs"
      path: "../shared-libs"
      url: "git@github.com:acme/shared-libs.git"

# These policies CANNOT be overridden by any child repository
enforced:
  security:
    # All children must follow these security rules
    secrets-detection: true
    secrets-action: "block"
    required-scanning:
      - "sast"
      - "dependency-check"
    blocked-packages:
      - "event-stream"  # Known compromised
      - "colors"        # Known compromised
  
  compliance:
    # Licence requirements across all repositories
    licence: "MIT"
    require-licence-headers: true
    approved-dependencies:
      - "MIT"
      - "Apache-2.0"
      - "BSD-3-Clause"
    blocked-licences:
      - "GPL-3.0"
      - "AGPL-3.0"
  
  versioning:
    # All repos must follow same versioning scheme
    scheme: "semver"
    require-changelog: true
  
  ci:
    # Required CI checks for all repositories
    required-checks:
      - "lint"
      - "test"
      - "security-scan"
    branch-protection:
      main:
        required-approvals: 2
        require-ci-pass: true

# Per-child overrides (still cannot be overridden by the child itself)
child-overrides:
  frontend-app:
    enforced:
      testing:
        # Frontend has additional requirements
        required-types:
          - "unit"
          - "e2e"
          - "visual-regression"
  
  backend-api:
    enforced:
      testing:
        min-coverage: 90  # Higher bar for API
        required-types:
          - "unit"
          - "integration"
          - "contract"

defaults:
  # Defaults that children CAN override
  style:
    formatter: "prettier"
  
  review:
    required-approvals: 1
```

```yaml
# frontend-app/master-mx.yaml
# Child repository - declares hub relationship
# Hub policies CANNOT be overridden here

intent:
  version: "1.0"
  level: "repository-master"

hub:
  # Declare relationship to hub
  parent: "git@github.com:acme/hub-repository.git"
  # Or local path
  # parent: "../hub-repository"
  
  # Verification (optional but recommended)
  verify: true
  trusted-key: "ssh-ed25519 AAAA..."  # Hub's signing key

# These are enforced WITHIN this repo, but cannot contradict hub
enforced:
  architecture:
    # Frontend-specific boundaries
    restricted-imports:
      - from: "src/components/**"
        cannot-import: "src/api/**"
  
  testing:
    # Can ADD requirements, but cannot REMOVE hub requirements
    additional-required-types:
      - "accessibility"

defaults:
  ownership:
    team: "frontend-team"
    contact: "frontend@example.com"
```

---

## Appendix D: Folder Metadata Schema (Draft)

```yaml
# MX.yaml - Folder-level metadata
intent:
  version: "1.0"
  
ownership:
  team: "team-name"
  contacts:
    - name: "Developer Name"
      email: "dev@example.com"
      role: "maintainer"
  
style:
  inherit: true  # or false to block, or "extend" to add
  rules:
    - rule-id: "naming-convention-camelcase"
    - rule-id: "max-file-length-500"
  formatter: "prettier"
  linter: "eslint"
  config-path: "../../.prettierrc"

review:
  required-approvals: 2
  required-reviewers:
    - "team-lead"
  auto-assign: true

testing:
  coverage-threshold: 80
  required-types:
    - "unit"
    - "integration"

documentation:
  required: true
  format: "jsdoc"
  
dependencies:
  allowed-packages:
    - "lodash"
    - "date-fns"
  blocked-packages:
    - "moment"  # Use date-fns instead
  version-policy: "exact"  # or "range", "latest"

build:
  target: "es2020"
  output: "../dist"
  
custom:
  # Project-specific metadata
  feature-flags:
    - "new-checkout-flow"
```

---

## Appendix E: File Metadata Examples

### JavaScript (JSDoc comment)

```javascript
/**
 * @intent
 * purpose: Utility functions for date formatting
 * update-instructions: |
 *   When adding new formats, ensure locale support.
 *   Run tests with TZ=UTC to verify timezone handling.
 * related-files:
 *   - ./format.test.ts
 *   - ../types/date.ts
 * overrides:
 *   coverage-threshold: 95  # Higher than folder default
 */

export function formatDate(date, format) {
  // ...
}
```

### CSS (comment block)

```css
/*
@intent
purpose: Button component styles
update-instructions: |
  Follows design system tokens from ../tokens.css.
  Do not use raw colour values—always reference tokens.
related-files:
  - ../tokens.css
  - ../../components/Button.tsx
*/

.button {
  background: var(--color-primary);
}
```

### JSON (reserved key)

```json
{
  "$intent": {
    "purpose": "TypeScript compiler configuration",
    "update-instructions": "Sync with root tsconfig.json when base settings change",
    "related-files": ["../../tsconfig.json"]
  },
  "compilerOptions": {
    "target": "es2020"
  }
}
```

### Generated file with sidecar

```
api-client.ts.mx
```

```yaml
intent:
  version: "1.0"
  purpose: "Generated API client from OpenAPI spec"
  
generation:
  source: "../specs/api.yaml"
  tool: "openapi-generator"
  tool-version: "6.0.0"
  command: "openapi-generator generate -i ../specs/api.yaml -g typescript-fetch"
  
update-instructions: |
  DO NOT EDIT DIRECTLY.
  1. Update ../specs/api.yaml
  2. Run: npm run generate-api-client
  3. Commit both spec and generated client together

overrides:
  style:
    inherit: false  # Generated code has its own style
  review:
    required-approvals: 1  # Lower bar for generated code
```

---

## Appendix F: Practical Implementation Patterns

This appendix documents patterns validated through actual implementation of Intent Repository.

### F.1: Repository Root Files

A compliant Intent Repository requires these files at the repository root:

| File | Purpose | Authority Level |
|------|---------|-----------------|
| `master-mx.yaml` | Enforced policies that cannot be overridden | Highest |
| `MX.yaml` | Repository defaults that can be overridden | High |
| `.mxignore` | Patterns excluded from intent metadata processing | Configuration |
| `llms.txt` | Informative index for AI navigation | None (descriptive only) |
| `CLAUDE.md` | AI agent guidance (or `AGENTS.md`) | Documentation |

### F.2: JSON File Metadata Using $intent Key

For JSON configuration files, use the `$intent` reserved key:

```json
{
  "$intent": {
    "purpose": "Description of what this configuration does",
    "update-instructions": "How to modify this file safely",
    "related-files": ["./other-config.json", "../MX.yaml"]
  },
  "actualConfigKey": "value",
  "anotherKey": "value"
}
```

**Placement rules:**

- `$intent` should be the first key in the object for visibility
- The `$intent` key is ignored by applications reading the config
- All standard intent metadata fields are supported

**Examples of JSON files that benefit from $intent:**

- `package.json` - npm configuration
- `tsconfig.json` - TypeScript configuration
- `.markdownlint.json` - Linting rules
- VS Code `settings.json` and `extensions.json`

### F.3: Comment-Based Metadata for Text Files

For files that support comments but not structured metadata (like `llms.txt`), use YAML in comments:

```text
# File Title
#
# @intent
# purpose: Description of the file's purpose
# audience: Who this file is for
# authority: NONE | LOW | NORMAL | HIGH
# update-instructions: |
#   1. Step one
#   2. Step two
# related-files:
#   - ./related-file.md
#   - ./another-file.yaml

Actual file content starts here...
```

### F.4: Markdown Frontmatter Schema

All markdown files should include YAML frontmatter with this structure:

```yaml
---
title: "Document Title"
description: "Brief description of the document"
author: "Author Name"
date: 2026-01-30
lastmod: 2026-01-30
version: "0.1.0"
keywords:
  - keyword1
  - keyword2
schema:
  type: "TechArticle"  # or HowTo, BlogPosting, etc.
ai-content-policy: "extract-with-attribution"
ai-freshness: "weekly"  # or monthly, daily
ai-attribution: "required"

intent:
  purpose: "What this document achieves"
  audience: "Who should read this"

related-files:
  - ./related-doc.md
  - ../mx-config/MX.yaml

update-instructions:
  source: "Where updates come from"
  method: |
    1. First step
    2. Second step
  style-rules:
    - Rule one
    - Rule two
---
```

### F.5: Folder MX.yaml Minimal Template

Every folder should have an `MX.yaml` file. Minimal template:

```yaml
# MX.yaml
# Folder-level metadata for [folder-name]/

intent:
  version: "1.0"
  level: "folder"

purpose: |
  Brief description of what this folder contains
  and its role in the repository.

ownership:
  inherit: true  # Or specify team/contacts

style:
  inherit: true  # Or override specific rules

update-instructions:
  method: |
    1. How to add new files to this folder
    2. What standards apply
```

### F.6: Distinguishing Authoritative vs Informative Files

**Authoritative files** (define rules, enforce policies):

- `master-mx.yaml` - Cannot be overridden
- `MX.yaml` files - Can be overridden by children
- File frontmatter - Applies to that file
- `$intent` keys in JSON - Applies to that file

**Informative files** (describe, do not enforce):

- `llms.txt` - Navigation aid only
- `README.md` - Human documentation
- Comments in code - Context for humans/AI

AI agents must:

- Follow rules from authoritative files
- Use informative files for discovery only
- Never modify informative files automatically
- Never treat informative content as policy

### F.7: Files Excluded from Intent Metadata

The `.mxignore` file specifies paths that should not have intent metadata:

```gitignore
# .mxignore inherits from .gitignore automatically

# User-specific configuration
.claude/settings.local.json
.vscode/

# Generated/vendored code
node_modules/
vendor/
dist/

# Lock files (auto-generated)
package-lock.json
yarn.lock
```

These files:

- Are not scanned for metadata
- Do not appear in coverage reports
- Do not trigger validation errors
- Are not indexed for queries

### F.8: AI Agent Guidance File (CLAUDE.md/AGENTS.md)

The AI guidance file should include:

1. **Authoritative vs Informative distinction** - Clear list of which files define rules
2. **Key files section** - Organised by authority level
3. **Style guidelines** - Inherited from master-mx.yaml enforced rules
4. **Common tasks** - How to add documentation, create packages
5. **Commands** - Available npm scripts and their purposes

Example structure:

```markdown
## Key Files

### Authoritative Metadata (Use These for Rules)
- **master-mx.yaml** - Enforced policies (CANNOT be overridden)
- **MX.yaml** - Repository defaults

### Informative Files (Do Not Use as Authority)
- **llms.txt** - Navigation aid only

## Important: llms.txt is Informative Only
[Explanation of why and what to use instead]
```

---

## Appendix G: Reference Implementation Structure

Complete example of an Intent Repository structure:

```
repository/
├── .claude/                    # AI assistant configuration
│   ├── MX.yaml                 # Folder metadata
│   ├── commands/               # Custom commands
│   ├── hooks/                  # Git hooks
│   ├── skills/                 # Reusable workflows
│   └── settings.local.json     # Local settings (in .mxignore)
│
├── .github/                    # GitHub configuration
│   ├── MX.yaml                 # Folder metadata
│   └── workflows/              # CI/CD workflows
│
├── .vscode/                    # VS Code settings (in .mxignore)
│   ├── settings.json           # With $intent key
│   └── extensions.json         # With $intent key
│
├── mx-config/                     # Configuration files
│   ├── MX.yaml                 # Folder metadata
│   ├── .editorconfig           # Editor config (sidecar if needed)
│   └── .markdownlint.json      # With $intent key
│
├── docs/                       # Documentation
│   ├── MX.yaml                 # Folder metadata
│   ├── architecture/           # ADRs
│   │   └── MX.yaml
│   ├── for-ai/                 # AI-optimised docs
│   │   └── MX.yaml
│   └── specifications/         # PRDs and specs
│       └── MX.yaml
│
├── packages/                   # Implementation packages
│   └── MX.yaml                 # Folder metadata
│
├── scripts/                    # Automation scripts
│   └── MX.yaml                 # Folder metadata
│
├── .gitignore                  # Git exclusions
├── .mxignore                   # Intent metadata exclusions
├── master-mx.yaml              # Repository master (ENFORCED)
├── MX.yaml                     # Repository defaults
├── CLAUDE.md                   # AI agent guidance
├── LEARNINGS.md                # Accumulated learnings
├── llms.txt                    # LLM index (INFORMATIVE ONLY)
├── ONBOARDING.md               # New contributor guide
├── package.json                # With $intent key
└── README.md                   # With YAML frontmatter
```

Every markdown file has YAML frontmatter.
Every JSON config file has a `$intent` key.
Every folder has an `MX.yaml` file.
The repository root has `master-mx.yaml` (enforced) and `MX.yaml` (defaults).

---

*Tom Cranstoun is Principal Consultant at Digital Domain Technologies Ltd and founder of the Machine Experience community.*

*Tom also has a digital twin built on MX principles, available at mx.machine.experience@gmail.com.*

*This document was generated by Tom's intent CMS and intent data lake—like Adobe EDS on steroids.*
