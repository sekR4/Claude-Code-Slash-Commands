You are an AI assistant tasked with **refining an existing (possibly rough or outdated) GitHub Issue** so that any developer — or a smaller LLM — can pick it up and deliver.

issue_number: $ARGUMENTS

## Workflow

Follow these steps, make a todo list and **think ultrahard**––but stay concise:

### 0 Preview & Delta Analysis  
- Read issue once end‑to‑end (use `gh issue view`).  
- Summarize: *current intent*, *scope*, *assumptions*.  
- List mismatches: outdated info, missing context, scope creep, unclear goals.  
- Decide if the issue should be **updated**, **split**, or **closed**.

### 1 Repository Reconnaissance  
- Scan repo tree, open issues/PRs, `CONTRIBUTING.md`, coding conventions.  
- Spot affected modules, naming patterns, tests, CI rules.

### 2 Intent Clarification (interactive)  
Ask **only high‑leverage questions** to lock down:  
- Real problem to solve & desired outcome  
- Success / done criteria  
- New constraints or changed circumstances (perf, security, UX, deadlines)  
- You MUST not continue with the next steps until the user answered.

### 3 Precedent & Best‑Practice Scan  
- Grep repo for similar fixes, merged PRs, or design docs.  
- Note helpers/patterns to reuse.  
- Pull **≤2** authoritative external refs if they add clear value.  
- Add findings to **🛠️ Implementation Notes** and **📚 Resources**.

### 4 Mandatory complexity assessment & decomposition  
**MANDATORY**: Re-estimate scope using these criteria:
- **Size**: >3 files OR >400 LOC?
- **Domains**: Involves >2 technical areas (frontend, backend, database, infrastructure, etc.)?
- **Acceptance criteria**: Would need >3 acceptance criteria?
- **Unknowns**: Contains ≥2 unknowns or research tasks?

**Decision point**: 
- **If ANY criterion is met → Convert to Epic with sub-issues**
- **If ALL criteria are false → Keep as focused single issue**

### 5 Epic Conversion Decision
**If converting to Epic**:
- Create parent issue with high-level goal only
- Create 2-5 focused sub-issues, each ≤3 files AND ≤400 LOC
- Parent gets `epic` label, sub-issues get `story`/`task` labels
- Each sub-issue: `Title`, `Goal`, `Exit Criteria`, `Blocked by: #parent`

**If keeping as single issue**:
- Streamline existing content
- Ensure ≤3 acceptance criteria
- Remove over-engineering

### 6 Plan Outline  
Wrap in `<plan>` tags:  
- Section order you'll use  
- Labels / milestones / assignee logic  
- Any repo‑specific conventions (folders, tests, branch naming)

### 7 Draft the Refined GitHub Issue(s)  
After plan approval, output based on complexity assessment:

**If SIMPLE (no decomposition)**: Output refined issue in `<github_issue>` tags
**If COMPLEX (epic conversion)**: Output parent epic + sub-issues

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


### ✔️ Checklist
* [ ] Clarify open questions
* [ ] Add/update unit tests
* [ ] Update docs
* [ ] Pass CI
```

### 8 For COMPLEX issues (Epic Conversion)
Close original issue and create Epic + Sub-issues.

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

### 🔗 Replaces
Closes #original_issue_number (refined and decomposed)

```

#### Sub-Issue Format (each in separate `<sub_issue>` tags):
```md
### 📌 Title
<focused, actionable task>

### 🎯 Goal
<specific outcome>

### ✅ Exit Criteria
1. Specific, testable condition
2. Another specific condition
3. (max 3 criteria)

Part of #<parent-issue-number>

```

### 9 Final Output Rules
**For SIMPLE refinement**: Present refined content in `<github_issue>` tags only.
**For EPIC conversion**: Present epic in `<github_issue>` tags, then each sub-issue in separate `<sub_issue>` tags.

* Keep sentences concise & short (<20 words), avoid jargon, spell out acronyms once.
* Use GitHub CLI to update/create issues after generation.
* For epic conversion: close original issue and create new epic + sub-issues.

## Labels reference
- `ktlo`: Essential maintenance to keep systems running (bug fixes, patches, operations).
- `new-feature`: Development of new functionality, integrations, or product capabilities.
- `improvement`: Enhancements to existing features (performance, UX, reliability, security).
- `productivity`: Investments in code quality, developer experience, tooling, or scalability.

**Key principle**: Transform rough thoughts into focused, actionable issues (≤3 files, ≤400 LOC). When in doubt, decompose further.

**Implementation flow for epic conversion**:
1. Generate epic + sub-issue content
2. Use `gh issue create` to create epic with `--label epic`
3. For each sub-issue:
   - Create with `gh issue create --label story` (or `task`)
   - Include "Part of #<parent-number>" in the body for tracking
4. Update epic with actual sub-issue numbers in task list
5. Close original issue with reference: `gh issue close <original> -c "Refined and decomposed into #<epic-number>"`
6. Note: Parent-child relationships in the GitHub UI require manual project board setup or can be set via:
   - `gh project item-add <project> --owner <owner> --issue <number>`
   - Then setting the "Parent issue" field if configured in <project>