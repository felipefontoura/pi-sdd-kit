---
name: sdd-idea
description: 'Conversational SDD skill for exploring raw product or feature ideas before planning. Use when the user wants to brainstorm, clarify, compare directions, or convert an early idea into a plan or requirements, even without an explicit command. Do not use for implementation or technical task execution.'
---

# SDD Idea

Explore an idea before turning it into a plan, requirements, or code.

## Purpose

Use this skill to create cognitive clarity before formal planning. IDEA is divergent: it explores the problem space, users, alternatives, value signals, constraints, risks, and possible directions. It does not commit the user to a roadmap or implementation.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` only when writing the final artifact.
   - Use package-level `templates/idea.md` as the user-facing template when available.
   - Load relevant `.ai/steering/*.md` files when present, especially product, principles, or domain context.
   - If `.ai/strategy/handoff/strategy-brief.md` exists, read it as optional upstream context; use it to seed exploration, but do not require it or treat it as approved SDD scope.

2. Establish the workspace.
   - Use `.ai/sdd/ideas/` for idea artifacts.
   - Create `.ai/sdd/ideas/` if it does not exist.
   - If `.ai/sdd/PLAN.md` or `.ai/sdd/specs/` exists, briefly inspect them to avoid duplicating an existing direction.
   - If using the optional strategy handoff, record it as a source path in the idea artifact.

3. Explore the raw idea.
   - Ask one question at a time.
   - Prefer multiple-choice questions when useful.
   - Cover at least: problem, target users, current alternatives, desired outcome, constraints, success signals, and risk.
   - Do not ask implementation-first questions unless the idea is explicitly technical.

4. Present directions.
   - Propose 2-3 possible directions.
   - Include trade-offs: speed, complexity, user value, and risk.
   - Recommend one direction, but preserve dissenting alternatives.
   - Ask the user whether to continue exploring, create a PLAN, create REQUIREMENTS directly, or archive the idea.

5. Write the idea artifact only after the user confirms the direction.
   - Determine the next numeric prefix in `.ai/sdd/ideas/`.
   - Use `NNN-kebab-name.md`.
   - Fill the Idea Template from `../_shared/references/templates.md`.
   - Use clear technical product language; avoid implementation commitments.

6. Update optional index.
   - If `.ai/sdd/INDEX.md` exists, add or update an entry for the idea.
   - Do not invent statuses; use `idea:captured` for saved ideas.

## Output

- `.ai/sdd/ideas/NNN-name.md`
- Optional recommendation for next command:
  - create `.ai/sdd/PLAN.md` for medium projects
  - create `.ai/sdd/specs/NNN-feature/requirements.md` directly for small features

## Critical Rules

- Do not create requirements, design, tasks, or code inside this skill unless the user explicitly changes the requested phase.
- Do not collapse exploration into a plan too early.
- Do not treat IDEA as approved scope; it is a thinking artifact.
- Do not proceed without explicit user confirmation before writing the final idea file.
- Do not silently promote or infer feature-spec approval states from IDEA artifacts.
