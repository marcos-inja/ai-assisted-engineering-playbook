# Custos e performance: roteamento, budgets, cache e retries

## Quando usar / Quando evitar

- **Quando usar**: qualquer sistema com volume (produtos com IA, automações internas em lote, agentes rodando em CI) ou quando o custo de um “modelo topo” é proibitivo.
- **Quando evitar**: “roteamento” sem métrica de qualidade/erro — vira loteria barata que aumenta retrabalho.

## Sinais de que está dando errado

- **Custo cresce sem ganho de qualidade**: prompts longos e repetitivos; falta de cache; falta de limites de output.
- **Qualidade instável** (piora aleatória): roteamento por heurística fraca; ausência de fallback com *quality gate*.
- **Latência imprevisível**: retries em cascata sem budget; tool calls excessivas; batching inexistente.

## Checklist operacional

### 1) Defina budgets (contratos explícitos)

- **Por request**: max input tokens, max output tokens, max tool calls, max retries.
- **Por feature**: custo mensal, p95 latência, taxa de falhas/retries.
- **Por tarefa** (agentes): número máximo de iterações e “stop conditions”.

### 2) Roteamento por complexidade (triagem)

Crie uma política simples e auditável:
- **Tier barato**: classificação, extração, linting textual, “boilerplate” controlado.
- **Tier caro**: decisões arquiteturais, refactors, debugging, tarefas multi-arquivo.

Padrão recomendado:
- **cheap-first com fallback**: roda barato → aplica *quality gate* → se falhar, escala modelo.

### 3) Caching (onde dá mais ROI)

- **Prompt caching** (inputs repetidos): system prompts estáveis, políticas, templates.
- **Cache de retrieval**: resultados de busca/embedding/RAG por TTL e versionamento.
- **Cache semântico** (alta repetição): somente quando o risco de stale é aceitável e há invalidação.

### 4) Quality gates para fallback (anti “barato errado”)

Escolha gates que não dependem de “parecer bom”:
- validação por schema (JSON)
- lint/typecheck
- testes unit/integration
- checagens determinísticas (regex/AST)

### 5) Retries e políticas de falha

- **Retry com mudança de condição** (não repita igual):
  - aumentar modelo
  - reduzir contexto
  - adicionar evidência (arquivo/símbolo)
  - mudar formato (JSON/steps)
- **Circuit breaker**:
  - se falhar N vezes, parar e pedir intervenção humana ou registrar incidente

## Trade-offs e decisões

- **Roteamento agressivo** reduz custo mas aumenta risco de regressão e retrabalho.
- **Caching agressivo** reduz custo/latência mas aumenta risco de respostas “stale” (principalmente para código que muda).
- **Fallback automático** melhora qualidade mas pode duplicar custo; controle com budget e gates.

## Exemplos (políticas práticas)

### Política simples de roteamento (para automação e backoffice)

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

### Budget por agente (long-running)

```text
Max iterations: 5
Max tool calls: 60
Max output tokens/iteration: 800
Stop if:
  - tests green AND lint/typecheck green
  - or 2 consecutive iterations with no progress
```

## Referências

- `https://www.getmaxim.ai/articles/reduce-llm-cost-and-latency-a-comprehensive-guide-for-2026/` — estratégias práticas de routing/caching/latency em produção.
- `https://www.maviklabs.com/blog/llm-cost-optimization-2026` — routing + caching + batching como camadas; foco em governança de custos.
- `https://docs.vllm.ai/en/latest/features/speculative_decoding/` — serving otimizado (batching/decoding) quando você controla inferência.

