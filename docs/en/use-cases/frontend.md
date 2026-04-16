# Use cases: frontend (UI, a11y, e2e, visual regression)

## When to use / When to avoid

- **When to use**: component implementation following a design system, UI refactors, a11y fixes, e2e and visual regression.
- **When to avoid**: “design-to-code” without specs (tokens, spacing, breakpoints) and without visual validation.

## Signals things are going wrong

- **UI “looks ok” but breaks on edge cases**: missing states (loading/empty/error) and missing e2e.
- **A11y regressions**: missing automated checks (axe) and keyboard/focus criteria.
- **Silent visual changes**: missing snapshot/visual regression and budgets.

## Operational checklist

### 1) Constraints-first (UI)

- canonical components/patterns to follow
- tokens (spacing, typography, colors)
- responsiveness (breakpoints)
- required states (loading/empty/error)

### 2) Oracles

- unit (component logic)
- e2e (user flow)
- a11y (axe + keyboard navigation)
- visual regression (when available)

### 3) Refactors

- prefer staged mechanical changes (codemod when useful)
- limit scope by folder/feature

## Trade-offs and decisions

- Visual regression increases confidence but costs infra and snapshot maintenance.
- E2E covers real flows but is slower; keep a short smoke suite.

## Examples

### “Verifiable UI” prompt template

```text
Implement component X following the pattern of Y in <file>.

Acceptance:
- [ ] states: loading/empty/error
- [ ] keyboard: correct tab order, visible focus
- [ ] a11y: labels/aria where needed
- [ ] e2e: flow Z passes
```

## References

- [../prompt-engineering/advanced-prompts.md](../prompt-engineering/advanced-prompts.md) — templates for rubrics and verifiable goals.
- [../evaluation-and-harness/ci-gates-and-regressions.md](../evaluation-and-harness/ci-gates-and-regressions.md) — risk-based gates.

