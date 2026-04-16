# Coding-agent benchmarks (how to interpret without fooling yourself)

## When to use / When to avoid

- **When to use**: compare models/harnesses, validate toolset changes, measure regressions in an agent harness.
- **When to avoid**: treating leaderboards as a direct proxy for “will it work in my monorepo”. Benchmarks have biases.

## Signals things are going wrong

- **You change the harness and credit the gain to the model**: in many settings, the harness is the dominant variable.
- **The benchmark doesn’t look like your work**: language mix, prompt style, repo structure, tooling, and CI differ.
- **High solve rate but bad PRs**: benchmarks measure “tests pass”, not necessarily security, readability, or maintainability.

## Operational checklist

### 1) Separate “model” from “harness”

Control:
- toolset (search, navigation, execution)
- context (rules, context files)
- limits (max iterations, budget)

### 2) Prefer execution-based signals

Whenever possible:
- fail→pass (F2P)
- regressions (P2P)
- build/typecheck/lint

### 3) Use public benchmarks for triage, not final decisions

Final decisions should include:
- a small internal eval on real code
- tool-use tracing
- cost per task

## Trade-offs and decisions

- **Repo-level** benchmarks (SWE-bench-like) are closer to real work than isolated function benchmarks (HumanEval), but still biased.
- **Multi-language** benchmarks help for polyglot codebases.
- **Production-derived** internal benchmarks are gold, but expensive to maintain.

## References (what each gives you)

- [https://www.swebench.com/](https://www.swebench.com/) — repo-level benchmark with variants (Verified/Lite/etc.) to compare agents.
- [https://www.swebench.com/verified.html](https://www.swebench.com/verified.html) — human-validated subset; better for reliable comparisons.
- [https://openreview.net/forum?id=n577FC6CKk](https://openreview.net/forum?id=n577FC6CKk) and [https://github.com/amazon-science/SWE-PolyBench](https://github.com/amazon-science/SWE-PolyBench) — SWE-PolyBench (multi-language), closer to polyglot environments.
- [https://arxiv.org/html/2604.01527v1](https://arxiv.org/html/2604.01527v1) — ProdCodeBench: methodology for “production-derived” benchmarks; shows tool-use/validation role and harness impact.

