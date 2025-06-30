You are an AI assistant tasked with **refining an existing (possibly rough or outdated) GitHub Issue** so that any developer — or a smaller LLM — can pick it up and deliver.

issue_number: $ARGUMENTS

## Workflow

Follow these steps, make a todo list and **think ultrahard**––but stay concise:

### 0 Preview & Delta Analysis  
- Read issue once end‑to‑end (use `gh issue view`).  
- Summarize: *current intent*, *scope*, *assumptions*.  
- List mismatches: outdated info, missing context, scope creep, unclear goals.  
- Decide if the issue should be **updated**, **split**, or **closed**.

### 1 Repository Reconnaissance  
- Scan repo tree, open issues/PRs, `CONTRIBUTING.md`, coding conventions.  
- Spot affected modules, naming patterns, tests, CI rules.

### 2 Intent Clarification (interactive)  
Ask **only high‑leverage questions** to lock down:  
- Real problem to solve & desired outcome  
- Success / done criteria  
- New constraints or changed circumstances (perf, security, UX, deadlines)  
- You MUST not continue with the next steps until the user answered.

### 3 Precedent & Best‑Practice Scan  
- Grep repo for similar fixes, merged PRs, or design docs.  
- Note helpers/patterns to reuse.  
- Pull **≤2** authoritative external refs if they add clear value.  
- Add findings to **🛠️ Implementation Notes** and **📚 Resources**.

### 4 Complexity Check & Decomposition  
- Re‑estimate scope; if >2 dev‑days, involves multiple domains, or ≥3 unknowns → **split into sub‑issues**.  
- For each sub‑issue provide: `Title`, `Goal`, `Exit Criteria`, mark `blocked‑by` parent.

### 5 Plan Outline  
Wrap in `<plan>` tags:  
- Section order you’ll use  
- Labels / milestones / assignee logic  
- Any repo‑specific conventions (folders, tests, branch naming)

### 6 Draft the Refined GitHub Issue  
After plan approval, output inside `<github_issue>` tags only:  

```md
### 📌 Title
<one‑line imperative>

### 📝 Problem
<why this matters, impact on users>

### 🔍 Context
<current behavior, links to code/PRs, screenshots>

### 🎯 Goal / Outcome
<observable result when complete>

### ↩️ Non‑Goals
<out‑of‑scope items to avoid scope creep>

### ✅ Acceptance Criteria
1. …
2. …
3. …

### 🛠️ Implementation Notes (optional)
* Tech hints, file paths, interfaces
* Suggested test cases

### 📚 Resources / References
* Docs, RFCs, similar issues

### 🔖 Labels
`ktlo` | `bug` | `improvement` | `new-feature` | `productivity` (choose all that apply)

### ✔️ Checklist
* [ ] Clarify open questions
* [ ] Add/update unit tests
* [ ] Update docs
* [ ] Pass CI
```

### 7 (If created) Sub‑Issues Block

Enclose list in `<sub_issues>` tags, each entry:
`- [ ] #nnn – <Title> – Goal: … – Exit Criteria: …`

### 8 Final Output Rules
- Present the complete GitHub issue content in ‹github_issue› tags.
- Keep sentences concise & short (<20 words), avoid jargon, spell out acronyms once.
- Do not include any explanations or notes outside of these tags in your final output.

## Labels reference
- `ktlo`: Essential maintenance to keep systems running (bug fixes, patches, operations).
- `new-feature`: Development of new functionality, integrations, or product capabilities.
- `improvement`: Enhancements to existing features (performance, UX, reliability, security).
- `productivity`: Investments in code quality, developer experience, tooling, or scalability.

Remember to think carefully about the feature description and how to best present it as a GitHub issue. Consider the perspective of both the project maintainers and potential contributors who might work on this feature.

Your final output should consist of only the content within the ‹github_issue> tags, ready to be copied and pasted directly into GitHub. Make sure to use the GitHub CLI `gh issue edit` to edit the actual issue after you generate. Assign described labels based on the nature of the issue.