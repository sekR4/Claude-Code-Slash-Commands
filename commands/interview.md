---
description: Interview me about the request to gather detailed requirements for a spec document.
argument-hint: [request]
---

<request>
$ARGUMENTS
</request>

Interview me about my request using the `AskUserQuestion` tool. Ultrathink before each question.

## Interview Focus (WHAT and WHY, not HOW)
- User intent and goals
- Target users / personas
- Scope: what's in, what's explicitly out
- User workflows and interactions
- Acceptance criteria (how do we know it's done?)
- Constraints (business rules, performance, security)
- Concerns, risks, edge cases
- Dependencies on existing systems

Continue until requirements are clear, then write the spec to `.specs/{spec-name}.md`.

## Spec Template
```markdown
# Feature: [Name]

## 1. Context & Problem
Why does this exist? What pain does it solve?

## 2. Scope
### In Scope
### Out of Scope

## 3. User Stories & Acceptance Criteria
### US-001: [Title]
**As a** [role], **I want** [goal] **so that** [benefit]
**Acceptance Criteria:**
- WHEN [condition] THEN [expected behavior]

## 4. Constraints
- Business:
- Performance:
- Security:

## 5. Open Questions
```

## Exclusions
Do NOT include in the spec:
- Code or pseudocode
- Technology choices
- Architecture decisions
- Implementation details

These belong in the planning phase, not the specification.
