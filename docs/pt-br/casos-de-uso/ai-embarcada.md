# Casos de uso: IA embarcada (construindo produto com LLM)

## Quando usar / Quando evitar

- **Quando usar**: chat com dados internos, assistentes com tool-use, automação orientada a linguagem, RAG.
- **Quando evitar**: colocar LLM no caminho crítico sem eval, observabilidade, budgets e gates.

## Sinais de que está dando errado

- **Alucinação**: falta grounding (retrieval) ou falta de “não inventar” com recusa controlada.
- **Custos explodem**: prompts grandes, sem cache, sem roteamento, sem limites de output.
- **Qualidade instável**: falta eval contínua e datasets representativos.

## Checklist operacional

### 1) Arquitetura mínima “produtizável”

- routing (cheap-first + gates)
- caching (prompt/retrieval)
- observabilidade (traces + custos)
- eval contínua (exec-based quando aplicável; LLM-judge com rubrica)
- segurança (redaction, secrets, policy)

### 2) RAG (quando usar)

Use quando:
- resposta precisa estar ancorada em documentos que mudam

Exigir:
- chunking + citations/pointers
- métricas (context precision/recall quando possível)
- cache de retrieval

### 3) Agentes com tool-use

Exigir:
- tools com contrato e validação
- circuit breaker
- human checkpoints para ações de escrita de alto risco

## Trade-offs e decisões

- **RAG** aumenta factualidade, mas adiciona falhas (retrieval ruim) e custo; compensa com cache e observabilidade.
- **Agentes** aumentam capacidade, mas aumentam superfície de risco; exija gates e logs.

## Exemplos

### Gate simples de groundedness (prático)

```text
Regra: toda afirmação factual deve apontar para evidência (doc_id/trecho/path).
Se não houver evidência, responder “não sei” e pedir fonte.
```

## Referências

- [../avaliacao-e-harness/eval-taxonomy.md](../avaliacao-e-harness/eval-taxonomy.md) — como escolher métricas e oráculos confiáveis.
- [../custos-e-performance/routing-e-controle-de-custos.md](../custos-e-performance/routing-e-controle-de-custos.md) — budgets, caching, fallback.
- [../ferramentas/tool-use-patterns.md](../ferramentas/tool-use-patterns.md) — contratos de tools e loops agentic.

