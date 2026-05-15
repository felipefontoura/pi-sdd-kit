# Project Principles

> Status: Active
> Last Updated: YYYY-MM-DD

## Purpose

[Describe what these principles govern and when AI agents or humans should use them. Keep this short and practical.]

## How to Use These Principles

- Use these principles when creating or reviewing PRD, SPEC, TASKS, EXEC, and REVIEW artifacts.
- Treat `MUST` rules as non-negotiable unless the user explicitly approves a change.
- Treat `SHOULD` rules as strong defaults that may be bypassed with a reason.
- Treat `MAY` rules as allowed options, not requirements.
- If a principle conflicts with an approved SDD artifact, stop and ask which source should be updated.

## Principles

### P-001: [Principle name]

**Level:** MUST  
**Rule:** [Clear rule that can be evaluated.]  
**Reason:** [Why this principle matters.]  
**Applies to:** PRD, SPEC, TASKS, EXEC, REVIEW

**Examples:**

- Good: [Concrete example of following the rule]
- Avoid: [Concrete example of violating the rule]

### P-002: [Principle name]

**Level:** SHOULD  
**Rule:** [Clear recommendation or default behavior.]  
**Reason:** [Why this is the preferred default.]  
**Applies to:** SPEC, TASKS, EXEC

**Examples:**

- Good: [Concrete example]
- Acceptable exception: [When bypassing this principle is reasonable]

### P-003: [Principle name]

**Level:** MAY  
**Rule:** [Allowed option or flexible practice.]  
**Reason:** [Why this option exists.]  
**Applies to:** [Relevant phases]

## Decision Rules

When principles conflict, use this order:

1. Safety, privacy, and legal/compliance requirements take priority.
2. Approved product requirements take priority over implementation preferences.
3. Simpler solutions are preferred unless they fail an approved requirement.
4. If the trade-off is unclear, ask the user before changing direction.

## Review Expectations

Before implementation:

- [ ] Requirements respect all relevant `MUST` principles.
- [ ] Design documents justify any exception to `SHOULD` principles.
- [ ] Tasks include verification for principle-related requirements.

During review:

- [ ] Implementation follows relevant `MUST` principles.
- [ ] Exceptions are documented and approved.
- [ ] Verification evidence supports principle-sensitive claims.

## Change Policy

- Changes to `MUST` principles require explicit user approval.
- Changed principles do not silently rewrite approved SDD artifacts.
- If a principle conflicts with approved requirements, design, or tasks, ask whether to update the principle or the approved artifact.
- Record important principle changes with date and reason.

## Open Questions

- [Question about project principles that still needs a decision]
