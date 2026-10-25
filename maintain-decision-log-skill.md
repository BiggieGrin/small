---
name: maintain-decision-log
description: Maintain double-entry truth with an Obsidian vault during coding. Generates decision trajectory notes in Decisions/, creates bidirectional links between code changes and vault docs, and manages context pruning. Use every time you code, refactor, or make architectural choices when an Obsidian vault is available.
---

# Continuous Decision Log & Knowledge Maintainer

Execute coding, refactoring, and architectural tasks while preserving ground truth in Obsidian. Automatically log reasoning trajectories into dedicated decision notes and update codebase documentation bidirectionally.

## Pre-Execution Ground Truth Verification

Before editing or writing code or notes:

1. Query the connected Obsidian vault (via Obsidian MCP or local files) to retrieve relevant project context, guidelines, and past decision logs.
2. Apply the Ground Truth Conflict Rule — never silently overwrite existing vault notes or technical assumptions.
   - If a code implementation introduces a breaking change or updates an architecture pattern:
     - Record the conflict explicitly in a new decision log.
     - Update the existing vault note with a clear explanation and a wikilink to the decision note.

## Decision Log Generation (Decisions/)

For any non-trivial code modification, architecture choice, or multi-step execution:

1. Create a dedicated reasoning file in the `Decisions/` directory named:
   `Decisions/DEC-YYYYMMDD-brief-topic.md`
2. Populate the file using this mandatory schema:

```yaml
type: decision_log
timestamp: ""
session_id: ""
related_notes: ["[[00_Index]]", "[[Architecture/Overview]]"]
affected_files: ["src/main.ts"]
status: executed
```

```markdown
# Decision Log: [Brief Topic Title]

## 1. Problem Context & Goal
[Explain the goal, trigger, or bug being addressed]

## 2. Reasoning Trajectory & Options Evaluated
**Chosen Approach:** [Why this implementation path was chosen]
**Rejected Alternatives:** [What options were considered and why they were discarded]
**Trade-offs & Risks:** [Performance, technical debt, or safety considerations]

## 3. Execution Summary & File Deltas
Key code or configuration changes made.
References to modified source files.
```

## Bidirectional Linking & Indexing

1. Update `00_Index.md` (or the relevant component note) by adding a wikilink `[[Decisions/DEC-YYYYMMDD-brief-topic]]` under its decision history section.
2. Add an inline code comment or PR/commit annotation referencing the decision log title so future developers can trace the code back to its reasoning note.

## Context Pruning

During long execution sessions, prune outdated intermediate context from working memory while preserving the decision log as the durable source of truth. Prefer referring back to decision notes rather than re-deriving prior reasoning.
