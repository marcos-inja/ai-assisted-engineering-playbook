# Fundamentals: operational mental model (prompt vs context vs harness)

## When to use / When to avoid

- **When to use**: whenever you want predictability (less “vibe coding”) and you need to decide **which mode, which model, which evidence**, and **which validation mechanism**.
- **When to avoid**: you don’t. This is the map. What you *do* avoid is “copy-paste theory”; only things that change decisions belong here.

## Signals things are going wrong (and how to diagnose)

- **The agent invents paths, APIs, or symbols**: you’re missing a “source of truth” (the repo) and an *impact map*; you’re feeding it a ticket, not code.
- **The output looks good but breaks in integration**: you lack an *oracle* (tests/lint/typecheck) in the loop; validation isn’t coupled to the workflow.
- **The more context you dump, the worse it gets**: *context rot* / loss of focus; you provided noise instead of signal.
- **Large, incoherent changes**: tasks aren’t atomic; you’re missing gates (plan → implement → verify).

## Operational checklist (minimum for consistent results)

- **Define the goal in verifiable terms**
  - What behavior changes?
  - Which test/check proves it’s correct?
  - Which regression is unacceptable?
- **Choose the operating mode**
  - Chat/pairing (exploration)
  - Agent (multi-file execution)
  - Multi-agent (parallel search/sweep + synthesis)
- **Provide context by reference, not by dumping**
  - Real file paths, symbols, canonical examples
  - “Find X and follow pattern Y” instead of pasting 2k lines
- **Put validation inside the loop**
  - Tests, lint, typecheck, build, e2e, smoke
  - “Fail → fix → re-validate” as the default rhythm

## Trade-offs and decisions

### Prompt engineering vs Context engineering vs Harness engineering

- **Prompt engineering**: how you express instructions and output format.
  - **Good for**: style, structure, steps, constraints.
  - **Limit**: it can’t replace evidence; it won’t fix repo ignorance.

- **Context engineering**: how you **curate tokens** (instructions + tools + data + history) to maximize signal.
  - **Good for**: reducing hallucination and drift; keeping focus; controlling cost.
  - **Techniques**: minimum viable context (MVC), *just-in-time context*, compaction, note-taking, subagents.

- **Harness engineering**: designing the **working environment** (process + tools + gates) that makes the agent reliable.
  - **Good for**: predictability and team scalability; reducing “structural errors”.
  - **Core**: impact (impact map) → structured tasks → validation.

### Core idea: “context is a finite resource”

More tokens means higher cost and higher chances to:
- lose retrieval precision,
- mix instructions,
- anchor on stale information.

Practical conclusion: **prefer references + tool use** over pasting content.

## Examples (copyable artifacts)

### Template: a “verifiable” request

```text
Goal: <behavior change in one sentence>

Minimum context:
- Relevant files/symbols: <real paths and symbols>
- Pattern to follow: <reference to an existing implementation>

Constraints:
- Do not change: <what must not change>
- Performance/SLA: <if applicable>
- Security: <if applicable>

Acceptance (verifiable):
- [ ] <criterion 1>
- [ ] <criterion 2>

Validation:
- Run: <commands/tests>
```

### “If the output is wrong, fix the harness”

Operational rule: when it fails, record **which gate** was missing:
- missing impact map?
- missing task with real paths?
- missing tests?
- missing scope limits?

## References

- [https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — defines context engineering, MVC, compaction, note-taking, and subagents; explains why more context can get worse.
- [https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development](https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development) — practical harness blueprint (impact map + task template + checkpoint).

