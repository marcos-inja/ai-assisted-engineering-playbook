# Use cases: backend (APIs, DB, tests, migrations, performance)

## When to use / When to avoid

- **When to use**: CRUD/API, integrations, refactors with coverage, regression debugging, query/hot-path optimization.
- **When to avoid**: domain decisions without a spec (contracts, invariants). Write spec/acceptance/tests first.

## Signals things are going wrong

- **Change passes unit but breaks integration**: missing integration tests and realistic fixtures.
- **SQL/ORM “looks ok” but is slow**: missing an execution plan and benchmarking.
- **Risky migration**: missing rollout strategy and compatibility (dual-write/dual-read).

## Operational checklist

### 1) API changes (contracts and compatibility)

- declare contracts (OpenAPI/JSON schema) and invariants
- define compatibility (backward/forward)
- define versions and deprecations

### 2) Tests as the oracle

- unit for pure logic
- integration for DB/IO
- contract tests for integrations
- smoke tests for critical endpoints

### 3) Debugging and regressions

- ask the agent for: 3 hypotheses + minimal instrumentation
- require evidence (logs/test output) before changing code

### 4) Performance

- require: baseline and budget (p95, throughput)
- ask for analysis: N+1, indexes, caches, serialization

## Trade-offs and decisions

- **Mocking the DB** is faster but lowers confidence; use a real DB in integration for medium/high risk.
- **Refactor + feature** together tends to explode diffs and cost; prefer splitting.

## Examples

### Endpoint task spec

```text
## Description
Add endpoint GET /v1/foo?bar=...

## Files to Modify
- <path> controller/router
- <path> service
- <path> repository

## Acceptance Criteria
- [ ] returns 200 with payload per schema
- [ ] returns 400 for invalid input

## Test Requirements
- [ ] integration test with DB/fixtures
```

## References

- `docs/en/architecture/harness-engineering.md` — impact map + task specs to avoid “wrong module”.
- `docs/en/evaluation-and-harness/ci-gates-and-regressions.md` — gates and F2P/P2P to reduce regressions.

