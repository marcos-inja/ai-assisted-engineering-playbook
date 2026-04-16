# CI gates and regressions (making AI safe for production)

## When to use / When to avoid

- **When to use**: every time AI generates or changes code, tests, infra, or configuration.
- **When to avoid**: you don’t. What changes is the “size” of the gate (light vs heavy) based on risk.

## Signals things are going wrong

- **PRs are green but break later**: incomplete gates (missing integration/e2e), or flakiness hiding failures.
- **Agents introduce regressions**: tasks are too large; missing impact analysis; “procedural” TDD without context.
- **CI is too slow**: no relevant test selection; missing caching/parallelization.

## Operational checklist

### 1) Gates by risk level

- **Low risk** (docs, mechanical refactor):
  - lint + fast unit tests
- **Medium risk** (local behavior change):
  - unit + integration subset + typecheck/build
- **High risk** (auth, payments, infra, migrations):
  - integration + e2e + security checks + canary/perf

### 2) Fail-to-pass (F2P) as a strong signal

For bugfix/feature work:
- identify tests that **fail before and pass after**
- keep a P2P (pass-to-pass) set for regression

### 3) Impact analysis (reduce regressions without exploding CI)

Strategies:
- dependency-based test selection (import graph)
- path/pattern-based mapping
- heuristics + validation (execute top-k)

### 4) Anti-flakiness

- run candidate tests multiple times while curating suites
- if flaky: isolate, mark, or remove from the critical gate

## Trade-offs and decisions

- **TDD as a forcing function**: improves human understanding and provides a clear oracle, but can become an empty ritual if the agent follows steps without context.
- **Test selection** reduces cost but increases false-negative risk; mitigate with P2P + smoke.

## Examples (ready-made gates)

### Minimal “agent PR” gate

```text
- lint/format
- typecheck
- unit tests (subset)
- build
```

### High-risk gate (example)

```text
- unit + integration
- e2e smoke
- SAST/secret scan
- migration dry-run (if applicable)
```

## References

- `https://arxiv.org/html/2604.01527v1` — value of validation (tests/static analysis) in the loop and execution-based signals (F2P).
- `https://arxiv.org/html/2603.17973v1` — TDAD: impact of procedural TDD prompting vs providing context/impact analysis to reduce regressions.

