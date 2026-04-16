# Patterns: review & safety (AI-generated PRs, security, compliance)

## When to use / When to avoid

- **When to use**: every time AI generates code, IaC, pipelines, or configs.
- **When to avoid**: “approve because it compiles”. AI tends to be plausibly wrong.

## Signals things are going wrong

- **Large change without a reason**: unsolicited refactor, broad diffs.
- **Silent security changes**: relaxed authz, sensitive logs, removed validation.
- **Dependencies added casually**: supply-chain risk.

## Operational checklist (review rubric)

### Correctness and maintainability

- invariants preserved?
- edge cases and null states?
- concurrency/idempotency/timeouts?
- API/DB contract preserved?

### Security

- secrets in code/logs?
- injection (SQL/command/template)?
- SSRF/path traversal/deserialization?
- authn/authz correct? (fail closed)

### Reliability

- retries and timeouts defined?
- errors handled with context?
- observability (logs/metrics/traces) adequate?

### Tests

- tests cover the change? (F2P when applicable)
- avoids brittle mocks?
- enough regression (P2P)?

## Trade-offs and decisions

- Human review is the “final gate” for high risk.
- Automate what you can: secret scanning, SAST, lint, typecheck, unit/integration.

## Examples

### “Anti-vibe” checklist

```text
- Which canonical file/pattern does this follow?
- Which test proves this is correct?
- What regression could this introduce?
- Which part is irreversible/high-risk?
```

## References

- `docs/en/evaluation-and-harness/ci-gates-and-regressions.md` — how to structure gates by risk.

