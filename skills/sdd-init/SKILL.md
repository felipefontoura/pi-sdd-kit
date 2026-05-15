---
name: sdd-init
description: 'Explicit command-style skill for initializing or adopting SDD in a project by creating or preparing .ai/, .ai/steering/, and .ai/sdd/. Use only when the user explicitly asks to initialize, set up, adopt, or bootstrap SDD. Do not auto-load for general planning, feature specs, status checks, or implementation.'
---

# AI / SDD Init

Initialize a project workspace for AI-assisted Spec-Driven Development.

## Purpose

INIT prepares the project for consistent AI work. It creates the shared `.ai/` structure, captures minimal reusable steering context, initializes SDD tracking, and recommends the next safe step. Because this changes project structure, use it only after an explicit user request to initialize, set up, adopt, or bootstrap SDD.

## Workflow

1. Load references.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` when creating starter files.
   - Use package-level `templates/` files as user-facing examples when available.

2. Inspect the project.
   - Check whether `.ai/`, `.ai/steering/`, `.ai/sdd/`, and `.ai/sdd/handoff/` already exist.
   - Read existing `.ai/steering/*.md`, `.ai/sdd/INDEX.md`, and `.ai/sdd/PLAN.md` if present.
   - If `.ai/strategy/handoff/strategy-brief.md` exists, note it as optional upstream context for future `/skill:sdd-idea`, `/skill:sdd-plan`, or `/skill:sdd-prd` work.
   - Briefly inspect README, package files, docs, source tree, and verification scripts when available.
   - Do not overwrite existing AI artifacts without explicit approval.

3. Clarify initialization scope.
   - Ask whether the user wants:
     - minimal setup: directories + index + workflow guide only
     - steering setup: product, tech stack, conventions, optional principles
     - SDD setup: index + workflow guide + optional first IDEA or PLAN
     - domain setup: extra steering doc such as `lp.md`
   - Ask one question at a time.
   - Prefer inferred project facts from files, but confirm uncertain durable rules.

4. Draft starter artifacts.
   - Use `.ai/steering/` for reusable context:
     - `product.md`
     - `tech-stack.md`
     - `conventions.md`
     - optional `principles.md`
     - optional `<domain>.md`
   - Use `.ai/sdd/` for SDD artifacts:
     - `INDEX.md`
     - optional `WORKFLOW.md` copied or adapted from `templates/sdd-workflow.md`
     - `handoff/` directory for future `.ai/sdd/handoff/sdd-brief.md`
     - optional `PLAN.md` as draft only if the user wants planning now
   - Keep generated starter docs concise and mark uncertain items as Open Questions.

5. Review with the user.
   - Present the proposed files and short content summary.
   - Ask for explicit approval before writing files.
   - If files already exist, show what will be preserved or changed.

6. Save approved initialization.
   - Create directories and files only after approval.
   - Never mark PLAN or feature artifacts approved during init.
   - Recommend next command:
     - `/skill:sdd-idea` for exploration
     - `/skill:sdd-plan` for roadmap planning
     - `/skill:sdd-prd` for a known small feature
     - `/skill:sdd-steering` for more reusable context

## Suggested Initial Structure

```text
.ai/
  steering/
    product.md
    tech-stack.md
    conventions.md
    principles.md        # optional
  sdd/
    INDEX.md
    WORKFLOW.md          # optional guide
    handoff/
```

## Starter INDEX.md

```markdown
# SDD Index

## Upstream Handoffs

- `.ai/strategy/handoff/strategy-brief.md`: missing or available

## Plan

- `.ai/sdd/PLAN.md`: missing

## Ideas

| ID | Name | Status | Path |
|----|------|--------|------|

## Feature Workspace

> Numbering source: actual directories under `.ai/sdd/specs/`, not this index.

| Field | Value | Notes |
|-------|-------|-------|
| Next Feature ID | 001 | Recompute from filesystem before creating a new spec |
| Numbering Issues | none | duplicate prefix / invalid status / non-canonical directory |

## Specs

| ID | Feature | Status | Requirements | Design | Tasks | Review |
|----|---------|--------|--------------|--------|-------|--------|

## Handoff

- `.ai/sdd/handoff/sdd-brief.md`: generated after approved tasks or completed review

## Next Actions

- [ ] Capture first idea with `/skill:sdd-idea`
- [ ] Or create a plan with `/skill:sdd-plan`
- [ ] Or create requirements for a known feature with `/skill:sdd-prd`
```

## Output

Common outputs:

- `.ai/steering/product.md`
- `.ai/steering/tech-stack.md`
- `.ai/steering/conventions.md`
- Optional `.ai/steering/principles.md`
- `.ai/sdd/INDEX.md`
- Optional `.ai/sdd/WORKFLOW.md`
- `.ai/sdd/handoff/` directory
- Optional `.ai/sdd/PLAN.md` draft
- Optional `.ai/steering/<domain>.md`

## Quality Bar

- Initialization must be safe and idempotent.
- Existing artifacts must be preserved unless the user approves changes.
- Generated files must be short enough to be useful as persistent context.
- Unknown facts must become Open Questions, not invented rules.
- The final response must list created/updated files and recommended next step.

## Critical Rules

- Do not create feature-level `requirements.md`, `design.md`, `tasks.md`, or code in this skill.
- Do not mark any draft as approved.
- Do not overwrite existing `.ai/` content without explicit approval.
- Do not ask many setup questions at once; initialize progressively.
