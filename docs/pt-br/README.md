# Guia avançado: desenvolvimento assistido por IA (engenharia de software)

Este repositório é um **material de referência prático** (PT-BR) para uso profissional de IA no desenvolvimento de software, com foco em **qualidade**, **custo/eficiência**, **decisão por contexto** e **workflows verificáveis**.

## Como usar (mapa de leitura por objetivo)

- **Quero aumentar qualidade e reduzir retrabalho**
  - Comece por [Fundamentos: modelos mentais](./fundamentos/mental-models.md)
  - Depois [Arquitetura: harness engineering](./arquitetura/harness-engineering.md)
  - Feche com [CI gates e regressão](./avaliacao-e-harness/ci-gates-e-regressao.md)
- **Quero reduzir custo (tokens/inferência) sem perder qualidade**
  - [Roteamento e controle de custos](./custos-e-performance/routing-e-controle-de-custos.md)
  - [Token & context economy](./custos-e-performance/token-e-context-economy.md)
- **Quero padronizar o uso de IA no time (processo e governança leve)**
  - [Spec-driven development](./patterns/spec-driven-development.md)
  - [Review e safety](./patterns/review-and-safety.md)
  - [Refactors e migrações](./patterns/refactoring-and-migrations.md)
  - [Roadmap de maturidade](./roadmap-dev/maturidade.md)
- **Quero aplicar em um cenário específico**
  - Backend: [Caso de uso: backend](./casos-de-uso/backend.md)
  - Frontend: [Caso de uso: frontend](./casos-de-uso/frontend.md)
  - DevOps/Cloud: [Caso de uso: DevOps/Cloud](./casos-de-uso/devops-cloud.md)
  - Automação: [Caso de uso: automação](./casos-de-uso/automacao.md)
  - IA embarcada (produto com LLM): [Caso de uso: IA embarcada](./casos-de-uso/ai-embarcada.md)

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

