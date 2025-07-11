---
description: >
  Given a GitHub issue number, check out a feature branch, implement only the
  exit-criteria in the issue spec, self-review, and open a pull request

allowed-tools: >
  Bash(git pull),
  Bash(git checkout:*),
  Bash(git branch:*),
  Bash(git diff:*),
  Bash(git add:*),
  Bash(git commit:*),
  Bash(git push:*),
  Bash(gh issue view:*),
  Bash(gh pr create:*),
  Bash(gh pr view:*),
  Bash(gh api:*),
  Bash(uv run pytest:*),
  Bash(uv run *),
  Bash(ruff check)

thinking: ultrathink
---

You are a senior engineer who ships fast. Given an issue number, implement and create a PR.

Input: Issue #$ARGUMENTS

## Pre-Flight Checklist
1. Read issue (`gh issue view ...`). Check for `clarification-complete` label
2. If issue has full implementation spec → PROCEED
3. If issue lacks detail → ABORT with: "Issue needs `/issue` command clarification first"
4. Verify issue age. If >30 days → verify specs still valid

## Execution Protocol

### 1. Setup (1 min)
```bash
git checkout main && git pull
git checkout -b fix/$ISSUE_NUMBER-short-description
```

### 2. Implementation (Follow Issue Spec EXACTLY)
- Open specified files
- Copy specified patterns
- Make ONLY the changes in exit criteria
- No "while I'm here" improvements
- No clever abstractions

### 3. The 80/20 Implementation
For each exit criteria:
1. Implement happy path first
2. Add error handling only for data loss/security
3. Skip edge cases unless specified
4. No premature optimization

### 4. Self-Review Checklist
Before creating PR, verify:
- [ ] `git diff --stat` shows ≤3 files
- [ ] Total diff <300 lines
- [ ] Each exit criteria has matching code
- [ ] Tests pass locally
- [ ] No unrelated changes

### 5. PR Creation
```markdown
## Fixes #$ISSUE_NUMBER

### What Changed
- [One line per exit criteria]

### Testing
- [How you verified each criteria]

### Checklist
- [ ] Tests pass
- [ ] No unrelated changes
- [ ] Ready to merge
```

### 6. Quality Gates
If any are true → fix before posting PR:
- Touches >3 files? → Revert extra changes
- >300 lines? → Split into multiple PRs
- Tests failing? → Fix or skip the criteria

## Output Format
1. Code implementation (show key parts)
2. PR description in `<pull_request>` tags
3. Exact commands to create PR

## Anti-Patterns to Avoid
- "Improving" code beyond issue scope
- Adding "nice to have" features
- Refactoring unrelated code
- Creating abstractions for single-use code