# ai-assisted-engineering-playbook

## Languages

- **Português (Brasil)**: [`pt-br/README.md`](pt-br/README.md)
- **English**: [`en/README.md`](en/README.md)

# Guia avançado: desenvolvimento assistido por IA (engenharia de software)

Este repositório é um **material de referência prático** (PT-BR) para uso profissional de IA no desenvolvimento de software, com foco em **qualidade**, **custo/eficiência**, **decisão por contexto** e **workflows verificáveis**.

## Como usar (mapa de leitura por objetivo)

- **Quero aumentar qualidade e reduzir retrabalho**
  - Comece por `[fundamentos/mental-models.md](fundamentos/mental-models.md)`
  - Depois `[arquitetura/harness-engineering.md](arquitetura/harness-engineering.md)`
  - Feche com `[avaliacao-e-harness/ci-gates-e-regressao.md](avaliacao-e-harness/ci-gates-e-regressao.md)`
- **Quero reduzir custo (tokens/inferência) sem perder qualidade**
  - `[custos-e-performance/routing-e-controle-de-custos.md](custos-e-performance/routing-e-controle-de-custos.md)`
  - `[custos-e-performance/token-e-context-economy.md](custos-e-performance/token-e-context-economy.md)`
- **Quero padronizar o uso de IA no time (processo e governança leve)**
  - `[patterns/spec-driven-development.md](patterns/spec-driven-development.md)`
  - `[patterns/review-and-safety.md](patterns/review-and-safety.md)`
  - `[patterns/refactoring-and-migrations.md](patterns/refactoring-and-migrations.md)`
  - `[roadmap-dev/maturidade.md](roadmap-dev/maturidade.md)`
- **Quero aplicar em um cenário específico**
  - Backend: `[casos-de-uso/backend.md](casos-de-uso/backend.md)`
  - Frontend: `[casos-de-uso/frontend.md](casos-de-uso/frontend.md)`
  - DevOps/Cloud: `[casos-de-uso/devops-cloud.md](casos-de-uso/devops-cloud.md)`
  - Automação: `[casos-de-uso/automacao.md](casos-de-uso/automacao.md)`
  - IA embarcada (produto com LLM): `[casos-de-uso/ai-embarcada.md](casos-de-uso/ai-embarcada.md)`

## Convenções do conteúdo

Cada arquivo segue (ou deve seguir) a estrutura:

- **Quando usar / Quando evitar**
- **Sinais de que está dando errado** (diagnóstico)
- **Checklist operacional**
- **Trade-offs e decisões**
- **Exemplos** (prompts/templates/workflows)
- **Referências** (links + por que importa)

## Estrutura

- `fundamentos/`: modelos mentais e modos de operação
- `prompt-engineering/`: prompts avançados + context engineering
- `arquitetura/`: harness, arquitetura agentic e contratos
- `ferramentas/`: panorama de ferramentas e padrões de tool-use
- `custos-e-performance/`: roteamento, cache, token economy e performance
- `avaliacao-e-harness/`: harness/eval, CI gates, benchmarks e regressão
- `patterns/`: padrões reutilizáveis (SDD, segurança, refactors/migrations)
- `casos-de-uso/`: guias por contexto (backend, frontend, DevOps, etc.)
- `roadmap-dev/`: trilha de maturidade (30/60/90 dias)

