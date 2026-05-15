---
name: sdd-status
description: 'Summarizes the current SDD workspace state from .ai/sdd and recommends the next safe action. Use to inspect ideas, plan, specs, statuses, incomplete tasks, blocked gates, and review readiness. Do not use to create specs or implement code.'
---

# SDD Status

Inspect the SDD workspace and report current progress, blockers, and next actions.

## Purpose

STATUS gives operational visibility across `.ai/sdd/` without changing artifacts. It helps the user understand what exists, what is approved, what is still draft, what is blocked, and what the next safe SDD step should be.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Use package-level `templates/sdd-index.md` as the dashboard reference when useful.
   - Load relevant `.ai/steering/*.md` files only if they help explain project context; do not summarize steering unless useful.

2. Inspect the workspace.
   - Check whether `.ai/sdd/` exists.
   - Check `.ai/sdd/INDEX.md` if present.
   - Check `.ai/sdd/PLAN.md` if present.
   - List `.ai/sdd/ideas/*.md` if present.
   - List `.ai/sdd/specs/*/` directories.
   - For each spec directory, read `.status` when present.
   - For each spec directory, note presence of `requirements.md`, `design.md`, `tasks.md`, `review.md`, and `decisions.md`.

3. Assess gates.
   - Identify specs that are ready for PRD, SPEC, TASKS, EXEC, or REVIEW.
   - Identify specs blocked by missing artifacts, draft statuses, or missing approvals.
   - Identify implementation specs with incomplete tasks when `tasks.md` exists.
   - Identify specs whose `.status` conflicts with existing artifacts.

4. Produce a concise dashboard.
   - Group by Ideas, Plan, Specs, In Progress, Review Ready, and Blocked.
   - Include exact paths for important artifacts.
   - Include the current `.status` value for each spec.
   - Recommend one or more next commands such as `/skill:sdd-prd`, `/skill:sdd-spec`, `/skill:sdd-tasks`, `/skill:sdd-exec`, or `/skill:sdd-review`.

5. Do not modify files.
   - STATUS is read-only.
   - If an index or status appears stale, recommend an update instead of editing it.

## Output Format

```text
SDD STATUS

Workspace: .ai/sdd
Steering: .ai/steering present/missing

Plan:
- [missing/draft/approved] .ai/sdd/PLAN.md

Ideas:
- 001-name — idea:captured — .ai/sdd/ideas/001-name.md

Specs:
- 001-feature — requirements:approved
  Artifacts: requirements.md yes, design.md no, tasks.md no, review.md no
  Next: /skill:sdd-spec

Blocked / Attention:
- [Path] [problem]

Recommended next action:
- [Specific next step]
```

## Quality Bar

- Be accurate and path-specific.
- Prefer short dashboards over long commentary.
- Do not infer approvals from file existence; use `.status` and artifact headers when available.
- Flag missing or inconsistent status instead of silently normalizing it.

## Critical Rules

- Do not create, edit, or delete files in this skill.
- Do not approve drafts.
- Do not implement code.
- Do not run expensive verification commands unless the user explicitly asks for a health check.
