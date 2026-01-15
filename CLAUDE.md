# Engineering Guidelines

## Dependencies & Runtime
- Use [`uv`](https://github.com/astral-sh/uv) for dependency management and execution:
  - Add dependencies: `uv add …`
  - Run scripts: `uv run …`

## Python Philosophy
- **Functions-first**: Default to functions for stateless operations and data transformations.
- **Use classes when**:
  - Multiple methods share state (3+ methods is a good heuristic)
  - You need Pydantic models (`BaseModel`, `BaseSettings`) for config/validation
  - Clear polymorphic behavior or inheritance is needed
- **Cohesion over convention**: Group code by what changes together, not by arbitrary categories.
- **Abstractions**: Introduce them at known variation points or when anticipating change, not as generic "good practice."
- **SOLID applies strategically**: Use dependency injection, interfaces, and separation when you identify seams that will change—not everywhere by default.

## Code Quality
- **Cognitive load is the metric**: Can this section be understood without holding the whole system in memory? That's the readability bar.
- **Decompose with purpose**: Split at meaningful abstraction boundaries—where it enables independent testing or change—not at arbitrary line counts.
- **Keep It Simple (KISS)**: Solve the problem at hand without unnecessary complexity.
- **Done > Perfect**: Ship working code over perfect code. Iterate based on real needs.
- **Less code is better**: Write efficient, non-redundant code. Remove dead code. Smart/concise, not minimal at all costs.
- **Avoid over-engineering**: Build what is needed now. Don't architect for hypothetical futures.
- **Easy to Change (ETC)**: When you know code will evolve, favor extensibility. When it's one-off, favor simplicity.

## SQL
- Use **PostgreSQL** dialect for all SQL.
- Write **all keywords in lowercase** for consistency.

## Testing
- Target **~80% coverage** on core functionality.
- Focus on **contracts and behavior**, not implementation details.
- Avoid **over-engineered tests**: No excessive mocking, no brittle setup. Tests should be clear and maintainable.
- Run tests **before every commit/push**:
  - `uv run pytest tests/ -v`

## Workflow
- **Clarify**: if P(understood) < 90%, ask a few clarifying questions using the `AskUserQuestion` tool.
- **Plan before you act**: Thorough preparation saves time.
- **Small, verifiable steps**: If a change can't be tested or verified quickly, break it down further.
- **Use `cli`/`mcp` tools** instead of guessing—leverage what exists:
  - `gh` (GitHub CLI)
  - `context7` (fetch latest docs/examples)
  - `duckdb` (local data exploration)
- **Implement only what is requested**:
  - Suggest improvements in comments or separately.
  - Do not implement suggestions without explicit approval.

## Project Context
- Check project-specific `CLAUDE.md` (or docs/readme) for phase indicators (PoC/MVP/Production) and local guidelines.
- Adapt code quality balance based on project phase when specified.
