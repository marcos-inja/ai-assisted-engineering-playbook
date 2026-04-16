# Use cases: embedded AI (building an LLM-powered product)

## When to use / When to avoid

- **When to use**: chat over internal data, assistants with tool-use, language-driven automation, RAG.
- **When to avoid**: putting an LLM on the critical path without evals, observability, budgets, and gates.

## Signals things are going wrong

- **Hallucination**: missing grounding (retrieval) or missing a controlled “don’t invent” policy.
- **Costs explode**: large prompts, no cache, no routing, no output limits.
- **Unstable quality**: missing continuous eval and representative datasets.

## Operational checklist

### 1) Minimum “productionizable” architecture

- routing (cheap-first + gates)
- caching (prompt/retrieval)
- observability (traces + costs)
- continuous eval (exec-based where applicable; LLM-judge with rubric)
- security (redaction, secrets, policy)

### 2) RAG (when to use)

Use when:
- answers must be grounded in documents that change

Require:
- chunking + citations/pointers
- metrics (context precision/recall when possible)
- retrieval caching

### 3) Agents with tool-use

Require:
- tools with contracts and validation
- circuit breaker
- human checkpoints for high-risk write actions

## Trade-offs and decisions

- **RAG** improves factuality but adds failure modes (bad retrieval) and cost; offset with caching and observability.
- **Agents** increase capability but expand the risk surface; require gates and logs.

## Examples

### Simple groundedness gate (practical)

```text
Rule: every factual claim must point to evidence (doc_id/snippet/path).
If there is no evidence, answer “I don’t know” and request a source.
```

## References

- [../evaluation-and-harness/eval-taxonomy.md](../evaluation-and-harness/eval-taxonomy.md) — how to pick trustworthy metrics and oracles.
- [../costs-and-performance/routing-and-cost-controls.md](../costs-and-performance/routing-and-cost-controls.md) — budgets, caching, fallback.
- [../tools/tool-use-patterns.md](../tools/tool-use-patterns.md) — tool contracts and agentic loops.

