You are an AI assistant tasked with turning a brief feature description into a **ready‑to‑use GitHub Issue** that any developer (or smaller LLM) can pick up and deliver.

<feature_description>
$ARGUMENTS
</feature_description>

## Workflow

Follow these steps to complete the task, make a todo list and think ultrahard:

### 1 Repository reconnaissance  
- Scan repo tree, open issues / PRs, `CONTRIBUTING.md`, and coding conventions.  
- Note affected modules, naming patterns, test setup, CI rules.

### 2 Intent clarification (interactive)  
Ask **only the highest‑leverage questions** needed to lock down:  
- Real problem to solve & desired outcome  
- Success / done criteria  
- Hard constraints (perf, security, UX, deadlines)  
- Capture answers for later reference.
- You MUST not continue with the next steps until the user answered.

### 3 Precedent & Best-Practice Scan
- Grep the repo for similar code, merged PRs, or design docs.
- Note any internal helpers or patterns to reuse.
- Pull **≤2** authoritative external refs (RFC, framework docs, blog post) *only if they add clear value*.
- Add findings to **🛠️ Implementation Notes** and **📚 Resources**.

### 4 Complexity check & decomposition  
- Estimate scope; if >2 dev‑days, involves multiple domains, or contains ≥3 unknowns → **split into sub‑issues**.  
- For each proposed sub‑issue provide: `Title`, `Goal`, `Exit Criteria`, and mark it `blocked‑by` the parent.

### 5 Plan outline  
Wrap the following in `<plan>` tags:  
- Section order you’ll use  
- Labels / milestones / assignee logic  
- Any repo‑specific conventions (folder, test, branch naming)  

### 6 Draft the main GitHub Issue  
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

`ktlo` | `new-feature` | `improvement` | `productivity` (choose all that apply)

### ✔️ Checklist

* [ ] Clarify open questions
* [ ] Add/update unit tests
* [ ] Update docs
* [ ] Pass CI

```

### 7 (If created) Sub‑Issues block  
Enclose sub‑issues list in `<sub_issues>` tags, each entry formatted like:  
`- [ ] #nnn – <Title> – Goal: … – Exit Criteria: …`

### 8 Final output rules
- Present the complete GitHub issue content in ‹github_issue› tags.
- Do not include any explanations or notes outside of these tags in your final output.

* Keep sentences short (<20 words), avoid jargon, spell out acronyms once.

### Labels reference
- `ktlo`: Essential maintenance to keep systems running (bug fixes, patches, operations).
- `new-feature`: Development of new functionality, integrations, or product capabilities.
- `improvement`: Enhancements to existing features (performance, UX, reliability, security).
- `productivity`: Investments in code quality, developer experience, tooling, or scalability.

Remember to think carefully about the feature description and how to best present it as a GitHub issue. Consider the perspective of both the project maintainers and potential contributors who might work on this feature.

Your final output should consist of only the content within the ‹github_issue> tags, ready to be copied and pasted directly into GitHub. Make sure to use the GitHub CLI `gh issue create` to create the actual issue after you generate. Assign described labels based on the nature of the issue.