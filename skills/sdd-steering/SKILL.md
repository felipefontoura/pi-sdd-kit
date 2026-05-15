---
name: sdd-steering
description: 'Creates or updates reusable project steering documents in .ai/steering for product context, tech stack, conventions, and domain-specific guidance. Use when shared AI context needs to be established or corrected, but confirm before saving durable/global steering changes. Do not use for feature-level requirements or implementation.'
---

# AI Steering

Create or update reusable project context in `.ai/steering/`.

## Purpose

Steering documents capture stable project guidance that many skills can reuse. They are not SDD feature artifacts; they describe the broader product, stack, principles, conventions, and domain rules that should guide IDEA, PLAN, PRD, SPEC, TASKS, EXEC, REVIEW, and other AI workflows. Because steering is durable project-wide context, draft freely but confirm before saving or changing global guidance.

## Workflow

1. Load references.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` when drafting artifacts.
   - Use package-level `templates/steering-*.md` files as user-facing examples when available.

2. Establish the steering workspace.
   - Use `.ai/steering/`.
   - Create `.ai/steering/` if it does not exist.
   - Read existing `.ai/steering/*.md` before changing them.
   - Briefly inspect project README, package files, docs, and source tree when useful.

3. Determine which steering docs are needed.
   - `product.md` for product vision, users, value, boundaries, success metrics, glossary.
   - `tech-stack.md` for runtime, frameworks, libraries, infrastructure, verification commands, constraints.
   - `conventions.md` for code style, architecture patterns, naming, testing, accessibility/security, workflow.
   - `principles.md` for project principles, MUST/SHOULD rules, decision rules, review expectations, and governance-like guidance.
   - Domain-specific docs such as `lp.md`, `payments.md`, `brand.md`, or `content.md` when the user wants reusable guidance for a specific workflow.

4. Clarify missing context.
   - Ask one question at a time.
   - Prefer multiple-choice questions when useful.
   - Do not over-interrogate; use existing project evidence when reliable.
   - Mark uncertain items as Open Questions rather than inventing durable rules.

5. Draft or update steering.
   - Use the Steering Templates from `../_shared/references/templates.md`.
   - Keep docs concise and stable.
   - Separate facts from preferences and open questions.
   - For `principles.md`, prefer practical `MUST`, `SHOULD`, and `MAY` rules over legalistic language such as "constitution".
   - For `principles.md`, help non-technical users choose principles with guided options and examples instead of asking broad governance questions.
   - Do not duplicate feature-level requirements from `.ai/sdd/specs/`.

6. Review with the user.
   - Present the proposed steering content or diff summary.
   - Ask for explicit approval before writing or overwriting durable steering docs.
   - If updating existing files, preserve useful existing content.

7. Save.
   - Save approved docs under `.ai/steering/`.
   - Recommend next SDD action if relevant, such as `/skill:sdd-idea`, `/skill:sdd-plan`, or `/skill:sdd-prd`.

## Output

Common outputs:

- `.ai/steering/product.md`
- `.ai/steering/tech-stack.md`
- `.ai/steering/conventions.md`
- `.ai/steering/principles.md`
- Optional `.ai/steering/<domain>.md`

## Quality Bar

- Steering must be reusable across features and skills.
- Steering must be concise enough to remain useful as context.
- Stack and verification commands should be based on actual project files when possible.
- Conventions should describe existing patterns, not aspirational rewrites, unless the user explicitly approves a new convention.
- Principles should be stable, actionable, and easy to evaluate during PRD, SPEC, TASKS, EXEC, and REVIEW.
- Open Questions should remain visible instead of being guessed.

## Critical Rules

- Do not write feature-specific requirements, design, tasks, or implementation code in this skill.
- Do not overwrite existing steering without reviewing it first.
- Do not invent project facts that are not provided by the user or repository evidence.
- Do not treat steering as higher priority than explicit user instructions or approved SDD artifacts; surface conflicts and ask.
