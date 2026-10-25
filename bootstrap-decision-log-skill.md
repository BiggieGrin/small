---
name: bootstrap-decision-log
description: Run once per project to scan a codebase, extract architecture, modules, dependencies, and business logic, then generate a structured Obsidian Knowledge Base with Maps of Content and wikilinks. Use when bootstrapping a new project vault or initializing documentation for an existing repository.
---

# Bootstrap Obsidian Knowledge Base

Scan an existing codebase or project folder, analyze its structure and architectural patterns, and generate an initial Obsidian Knowledge Base inside the designated vault directory.

## 1. Initialization & Discovery

1. Ask the user for:
   - The root path of the existing project codebase
   - The target directory in their Obsidian vault (e.g. `ObsidianVault/Projects/ProjectName/`)
2. Scan the target repository:
   - Read key metadata files — `README.md`, `package.json`, `pyproject.toml`, `Cargo.toml`, `Dockerfile`, `go.mod`, `composer.json`, etc.
   - Inspect top-level file trees and folder hierarchy
   - Identify key components, entry points, configuration layers, and data models

## 2. Obsidian Vault Generation Structure

Create the following directory structure inside the specified Obsidian project location:

```
ObsidianVault/Projects/[ProjectName]/
├── 00_Index.md              # Main Map of Content (MOC)
├── Architecture/            # System design & component relations
│   ├── Overview.md          # High-level architecture summary
│   └── Data_Flow.md         # Pipeline & data movement specs
├── Modules/                 # Notes for major codebase components
├── Decisions/               # Folder dedicated to historical reasoning logs
└── Guidelines/              # Code standards, conventions, and constraints
```

## 3. Note Creation Guidelines

### Main Map of Content (`00_Index.md`)

- Serve as the entry point using Obsidian wikilinks (`[[Note Name]]`)
- Categorize links into Architecture, Key Modules, Setup Guides, and Decision History

### Architecture Notes (`Architecture/Overview.md`)

- Document system components, tech stack choices, external API dependencies, and data structures

### Module Notes (`Modules/[ModuleName].md`)

- For each primary component, document its purpose, key files, key classes/functions, and dependencies
- Use bidirectional links back to `[[00_Index]]` and related modules

### Standard Markdown & Metadata

Add this YAML frontmatter to every note:

```yaml
---
type: project_knowledge
project: "[ProjectName]"
created: ""
status: active
---
```

Use clean Markdown tags (e.g. `#architecture`, `#module`, `#index`).

## 4. Completion Report

Once created, output a summary listing:

- Total notes generated
- Key components mapped
- Next steps instructing the user to activate the `maintain-decision-log` skill for continuous development during coding sessions
