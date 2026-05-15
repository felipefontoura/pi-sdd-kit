---
name: sdd-prd
description: 'Creates or updates SDD requirements.md artifacts from an approved idea, plan, or feature request. Use for defining WHAT and WHY: user stories, acceptance criteria, EARS functional requirements, non-functional requirements, and out-of-scope boundaries. Do not use for technical design or coding.'
---

# SDD PRD / Requirements

Create a practical `requirements.md` artifact for a small or medium project feature.

## Purpose

Requirements define the product contract. They explain what the feature must do, who it serves, why it matters, and how the team will know it is done. They must not prescribe implementation details.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` when drafting the artifact.
   - Use package-level `templates/requirements.md` as the user-facing template when available.
   - Load relevant `.ai/steering/*.md` files when present, especially `product.md`, `tech-stack.md`, and `conventions.md`.

2. Locate or create the feature spec directory.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - If the user names an existing feature, use its directory.
   - If creating a new feature, determine the next numeric prefix under `.ai/sdd/specs/`.
   - Create `.status` with `requirements:draft` when starting a new requirements artifact.

3. Gather context.
   - Read relevant `.ai/sdd/ideas/*.md` if the feature came from IDEA.
   - Read `.ai/sdd/PLAN.md` if it exists.
   - Read existing `requirements.md` when updating.
   - Inspect nearby project files only enough to understand product context and naming; do not design implementation yet.

4. Clarify scope.
   - Ask one question at a time.
   - Cover: target users, main flows, edge cases, acceptance criteria, non-functional needs, and out-of-scope boundaries.
   - Keep questions focused on WHAT and WHY.
   - Avoid database, framework, API, or component-structure questions.

5. Draft requirements.
   - Use the Requirements Template from `../_shared/references/templates.md`.
   - Include user stories with acceptance criteria.
   - Write functional requirements using EARS where possible.
   - Classify functional requirements with MoSCoW: Must Have, Should Have, Could Have, Won't Have.
   - Include non-functional requirements only when they matter: usability, performance, accessibility, security, reliability.
   - Include explicit Out of Scope.
   - Put unresolved items in Open Questions rather than guessing.

6. Review with the user.
   - Present the complete draft.
   - Ask for explicit approval or requested changes.
   - If changes are requested, revise and present again.

7. Save draft and gate.
   - Save draft requirements to `.ai/sdd/specs/NNN-feature-name/requirements.md` with `> Status: Draft` when useful for collaboration.
   - Keep `.status` as `requirements:draft` until explicit approval.
   - After explicit approval, update the artifact status to approved and set `.status` to `requirements:approved`.

## Output

- `.ai/sdd/specs/NNN-feature-name/requirements.md`
- `.ai/sdd/specs/NNN-feature-name/.status`

## Quality Bar

- Every Must Have requirement must be testable.
- Acceptance criteria must describe observable behavior.
- Out of Scope must prevent likely scope creep.
- Requirements must not contain implementation decisions.

## Critical Rules

- Do not create `design.md` in this skill.
- Do not write code in this skill.
- Do not proceed without explicit user approval before marking requirements approved.
- Draft requirements may be saved, but they do not authorize design as an approved gate.
- If the user asks for a very small change, keep the artifact concise but still preserve the gate.
