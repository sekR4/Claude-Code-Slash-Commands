---
description: Create a ready-to-implement GitHub issue from user input
allowed-tools: [Bash(gh issue view:*), Bash(gh issue create:*), Read, Write, Edit]
thinking: ultrathink
---

Create a self-contained GitHub issue that requires no follow-up questions from another LLM.

Input: $ARGUMENTS

## Workflow

### 1. Repository Context
- Scan structure, patterns, conventions
- Find similar merged PRs
- Note test setup

### 2. Deep Clarification (MANDATORY - ASK, DON'T ASSUME)

**CRITICAL**: You MUST ask these questions and WAIT for answers. Do NOT proceed or make assumptions.

Start with: "I need to understand this better before creating an issue."

**Step 1: Determine Type**
ASK: "Is this fixing something broken (bug) or adding something new (feature)?"
WAIT for answer.

**Step 2: Gather Context**
Based on their answer, ASK these questions (and number them):

For Problems/Bugs:
1. "What exactly is broken? Can you show me the error or describe the issue?"
2. "When did this start happening?"
3. "What's the impact? (users affected, revenue lost, etc.)"

For Features/Stories:
1. "What capability are we adding?"
2. "Who needs this and why?"
3. "How will we measure success?"

Think ultrahard, if you need additional information. If so, ask highest‑leverage questions (3 max).

**STOP HERE. Wait for their responses.**

**Solution Design**
Only AFTER they answer, think ultrahard & present thoroughly designed options:
```
A: Quick Fix (2h) - Minimal change, temporary
B: Proper Fix (6h) - Addresses root cause  
C: Over-engineered (2d) - Future-proof
```

**Lock-In Specification**:
Think ultrahard on Specs.
"Here's EXACTLY what will be built:"
```
File: src/routes/products.ts
Line 45: Add cache check
Pattern: Copy users.ts:L23-30
Test: Second call skips DB
```

WAIT for explicit confirmation.

### Example Interaction

USER: "Add caching"

YOU: "I need to understand this better before creating an issue. Is this fixing something broken (bug) or adding something new (feature)?"

USER: "Fixing slowness"

YOU: "Got it, let's fix this performance issue. I have 3 questions:
1. What exactly is slow? Can you show me specific endpoints or queries?
2. When did this start happening?
3. What's the impact? (users complaining, lost revenue, etc.)"

USER: "Product search takes 3 seconds. Started last week. Users abandoning carts."

YOU: "Based on what you've told me, here are 3 approaches:
A: Quick Fix (2h) - Add Redis cache for top 100 products
B: Proper Fix (6h) - Cache all product queries with TTL
C: Over-engineered (2d) - Elasticsearch integration

Given the cart abandonment, I recommend option B. Thoughts?"

[Continue ONLY after they choose]

### 3. Generate Issue

```markdown
## 📌 Title
[Verb] [component] to [outcome]

## 🔍 Context
[For Problems]
**Pain**: [Observable problem]
**Impact**: [Cost if unfixed]

[For Features]
**Need**: [Who wants what]
**Value**: [Business benefit]

## ✅ Implementation Spec
File: `exact/path.ts`
- Line: After X, before Y
- Code: [Exact change]
- Test: Input → Output

## 🏃 Quick Start
```bash
git checkout -b feat/### (or fix/###)
```

## 🏷️ Labels
`clarification-complete` `ready-to-code` `[bug|feature|enhancement]`
```

Output in `<github_issue>` tags.

## ❌ Common Mistakes to AVOID

1. **Assuming instead of asking**
   BAD: "I'll assume you want to cache the product endpoint..."
   GOOD: "What exactly is slow?"

2. **Proceeding without answers**
   BAD: "Here are 3 options for your caching needs..."
   GOOD: "I need to understand the problem first. Could you answer the questions above?"

3. **Creating issues from vague input**
   BAD: User says "add tests" → Create generic test issue
   GOOD: User says "add tests" → "What specifically needs testing? What bugs have we missed?"