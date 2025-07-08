You are an AI assistant tasked with turning a brief feature description into a **ready‑to‑use GitHub Issue** that any developer (or smaller LLM) can pick up and deliver.

<feature_description>
$ARGUMENTS
</feature_description>

## Workflow

Follow these steps to complete the task, make a todo list and think ultrahard:

### 1 Repository reconnaissance  
- Scan repo tree, open issues / PRs, `CONTRIBUTING.md`, and coding conventions.  
- Note affected modules, naming patterns, test setup, CI rules.

### 2 Intent clarification (interactive)  
Ask **only the highest‑leverage questions** needed to lock down:  
- Real problem to solve & desired outcome  
- Success / done criteria  
- Hard constraints (perf, security, UX, deadlines)  
- Capture answers for later reference.
- You MUST not continue with the next steps until the user answered.

### 3 Precedent & Best-Practice Scan
- Grep the repo for similar code, merged PRs, or design docs.
- Note any internal helpers or patterns to reuse.
- Pull **≤2** authoritative external refs (RFC, framework docs, blog post) *only if they add clear value*.
- Add findings to **🛠️ Implementation Notes** and **📚 Resources**.

### 4 Mandatory complexity assessment & decomposition  
**MANDATORY**: Estimate scope using these criteria:
- **Size**: >3 files OR >400 LOC?
- **Domains**: Involves >2 technical areas (frontend, backend, database, infrastructure, etc.)?
- **Acceptance criteria**: Would need >3 acceptance criteria?
- **Unknowns**: Contains ≥2 unknowns or research tasks?

**If ANY criterion is met → MUST split into sub‑issues**:
- Create Epic (parent issue) with high-level goal only
- Create 2-5 focused sub-issues, each ≤3 files AND ≤400 LOC
- Parent issue gets `epic` label, sub-issues get `story`/`task` labels
- Each sub-issue: `Title`, `Goal`, `Exit Criteria`, `Blocked by: #parent`

### 5 Plan outline  
Wrap the following in `<plan>` tags:  
- Section order you'll use  
- Labels / milestones / assignee logic  
- Any repo‑specific conventions (folder, test, branch naming)  

### 6 Draft the GitHub Issue(s)  
After plan approval, output based on complexity assessment:

**If SIMPLE (no decomposition needed)**: Output single issue in `<github_issue>` tags
**If COMPLEX (decomposition required)**: Output parent epic + sub-issues

#### For SIMPLE issues, use this format in `<github_issue>` tags:

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

### 7 For COMPLEX issues (Epic + Sub-issues)
After outputting the parent epic, create actual sub-issues using `gh issue create` and update parent with task list.

#### Epic Format (in `<github_issue>` tags):
```md
### 📌 Title
<high-level imperative>

### 📝 Problem
<why this matters, business impact>

### 🎯 Goal / Outcome
<observable result when complete>

### 📋 Sub-Issues
- [ ] #XXX - [Sub-issue title]
- [ ] #XXX - [Sub-issue title]
- [ ] #XXX - [Sub-issue title]
```

#### Sub-Issue Format (each in separate `<sub_issue>` tags):
```md
### 📌 Title
<focused, actionable task>

Part of #<parent-issue-number>

### 🎯 Goal
<specific outcome>

### ✅ Exit Criteria
1. Specific, testable condition
2. Another specific condition
3. (max 3 criteria)
```

### 8 Final output rules
**For SIMPLE issues**: Present complete content in `<github_issue>` tags only.
**For COMPLEX issues**: Present epic in `<github_issue>` tags, then each sub-issue in separate `<sub_issue>` tags.

* Keep sentences short (<20 words), avoid jargon, spell out acronyms once.
* Use GitHub CLI to create all issues after generation.
* Update parent epic with actual sub-issue numbers after creation.

### Labels reference
- `ktlo`: Essential maintenance to keep systems running (bug fixes, patches, operations).
- `new-feature`: Development of new functionality, integrations, or product capabilities.
- `improvement`: Enhancements to existing features (performance, UX, reliability, security).
- `productivity`: Investments in code quality, developer experience, tooling, or scalability.

**Key principle**: Create focused, actionable issues (≤3 files, ≤400 LOC). When in doubt, decompose further.

**Implementation flow**:
1. Generate issue content
2. Use `gh issue create` to create parent (if epic) with `--label epic`
3. For each sub-issue:
   - Create with `gh issue create --label story` (or `task`) 
   - Include "Part of #<parent-number>" in the body for tracking
4. Update parent epic with actual sub-issue numbers in task list
5. Note: Parent-child relationships in the GitHub UI require manual project board setup or can be set via:
   - `gh project item-add <project> --owner <owner> --issue <number>`
   - Then setting the "Parent issue" field if configured in <project>