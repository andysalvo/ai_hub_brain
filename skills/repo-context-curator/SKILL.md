---
name: repo-context-curator
description: Refresh project context for this repository by scanning FOR_AGENTS.md, AGENTS.md, CONTRIBUTING.md, README.md, docs/*, and threads/*, then updating only the Embedded Context Snapshot and Embedded Context Changelog sections inside FOR_AGENTS.md when material changes exist.
---

# Repo Context Curator

Use this skill when you need to maintain current repository context while preserving a strict single-source model.

## Inputs
- `FOR_AGENTS.md`
- `AGENTS.md`
- `CONTRIBUTING.md`
- `README.md`
- `threads/*.md`
- `docs/ideas/*.md`
- `docs/specs/*.md`
- `docs/decisions/*.md`

## Required Outputs
- Update only `FOR_AGENTS.md` sections:
  - `## Embedded Context Snapshot`
  - `## Embedded Context Changelog`
- Keep all other sections unchanged unless explicitly requested by a human maintainer.

## Workflow
1. Read source documents and thread/artifact files.
2. Identify material deltas since the last context snapshot.
3. If no material deltas:
   - Do not rewrite `FOR_AGENTS.md`.
   - Return a clear "no material change" status summary.
4. If material deltas exist:
   - Rewrite only the two embedded context sections.
   - Keep statements factual and avoid speculation.
   - Keep text concise for upload-first workflows.
   - Append one dated changelog entry inside `## Embedded Context Changelog`.

## Material Change Rules
Treat the following as material:
- New project facts, decisions, constraints, or workflow rules.
- New promoted artifacts in `docs/ideas`, `docs/specs`, or `docs/decisions`.
- New active thread directions that affect next actions.

Treat the following as non-material:
- Wording-only edits that do not change meaning.
- Cosmetic formatting changes.
- Reordering equivalent bullets with unchanged content.

## Guardrails
- Preserve the canonical project fact unless explicitly superseded by repository updates.
- Do not imply official Penn State sponsorship unless a source file states it.
- Never include secrets or sensitive data.
- Do not create or update separate context files outside `FOR_AGENTS.md`.
- Avoid large rewrites that erase historical continuity.
