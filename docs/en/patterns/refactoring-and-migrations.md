# Patterns: refactors and migrations (large changes with control)

## When to use / When to avoid

- **When to use**: upgrades, API migrations, infra changes, multi-file refactors, repetitive changes (codemods).
- **When to avoid**: “big bang” without gates and rollout. With AI, this gets worse.

## Signals things are going wrong

- **Giant diff**: tasks weren’t split.
- **Lack of compatibility**: broken contracts (API/DB/events).
- **Hard-to-trace regressions**: no stages, no checkpoints, no F2P/P2P.

## Operational checklist

### Recommended staged strategy

- **Map impact** (impact map)
- **Create atomic tasks** (1 verifiable change per PR)
- **Use codemods when mechanical**
- **Stage gates** (lint/typecheck/tests/e2e subset)
- **Rollout with compatibility**:
  - dual-read / dual-write (when needed)
  - feature flags
  - canary

### Data migrations

- dry-run
- idempotent backfill
- monitoring and rollback plan

## Trade-offs and decisions

- Codemods reduce cost and risk; AI can help design and adjust the codemod, but it doesn’t replace gates.
- Dual-write increases temporary complexity, but reduces downtime risk.

## Examples

### PR template for a large refactor

```text
Goal: <one sentence>
Scope: <folders/files>
Acceptance:
- [ ] tests green
- [ ] no behavior change (or specify what changes)
Rollout plan: <if applicable>
```

## References

- [../architecture/harness-engineering.md](../architecture/harness-engineering.md) — impact map + task specs.
- [../evaluation-and-harness/ci-gates-and-regressions.md](../evaluation-and-harness/ci-gates-and-regressions.md) — gates and regressions.

