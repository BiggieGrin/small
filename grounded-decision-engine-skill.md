---
name: grounded-decision-engine
description: Force knowledge-driven reasoning during active development. Before any coding decision, refactor, or system change, query the Obsidian vault, evaluate project invariants, align with documented context, and explicitly cite source notes. Use during coding, refactoring, or architectural work when an Obsidian vault is available.
---

# Knowledge-Grounded Decision Engine

Force the agent to base all coding choices, system designs, and file modifications on existing project context inside the Obsidian vault. Ensure that past architectural decisions, project conventions, and documented constraints directly guide every technical turn.

## 1. Mandatory Knowledge Retrieval (Pre-Execution Phase)

Before generating code, planning a refactor, or editing files:

1. **Query Vault Index** — Read `00_Index.md` and query the connected Obsidian vault (via MCP or local files) to pull relevant context notes.
2. **Identify Relevant Guidelines & Architecture**
   - Check `Architecture/` notes for data flows, module responsibilities, and system constraints.
   - Check `Guidelines/` notes for coding conventions, error handling standards, and tech stack constraints.
3. **Check Historical Decision Logs**
   - Search `Decisions/` notes to see if a similar problem, refactor, or architectural pattern was previously evaluated or logged.

## 2. Context Invariant & Evaluation Check

Before executing tool calls or outputting final code, perform an internal alignment check and document the grounding in your output:

- **Constraint Alignment** — Verify that the proposed solution adheres to all rules in `Guidelines/` and structural patterns in `Architecture/`.
- **Historical Consistency** — Verify whether the planned implementation conflicts with any previous decision logged in `Decisions/`.
- **Explicit Citing** — State the specific Obsidian notes governing this task (e.g. "Basing implementation on constraints in [[Architecture/Overview]] and [[Guidelines/Coding_Standards]]").

## 3. Conflict Resolution & Branching Rules

If the proposed solution conflicts with an existing vault note or past decision log:

1. **Do Not Silently Overwrite** — Do not ignore documented conventions or past decisions.
2. **Evaluate Divergence**
   - **Path A (Alignment)** — Modify the technical approach to match documented project standards.
   - **Path B (Evolving Architecture)** — If the user's new request explicitly overrides past architecture, highlight the conflict explicitly:
     > Conflict detected with [[Decisions/DEC-YYYYMMDD-topic]]. Proceeding with user request. A new decision note will be created to update this record.

## 4. Grounded Action Protocol

Execute the task while strictly maintaining the documented constraints. Once code or configuration changes are complete:

1. Invoke the `maintain-decision-log` skill to log the execution trajectory.
2. Link the generated decision note directly back to the architectural notes (`[[Architecture/...]]`) that influenced the choice.
