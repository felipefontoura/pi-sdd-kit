---
name: sdd-prd
description: 'Core cognitive SDD skill for creating or updating requirements.md from an approved idea, plan, or feature request. Use when the conversation calls for defining WHAT and WHY: user stories, acceptance criteria, EARS functional requirements, NFRs, and boundaries, even without an explicit command. Do not use for technical design or coding.'
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
   - Load relevant `.ai/steering/*.md` files when present, especially `product.md`, `tech-stack.md`, `conventions.md`, and `principles.md`.
   - If `.ai/strategy/handoff/strategy-brief.md` exists, read it as optional upstream context; use it to seed product requirements, but do not require it or let it bypass requirements approval.

2. Locate or create the feature spec directory.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - If the user names an existing feature, resolve it from actual `.ai/sdd/specs/*/` directories and artifact titles.
   - If exactly one existing feature matches, use its directory and validate its `.status` against the official status values from `sdd-practical.md`.
   - If an existing feature `.status` is missing or invalid, stop and ask the user to repair it before updating requirements.
   - If multiple existing features may match, list candidates and ask the user to choose.
   - If creating a new feature, determine the next numeric prefix from the filesystem, not from memory and not from `.ai/sdd/INDEX.md`.
   - Numbering algorithm: list directories under `.ai/sdd/specs/`, extract prefixes matching `^([0-9]+)-`, use `max + 1`, zero-pad to at least 3 digits, and preserve wider existing prefix width if present.
   - Generate a safe short slug from the feature name; ask the user if a safe slug is unclear.
   - Before creating a new spec directory, state the resolved path and continue only when it fits the user's intent.
   - Create `.status` with `requirements:draft` when starting a new requirements artifact.

3. Gather context.
   - Read relevant `.ai/sdd/ideas/*.md` if the feature came from IDEA.
   - Read `.ai/sdd/PLAN.md` if it exists.
   - Read existing `requirements.md` when updating.
   - When using the optional strategy handoff, preserve its path in the `> Source:` header or Business Context and translate strategic claims into testable requirements only after validation.
   - Inspect nearby project files only enough to understand product context and naming; do not design implementation yet.

4. Clarify scope with guided decisions.
   - Treat clarification as part of PRD, not as a separate public workflow step.
   - Ask one question at a time.
   - Cover: target users, main flows, edge cases, acceptance criteria, non-functional needs, and out-of-scope boundaries.
   - Keep questions focused on WHAT and WHY.
   - Avoid database, framework, API, or component-structure questions.
   - Prefer guided choice over open-ended questions when the user may not know how to answer technically.
   - For each important ambiguity, provide:
     - a short question;
     - why the answer matters;
     - a recommended option with a brief reason;
     - 2-4 concrete options plus `Custom` when useful;
     - the practical impact of each option.
   - Ask only questions whose answers materially change scope, UX, security/privacy, data behavior, acceptance criteria, or important NFRs.
   - Limit each pass to 3-5 high-impact questions unless the user asks to go deeper.

5. Draft requirements.
   - Use the Requirements Template from `../_shared/references/templates.md`.
   - Include user stories with acceptance criteria.
   - Write functional requirements using EARS where possible.
   - Classify functional requirements with MoSCoW: Must Have, Should Have, Could Have, Won't Have.
   - Include non-functional requirements only when they matter: usability, performance, accessibility, security, reliability.
   - Include explicit Out of Scope.
   - Use `Questions` to capture unresolved requirement uncertainty instead of guessing.
   - Use `Decisions` to record answered questions or explicit product choices.
   - When a question is answered, update the affected requirements and link the decision back to the source question.

6. Record Questions and Decisions.
   - Keep both sections inside `requirements.md`.
   - Use `Q-001`, `Q-002`, ... for questions.
   - Use `D-001`, `D-002`, ... for decisions.
   - A question may be `open` or `answered`.
   - A decision should include the decision, reason, source question when applicable, and impacted requirement IDs or sections.
   - Open critical questions block approval but do not block saving a draft.

7. Review with the user.
   - Present the complete draft.
   - Ask for explicit approval or requested changes.
   - If changes are requested, revise and present again.

8. Save draft and gate.
   - Save draft requirements to `.ai/sdd/specs/NNN-feature-name/requirements.md` with `> Status: Draft` when useful for collaboration.
   - Keep `.status` as `requirements:draft` until explicit approval.
   - Do not mark requirements approved while critical `Questions` remain open.
   - After explicit approval, update the artifact status to approved and set `.status` to `requirements:approved`.
   - Update `.ai/sdd/INDEX.md` with the spec row and current status when practical; if not updated, tell the user the index may be stale.

## Output

- `.ai/sdd/specs/NNN-feature-name/requirements.md`
- `.ai/sdd/specs/NNN-feature-name/.status`
- Updated `.ai/sdd/INDEX.md` row when practical

## Quality Bar

- Every Must Have requirement must be testable.
- Acceptance criteria must describe observable behavior.
- Out of Scope must prevent likely scope creep.
- Requirements must not contain implementation decisions.
- Questions must help non-technical users make product decisions through clear options and impacts.
- Decisions must be reflected in the affected user stories, requirements, NFRs, or scope boundaries.

## Critical Rules

- Do not create `design.md` in this skill.
- Do not guess or reuse feature IDs from memory; always determine the next ID from actual directories under `.ai/sdd/specs/`.
- Do not infer approval from artifact existence; require valid `.status` for existing specs.
- Do not write code in this skill.
- Do not proceed without explicit user approval before marking requirements approved.
- Draft requirements may be saved, but they do not authorize design as an approved gate.
- If the user asks for a very small change, keep the artifact concise but still preserve the gate.
