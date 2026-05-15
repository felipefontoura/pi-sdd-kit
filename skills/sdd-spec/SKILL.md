---
name: sdd-spec
description: 'Creates SDD design.md technical specifications from approved requirements. Use for HOW decisions: architecture, components, data/state, APIs, flows, edge cases, technical decisions, risks, and implementation FAQ. Do not use for requirements creation, task breakdown, or coding.'
---

# SDD Spec / Design

Translate approved requirements into a practical technical design.

## Purpose

Design defines how the approved requirements will be implemented. It should be detailed enough for an implementer to work without guessing, but lightweight enough for small and medium projects.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` when drafting the artifact.
   - Use package-level `templates/design.md` as the user-facing template when available.
   - Load relevant `.ai/steering/*.md` files when present, especially `product.md`, `tech-stack.md`, and `conventions.md`.

2. Locate the feature.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - Read `.status`.
   - Block if status is not `requirements:approved`, unless the user explicitly asks for a non-binding draft spike.
   - Read `requirements.md` completely.

3. Explore project context.
   - Inspect existing code, conventions, routing, components, services, tests, and build tooling relevant to the feature.
   - Prefer existing patterns over new abstractions.
   - Identify likely files and integration points, but do not generate tasks yet.

4. Clarify technical choices.
   - Ask one question at a time when decisions require user input.
   - Present 2-3 approaches for meaningful trade-offs.
   - Cover component/module boundaries, state/data ownership, API/integration boundaries, testing approach, and operational risks where relevant.

5. Draft design.
   - Use the Design Template from `../_shared/references/templates.md`.
   - Scale detail to project size:
     - small frontend feature: component structure, data/state, user flows, edge cases, decisions, tests
     - medium project: include API, persistence, auth, concurrency, observability, migration, or deployment only when relevant
   - Include a Requirements Mapping table linking each Must Have requirement to design sections or decisions.
   - Include technical decisions with trade-offs and alternatives.
   - Include rich technical sections when relevant: data model, API/integration contract, security/permissions/privacy, accessibility, observability, migration/rollout, and verification strategy.
   - Include an Implementation FAQ for ambiguity-prone points.
   - Add or update `decisions.md` only when a decision should survive beyond this feature or has significant trade-offs.

6. Review with the user.
   - Present the complete draft.
   - Ask for explicit approval or requested changes.
   - Revise until approved.

7. Save draft and gate.
   - Save draft design to `.ai/sdd/specs/NNN-feature-name/design.md` with `> Status: Draft` when useful for collaboration.
   - Keep `.status` as `design:draft` until explicit approval.
   - After explicit approval, update the artifact status to approved and set `.status` to `design:approved`.

## Output

- `.ai/sdd/specs/NNN-feature-name/design.md`
- Optional `.ai/sdd/specs/NNN-feature-name/decisions.md`
- Updated `.status`

## Quality Bar

- Every Must Have requirement maps to a technical approach in the Requirements Mapping table.
- Design must prefer existing project patterns.
- Technical decisions must name trade-offs.
- Edge cases from requirements must have expected behavior.
- Do not over-design: avoid new layers, services, or abstractions unless justified.

## Critical Rules

- Do not create `tasks.md` in this skill.
- Do not write implementation code in this skill.
- Do not silently change requirements; if the design reveals a requirements problem, stop and ask whether to update `requirements.md`.
- Do not mark design approved without explicit user approval.
- Draft designs may be saved, but they do not authorize task execution or implementation.
