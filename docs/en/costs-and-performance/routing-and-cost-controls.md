# Costs and performance: routing, budgets, caching, retries

## When to use / When to avoid

- **When to use**: any high-volume system (AI products, batch internal automation, agents running in CI) or when the cost of a frontier model is prohibitive.
- **When to avoid**: routing without quality/error metrics — it becomes cheap roulette that increases rework.

## Signals things are going wrong

- **Cost grows with no quality gain**: long, repetitive prompts; missing caching; missing output limits.
- **Unstable quality** (random degradation): weak routing heuristics; no fallback with a *quality gate*.
- **Unpredictable latency**: cascading retries without budgets; too many tool calls; no batching.

## Operational checklist

### 1) Define budgets (explicit contracts)

- **Per request**: max input tokens, max output tokens, max tool calls, max retries.
- **Per feature**: monthly cost, p95 latency, failure/retry rate.
- **Per task** (agents): max iterations and stop conditions.

### 2) Route by complexity (triage)

Build a simple, auditable policy:
- **Cheap tier**: classification, extraction, text linting, controlled boilerplate.
- **Expensive tier**: architectural decisions, refactors, debugging, multi-file tasks.

Recommended pattern:
- **cheap-first with fallback**: run cheap → apply a *quality gate* → if it fails, escalate the model.

### 3) Caching (highest ROI first)

- **Prompt caching** (repeated inputs): stable system prompts, policies, templates.
- **Retrieval cache**: search/embedding/RAG results with TTL + versioning.
- **Semantic cache** (high repetition): only when stale risk is acceptable and invalidation exists.

### 4) Quality gates for fallback (anti “cheap but wrong”)

Choose gates that don’t depend on “looks good”:
- schema validation (JSON)
- lint/typecheck
- unit/integration tests
- deterministic checks (regex/AST)

### 5) Retries and failure policy

- **Retry with a changed condition** (don’t repeat the same call):
  - upgrade model
  - reduce context
  - add evidence (file/symbol)
  - change format (JSON/steps)
- **Circuit breaker**:
  - if it fails N times, stop and require human intervention or log an incident

## Trade-offs and decisions

- **Aggressive routing** lowers cost but increases regression and rework risk.
- **Aggressive caching** lowers cost/latency but increases stale-answer risk (especially when code changes).
- **Automatic fallback** improves quality but can double cost; control it with budgets and gates.

## Examples (practical policies)

### Simple routing policy (automation/backoffice)

```text
if task in {classification, extraction, summarization_with_schema}:
  model = cheap
  gate = schema_validate
elif task in {code_change_small_with_tests}:
  model = mid
  gate = unit_tests + lint
else:
  model = strong
  gate = tests + reviewer_rubric

if gate fails:
  escalate model (cheap→mid→strong) up to budget
```

### Per-agent budget (long-running)

```text
Max iterations: 5
Max tool calls: 60
Max output tokens/iteration: 800
Stop if:
  - tests green AND lint/typecheck green
  - or 2 consecutive iterations with no progress
```

## References

- `https://www.getmaxim.ai/articles/reduce-llm-cost-and-latency-a-comprehensive-guide-for-2026/` — practical routing/caching/latency strategies in production.
- `https://www.maviklabs.com/blog/llm-cost-optimization-2026` — routing + caching + batching as layers; cost governance focus.
- `https://docs.vllm.ai/en/latest/features/speculative_decoding/` — optimized serving (batching/decoding) when you control inference.

