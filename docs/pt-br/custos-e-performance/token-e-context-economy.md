# Token & context economy (reduzir custo sem perder qualidade)

## Quando usar / Quando evitar

- **Quando usar**: sempre que custo ou latência importam, e principalmente em agentes (múltiplas iterações).
- **Quando evitar**: “compressão” que remove invariantes/decisões; cortar contexto sem garantir oráculos aumenta retrabalho.

## Sinais de que está dando errado

- **Prompt cresce a cada iteração**: falta compaction; tool outputs antigos sendo re-injetados.
- **Respostas verbosas**: ausência de `max_tokens`/limites e ausência de formato estruturado.
- **Busca demais**: navegação ruim, toolset confuso, falta de notes/memória.

## Checklist operacional

### 1) Pare de pagar por texto desnecessário

- **Limite output**: “responda em até N bullets” + `max_tokens`.
- **Formato**: prefira JSON/Markdown curto quando você precisa parsear.
- **Sem duplicação**: não peça “explicação longa” junto com patch.

### 2) Contexto por referência

- Passe:
  - paths reais
  - símbolos
  - IDs de issues/PRs
  - comandos a rodar
- Evite:
  - colar logs enormes
  - colar arquivos completos quando só 30 linhas importam

### 3) Resumos (compaction) como parte do workflow

Quando a conversa ficar longa:
- resuma decisões + plano + pendências
- reinicie com o resumo + últimos arquivos relevantes

### 4) Token-cost drivers típicos em engenharia

- **Tool outputs**: resultados de busca e logs gigantes.
- **Histórico de chat**: repetição de contexto já “resolvido”.
- **RAG chunking ruim**: chunks grandes e irrelevantes.

Mitigações:
- tools com saída “top-k” e “files-only”
- limpar outputs antigos (“tool result clearing”)
- notes persistentes fora do contexto

### 5) Economias que não quebram qualidade

- **Cache de retrieval/tool outputs** com TTL.
- **Batching** (quando aplicável) para embeddings e chamadas repetidas.
- **Roteamento** (cheap-first + gate) para tarefas triviais.

## Trade-offs e decisões

- **Contexto maior** pode reduzir alucinação *até certo ponto*; depois aumenta confusão e custo.
- **Menos contexto** exige harness melhor (tools + oráculos) para não virar adivinhação.

## Exemplos

### Prompt “token-efficient” para revisão

```text
Revise este diff com foco em riscos.

Output:
- 10 achados no máximo
- Cada achado: risco (alto/médio/baixo) + ação sugerida + teste recomendado
Sem explicações longas.
```

### “Tool output contract” (para scripts internos)

```text
Para qualquer comando de diagnóstico:
- retorne somente: 1) resumo, 2) top-10 linhas relevantes, 3) path/linha/erro
- forneça um modo --full apenas sob demanda
```

## Referências

- `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents` — contexto como recurso finito; compaction, note-taking e subagents.
- `https://redis.io/blog/llm-token-optimization-speed-up-apps/` — fontes práticas de desperdício de tokens e estratégias de contenção.

