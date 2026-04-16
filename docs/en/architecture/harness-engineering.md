# Harness engineering (impact map → task specs → validation)

## When to use / When to avoid

- **When to use**: any multi-repo / multi-module work (monorepo, microservices, infra + app), or when the agent often gets “where to change” wrong.
- **When to avoid**: trivial single-file, low-risk tasks — the overhead doesn’t pay off.

## Signals things are going wrong

- **Plans with invented paths**: the impact map wasn’t generated from the real repo.
- **The agent fixes it “in the wrong module”**: missing a human checkpoint after the impact map.
- **Large PRs that are hard to review**: tasks aren’t atomic; missing “one verifiable goal per task”.

## Operational checklist

### Phase 1 — Repository impact map (planning grounded in code)

Deliverable: a short, reviewable map (not a long essay) containing:
- affected repos/modules
- likely files (real paths)
- existing symbols/patterns to follow
- risks (migration, compatibility, data, performance)

**Human gate**: review the map before creating tasks/PRs.

### Phase 2 — Structured task specs (implementation contract)

Each task must include:
- **Repository** (or module): defines scope
- **Files to modify**: real paths
- **Implementation notes**: references to existing symbols/patterns
- **Acceptance criteria**: pass/fail checklist
- **Test requirements**: which tests and where they live

### Phase 3 — Implementation with validation in the loop

Rules:
- one task at a time
- minimal changes to satisfy acceptance
- always run oracles (tests/lint/typecheck/build) before declaring “done”

## Trade-offs and decisions

- **More structure** ↓ creativity, ↑ predictability (almost always good in production).
- **Overly detailed impact maps** become “fake documentation”; keep them short and verifiable.

## Examples (templates)

### Template: impact map (short and reviewable)

```text
<repoA>:
  changes:
    - ...
  touch:
    - <path>
  follow-pattern:
    - <symbol in file>

<repoB>:
  changes:
    - ...
```

### Template: task spec (ready for execution)

```text
## Repository
<repo/module>

## Description
<1–2 sentences>

## Files to Modify
- `<real/path>` — <what to change>

## Implementation Notes
- Follow the pattern of `<symbol>` in `<file>`
- Reuse `<type>` from `<file>`

## Acceptance Criteria
- [ ] <pass/fail criterion>

## Test Requirements
- [ ] <test/unit/integration> in `<path>`
```

## References

- [https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development](https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development) — impact map + task template + human checkpoint to reduce “structural errors”.
- [https://arxiv.org/html/2604.01527v1](https://arxiv.org/html/2604.01527v1) — IDE-like harness + validation (tests/static checks) increases solve rate and narrows model gaps.

