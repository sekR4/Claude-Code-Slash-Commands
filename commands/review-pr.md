Please review the GitHub issue and its corresponding pull request specified

issue_number: $ARGUMENTS
pr_number: $ARGUMENTS

**Instructions:**

1. Use `gh issue view <issue-number>` to read and understand the issue requirements.
2. Use `gh pr diff <pr-number>` to examine all code changes in the PR.
3. Compare the issue and PR:
    - Ensure the PR **fully addresses the issue requirements**, no more and no less.
    - Check for any **breaking changes**; confirm that nothing will disrupt existing functionality unless explicitly required by the issue.
    - Verify that **changes follow the KISS principle** (Keep It Simple, Stupid): avoid unnecessary complexity, only solve the actual problem described in the issue.
    - Assess the code for **SOLID principles** (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion).
    - Prefer **simplicity and clarity** over clever or convoluted solutions.
    - Ignore PR description if it contradicts the issue or code changes.
4. Write a thorough, line-numbered code review in Markdown:
    - Highlight any issues, unclear logic, or potential improvements.
    - Flag code that introduces unnecessary risk or technical debt.
    - Suggest simpler or more robust alternatives where possible.
    - Point out violations of SOLID, KISS, or team conventions.
    - Reference the specific lines in the PR and requirements in the issue.