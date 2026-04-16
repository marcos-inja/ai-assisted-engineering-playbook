# Avaliação: taxonomia prática (o que medir e como confiar)

## Quando usar / Quando evitar

- **Quando usar**: sempre que IA entra em produção (código, PRs, pipelines, produto com LLM) e quando você quer escalar para time/org.
- **Quando evitar**: “LLM-as-a-judge” como único veredito para coisas testáveis. Prefira execução (tests/build) quando existir.

## Sinais de que está dando errado

- **Métricas sobem mas bugs em produção aumentam**: você está medindo “boa aparência”, não correção.
- **Evals não reproduzíveis**: testes flakey; datasets mutáveis; falta de versionamento de prompts/modelos.
- **Comparações injustas**: harness muda (tools, contexto) e você atribui ganho ao modelo.

## Checklist operacional

### 1) Escolha o oráculo certo

- **Execução (preferido)**:
  - unit/integration/e2e tests
  - build, typecheck, lint
  - benchmarks de performance (p95/p99)
- **Regras determinísticas**:
  - schema validation
  - AST/lints customizados
  - invariantes de contrato
- **LLM judge (último recurso)**:
  - qualidade textual, alinhamento, UX copy, sínteses
  - sempre com rubrica e exemplos

### 2) O que medir (por categoria)

- **Correção**: passa em testes, não quebra regressões.
- **Robustez**: comportamento em edge cases e inputs adversários.
- **Confiabilidade**: variância por seed/run; taxa de retries; flakiness.
- **Eficiência**: custo por tarefa, tokens, tool calls, latência.
- **Segurança**: policy compliance, red teaming, vazamento de segredos.

### 3) Instrumentação mínima para avaliação

- log de: modelo/versão, prompt (hash), contexto (hash), ferramentas, tempo, custo
- resultado de validação (test/lint/build) e diffs gerados

## Trade-offs e decisões

- **Evals exec-based** custam mais infra, mas dão confiança real.
- **LLM-judge** escala barato, mas sofre de viés e instabilidade; use para o que não é testável.
- **Harness** afeta resultado: melhorar ferramentas pode “diminuir gap” entre modelos — isso é bom, mas precisa ser controlado.

## Exemplos

### Rubrica curta para LLM-judge (quando inevitável)

```text
Critérios (0–2 cada):
- factualidade vs evidência fornecida
- completude vs objetivo
- ação prática (passos executáveis)
- concisão (sem redundância)
```

## Referências

- [https://arxiv.org/html/2604.01527v1](https://arxiv.org/html/2604.01527v1) — defende exec-based (fail-to-pass tests) e mostra impacto do harness/tooling.
- [https://www.swebench.com/](https://www.swebench.com/) — benchmark repo-level amplamente usado; útil para comparar agentes.

