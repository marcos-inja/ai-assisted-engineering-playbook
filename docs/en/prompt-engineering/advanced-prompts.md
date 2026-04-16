# Advanced prompt engineering (focused on verifiable output)

## When to use / When to avoid

- **When to use**: to guide the agent on format, constraints, strategy, and acceptance criteria — especially when the problem is ambiguous.
- **When to avoid**: as a “replacement” for real repo context, tests, and tools. A good prompt can’t compensate for missing evidence.

## Signals things are going wrong

- **Long, non-specific answers**: missing *constraints-first* + output limits.
- **It does the wrong thing “correctly”**: acceptance isn’t verifiable; missing anchoring on a real file/symbol.
- **It pretends it ran tests**: you didn’t explicitly require “run and report output”.

## Operational checklist

- **Constraints-first**: declare non-negotiables (security, performance, compatibility, don’t touch X).
- **Verifiable goal**: write acceptance as a pass/fail checklist.
- **Repo anchor**: “follow the pattern of `X` in `Y`” + real paths.
- **Output contract**: small diffs, list of impacted files, validation commands.
- **Scope limit**: “do not refactor beyond what’s necessary”.

## Trade-offs and decisions

### “Procedural” vs “contextual” prompts

- **Procedural** (“do A, then B, then C”) can make smaller models worse and increase regressions when it becomes cargo-cult.
- **Contextual** (“here is the pattern, here are invariants, here is the oracle”) tends to scale better.

### Few-shot examples vs rules

- **Few-shot** is powerful but expensive. Prefer 1–3 **canonical** examples instead of 20 edge cases.
- Large style rules are better enforced via linter/formatter than via prompts.

## Examples (ready-to-use templates)

### Template: small code change (controlled diff)

```text
Task: <one sentence>

Scope:
- Files to touch: <real paths>
- Do not touch: <paths/folders>

Pattern to follow:
- See <file> (function/class <symbol>) and replicate the pattern.

Acceptance:
- [ ] <verifiable criterion>
- [ ] <verifiable criterion>

Required validation:
- Run: <commands>
- If it fails: fix and re-run until it passes.

Output:
- List changed files
- Summarize why (1–3 bullets)
```

### Template: debugging with hypotheses + instrumentation

```text
Problem: <symptom and when it happens>

Constraints:
- Do not change behavior (except the bug)
- Do not change public APIs

Do:
1) Generate 3 hypotheses with observable signals (what we’d see in logs/tests)
2) Propose minimal instrumentation (logs/flags) to distinguish hypotheses
3) Execute the plan and report evidence (test/log output)
4) Apply the minimal fix + a regression test
```

### Template: AI-generated PR review (rubric)

```text
Review this diff as if it were production code.

Rubric:
- Correctness: invariants, edge cases, null states, concurrency
- Security: secrets, injection, authz/authn, SSRF, path traversal
- Performance: unexpected O(n), N+1, allocations, hot paths
- Reliability: retries/timeouts, idempotency, flakiness
- Tests: does it cover the change? avoid brittle mocks?

Deliver:
- 5–15 findings ordered by risk
- Concrete suggestions (lines/files) and tests to add
```

## References

- `https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development` — how to turn a “ticket” into a structured task (paths + symbols + acceptance).
- `https://martinfowler.com/fragments/2026-01-08.html` — TDD as a forcing function to keep humans in the loop.
- `https://arxiv.org/html/2603.17973v1` — TDAD: evidence that “TDD prompting” alone can increase regressions; context and impact analysis matter.

