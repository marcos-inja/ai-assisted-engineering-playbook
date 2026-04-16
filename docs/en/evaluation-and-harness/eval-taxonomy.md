# Evaluation: practical taxonomy (what to measure and how to trust it)

## When to use / When to avoid

- **When to use**: whenever AI enters production (code, PRs, pipelines, LLM-powered products), and when you want to scale to a team/org.
- **When to avoid**: using “LLM-as-a-judge” as the only verdict for testable things. Prefer execution (tests/build) when available.

## Signals things are going wrong

- **Metrics go up but production bugs increase**: you’re measuring “good-looking”, not correctness.
- **Non-reproducible evals**: flaky tests; mutable datasets; missing prompt/model versioning.
- **Unfair comparisons**: the harness changes (tools/context) and you attribute gains to the model.

## Operational checklist

### 1) Choose the right oracle

- **Execution (preferred)**:
  - unit/integration/e2e tests
  - build, typecheck, lint
  - performance benchmarks (p95/p99)
- **Deterministic rules**:
  - schema validation
  - custom AST/lints
  - contract invariants
- **LLM judge (last resort)**:
  - textual quality, alignment, UX copy, summaries
  - always with a rubric and examples

### 2) What to measure (by category)

- **Correctness**: passes tests; doesn’t break regressions.
- **Robustness**: behavior under edge cases and adversarial inputs.
- **Reliability**: variance across runs; retry rate; flakiness.
- **Efficiency**: cost per task, tokens, tool calls, latency.
- **Security**: policy compliance, red teaming, secret leakage.

### 3) Minimum instrumentation for evaluation

- log: model/version, prompt hash, context hash, tools, time, cost
- validation results (tests/lint/build) and produced diffs

## Trade-offs and decisions

- **Execution-based evals** cost more infra, but provide real confidence.
- **LLM judges** scale cheaply but are biased/unstable; use only for non-testable aspects.
- **Harness** affects outcomes: better tools can narrow model gaps — good, but must be controlled.

## Examples

### Short LLM-judge rubric (when unavoidable)

```text
Criteria (0–2 each):
- factuality vs provided evidence
- completeness vs goal
- practical actionability (executable steps)
- concision (no redundancy)
```

## References

- `https://arxiv.org/html/2604.01527v1` — execution-based (fail-to-pass tests) and harness/tooling impact.
- `https://www.swebench.com/` — widely used repo-level benchmark for comparing agents.

