# Advanced guide: AI-assisted software engineering

This repository is a **practical reference** for professional AI-assisted software development, focused on **quality**, **cost/efficiency**, **context-based decision-making**, and **verifiable workflows**.

## How to use (reading map by goal)

- **I want higher quality and less rework**
  - Start with [Fundamentals: mental models](./fundamentals/mental-models.md)
  - Then [Architecture: harness engineering](./architecture/harness-engineering.md)
  - Finish with [CI gates and regressions](./evaluation-and-harness/ci-gates-and-regressions.md)

- **I want lower cost (tokens/inference) without losing quality**
  - [Routing and cost controls](./costs-and-performance/routing-and-cost-controls.md)
  - [Token and context economy](./costs-and-performance/token-and-context-economy.md)

- **I want to standardize AI usage in a team (process and light governance)**
  - [Spec-driven development](./patterns/spec-driven-development.md)
  - [Review and safety](./patterns/review-and-safety.md)
  - [Refactoring and migrations](./patterns/refactoring-and-migrations.md)
  - [Maturity roadmap](./dev-roadmap/maturity.md)

- **I want to apply it in a specific scenario**
  - Backend: [Use case: backend](./use-cases/backend.md)
  - Frontend: [Use case: frontend](./use-cases/frontend.md)
  - DevOps/Cloud: [Use case: DevOps/Cloud](./use-cases/devops-cloud.md)
  - Automation: [Use case: automation](./use-cases/automation.md)
  - Embedded AI (LLM-powered product): [Use case: embedded AI](./use-cases/embedded-ai.md)

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

