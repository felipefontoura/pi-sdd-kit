---
name: sdd-plan
description: 'Cognitive SDD skill for creating or updating optional PLAN.md from captured ideas or project goals. Use when the conversation calls for roadmap, personas, feature mapping, phases, dependencies, and open decisions before requirements, even without an explicit command. Do not use for feature-level requirements or coding.'
---

# SDD Plan

Convert explored ideas into a product or project plan.

## Purpose

PLAN is the bridge between open-ended IDEA exploration and feature-level REQUIREMENTS. It is optional for very small work and recommended for medium projects with multiple features, modules, or phases.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` when drafting the artifact.
   - Use package-level `templates/plan.md` as the user-facing template when available.
   - Load relevant `.ai/steering/*.md` files when present, especially `product.md`, `tech-stack.md`, `conventions.md`, and `principles.md`.
   - If `.ai/strategy/handoff/strategy-brief.md` exists, read it as optional upstream context; use it to reduce rediscovery, but do not require it or bypass plan approval.

2. Gather context.
   - Read `.ai/sdd/ideas/*.md` relevant to the requested project or feature set.
   - Read existing `.ai/sdd/PLAN.md` when updating.
   - Inspect `.ai/sdd/specs/` if feature specs already exist.
   - Briefly inspect project README or product docs when available.
   - When a strategy handoff is used, reflect it in plan source/context notes and call out any unresolved readiness gaps.

3. Clarify planning scope.
   - Ask one question at a time.
   - Cover vision, personas, MVP boundary, feature map, dependencies, constraints, and open decisions.
   - Keep this at project/roadmap level; do not design implementation details.

4. Draft the plan.
   - Use the Plan Template from `../_shared/references/templates.md`.
   - Organize features by MoSCoW phases:
     - Phase 1 — MVP / Must Have
     - Phase 2 — Essentials / Should Have
     - Phase 3 — Nice to Have / Could Have
   - Include feature IDs such as `F01`, `F02`, `F03`.
   - Include dependencies only when they affect sequencing.
   - Include Open Decisions for unresolved strategy or scope questions.

5. Review with the user.
   - Present the complete draft.
   - Ask for explicit approval or requested changes.
   - Revise until approved.

6. Save draft and guide next step.
   - Save drafts to `.ai/sdd/PLAN.md` with `> Status: Draft` and `.status` as `plan:draft` when useful for collaboration.
   - After explicit approval, update `.ai/sdd/PLAN.md` to approved and set `.status` to `plan:approved` if a project-level `.status` is used.
   - Create `.ai/sdd/INDEX.md` if useful for tracking feature specs.
   - Recommend creating `requirements.md` for the first Phase 1 feature.

## Output

- `.ai/sdd/PLAN.md`
- Optional `.ai/sdd/INDEX.md`

## Quality Bar

- The plan must make MVP boundaries clear.
- Feature IDs must be specific enough to become spec directories.
- Dependencies must reflect real sequencing constraints, not arbitrary order.
- Open Decisions must capture unresolved ambiguity instead of hiding it.

## Critical Rules

- Do not write code in this skill.
- Do not create feature-level requirements unless the user explicitly changes phase.
- Do not over-plan small one-screen work; recommend going directly to PRD when PLAN would be wasteful.
- Do not mark a plan approved without explicit user approval.
- Draft plans may be saved, but they do not authorize feature implementation.
- Do not silently change feature-spec `.status` values from this skill unless the user explicitly requested a project-level plan status update.
