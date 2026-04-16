# Advanced guide: AI-assisted software engineering

This repository is a **practical reference** for professional AI-assisted software development, focused on **quality**, **cost/efficiency**, **context-based decision-making**, and **verifiable workflows**.

## How to use (reading map by goal)

- **I want higher quality and less rework**
  - Start with `[fundamentals/mental-models.md](fundamentals/mental-models.md)`
  - Then `[architecture/harness-engineering.md](architecture/harness-engineering.md)`
  - Finish with `[evaluation-and-harness/ci-gates-and-regressions.md](evaluation-and-harness/ci-gates-and-regressions.md)`

- **I want lower cost (tokens/inference) without losing quality**
  - `[costs-and-performance/routing-and-cost-controls.md](costs-and-performance/routing-and-cost-controls.md)`
  - `[costs-and-performance/token-and-context-economy.md](costs-and-performance/token-and-context-economy.md)`

- **I want to standardize AI usage in a team (process and light governance)**
  - `[patterns/spec-driven-development.md](patterns/spec-driven-development.md)`
  - `[patterns/review-and-safety.md](patterns/review-and-safety.md)`
  - `[patterns/refactoring-and-migrations.md](patterns/refactoring-and-migrations.md)`
  - `[dev-roadmap/maturity.md](dev-roadmap/maturity.md)`

- **I want to apply it in a specific scenario**
  - Backend: `[use-cases/backend.md](use-cases/backend.md)`
  - Frontend: `[use-cases/frontend.md](use-cases/frontend.md)`
  - DevOps/Cloud: `[use-cases/devops-cloud.md](use-cases/devops-cloud.md)`
  - Automation: `[use-cases/automation.md](use-cases/automation.md)`
  - Embedded AI (LLM-powered product): `[use-cases/embedded-ai.md](use-cases/embedded-ai.md)`

## Content conventions

Each file follows (or should follow) this structure:
- **When to use / When to avoid**
- **Signals things are going wrong** (diagnosis)
- **Operational checklist**
- **Trade-offs and decisions**
- **Examples** (prompts/templates/workflows)
- **References** (links + why they matter)

## Structure

- `fundamentals/`: mental models and operating modes
- `prompt-engineering/`: advanced prompts + context engineering
- `architecture/`: harness, agentic architectures and contracts
- `tools/`: tool landscape and tool-use patterns
- `costs-and-performance/`: routing, caching, token economy and performance
- `evaluation-and-harness/`: evals, CI gates, benchmarks and regressions
- `patterns/`: reusable patterns (SDD, safety, refactors/migrations)
- `use-cases/`: scenario guides (backend, frontend, DevOps, etc.)
- `dev-roadmap/`: maturity path (30/60/90 days)

