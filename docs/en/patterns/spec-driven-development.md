# Patterns: pragmatic Spec-Driven Development (SDD) (with a learning loop)

## When to use / When to avoid

- **When to use**: risky features (contracts, data, security), multi-module changes, and anything you want to make “delegable” to agents with predictability.
- **When to avoid**: writing a “perfect monolithic spec” before learning. Prefer a light spec + fast feedback.

## Signals things are going wrong

- **The spec becomes bureaucracy**: it grows but doesn’t guide tasks or tests.
- **The agent drifts from the goal**: vague acceptance; tasks with no real paths/symbols.
- **Implementation contradicts the spec**: missing a “spec update first” gate and acceptance-based review.

## Operational checklist

### Minimum artifacts (per feature)

- **Spec**: what/why + verifiable acceptance (Given/When/Then when it helps).
- **Plan**: how (architecture, impacts, risks, rollout).
- **Tasks**: decomposition into verifiable, PR-sized units with real paths.
- **Oracle**: tests/gates and how to prove done.

### Learning loop (avoid “rigid specs”)

Rule: if, during implementation, you learn something that changes requirements or approach:
- update spec/plan
- then update code

### Direct connection to the harness

For each task:
- reference an existing repo pattern
- list files to modify
- list acceptance + required tests

## Trade-offs and decisions

- SDD increases predictability and reduces rework, but requires discipline to keep artifacts updated.
- “Spec-as-source” (everything generated) only makes sense in very stable domains with strong eval/harness.

## Examples

### Template: light spec (delta spec)

```text
## Goal
...

## Non-goals
...

## Acceptance Criteria
- [ ] ...

## Risks / Rollout
...
```

### Template: task (agent-ready)

See `docs/en/architecture/harness-engineering.md` (task spec).

## References

- `https://developer.microsoft.com/blog/spec-driven-development-spec-kit` — practical SDD/Spec Kit overview.
- `https://github.com/github/spec-kit` — reference toolkit (specify/plan/tasks/implement).
- `https://martinfowler.com/fragments/2026-01-08.html` — critique of rigid specs; focus on feedback loops (TDD).

