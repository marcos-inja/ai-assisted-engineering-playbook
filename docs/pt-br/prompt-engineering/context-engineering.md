# Context engineering (MVC, just-in-time, compaction, memória e subagents)

## Quando usar / Quando evitar

- **Quando usar**: qualquer fluxo agentic com múltiplos passos, principalmente em codebases grandes; quando custo ou alucinação viram problemas.
- **Quando evitar**: “colocar tudo no contexto” como primeira estratégia. Quase sempre é pior.

## Sinais de que está dando errado

- **Contexto inchado** e o agente esquece decisões anteriores.
- **Busca repetitiva** (mesmas queries, mesmos arquivos) → falta de memória externa/notes.
- **Respostas inconsistentes** entre iterações → falta de compaction + resumo fiel.
- **Tool use caótico** → toolset grande e sobreposto; ferramenta sem contrato claro.

## Checklist operacional

### Contexto mínimo viável (MVC)

- **Instruções**: objetivo + restrições + formato de saída (curto e inequívoco).
- **Evidência**: paths/símbolos canônicos + 1–2 exemplos do padrão certo.
- **Oráculo**: comandos de validação e critérios de aceitação.
- **Limites**: escopo (pastas/arquivos) e limites de output.

### Just-in-time context

- Passe **referências** (paths/IDs/links), não o conteúdo.
- Use ferramentas para **carregar sob demanda**:
  - ler arquivo/trecho quando necessário
  - buscar símbolo/padrão
  - executar testes/lint

### Compaction (resumos para long-horizon)

- Resumir mantendo:
  - decisões arquiteturais
  - invariantes e restrições
  - bugs pendentes / hipóteses
  - plano atual e próximos passos
- Remover:
  - tool outputs antigos (ruído)
  - rascunhos e alternativas descartadas

### Memória externa (note-taking)

Manter um arquivo de estado (ex.: `NOTES.md`) com:
- hipótese atual + evidência
- lista de arquivos tocados
- decisões e trade-offs
- checklist de validação

### Subagents

Use subagents para isolar:
- exploração pesada (varredura do repo, pesquisa web)
- diagnóstico (performance/bugs)
- auditoria (segurança, testes)

O lead agent deve receber **somente síntese** (1–2 páginas), não dumps.

## Trade-offs e decisões

### Mais contexto vs mais foco

- **Mais contexto** aumenta custo e pode reduzir precisão.
- **Mais foco** (MVC + JIT) tende a:
  - reduzir alucinação,
  - melhorar consistência,
  - baratear execução.

### “RAG” vs “referências do filesystem”

- **RAG** é útil quando:
  - conhecimento não está no repo (docs internas, wikis)
  - é preciso recuperar de um corpus grande
- **Referências + JIT** é melhor quando:
  - o repo é a fonte da verdade
  - você quer evitar chunking ruim e contexto stale

## Exemplos (padrões prontos)

### Estrutura de contexto recomendada

```text
## Goal
...

## Non-negotiables
...

## Canonical references (paths/symbols)
- ...

## Validation
- ...

## Output contract
...
```

### “Tool results clearing” (prática)

Regra prática: após usar um output de ferramenta, **não recoloque** o conteúdo bruto no contexto; registre só:
- a conclusão
- a evidência mínima (path + linha + erro)
- o próximo passo

## Referências

- [https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — MVC, JIT, compaction, note-taking e subagents; alerta sobre context rot.
- [https://cursor.com/blog/agent-best-practices](https://cursor.com/blog/agent-best-practices) — gestão de contexto em workflows reais com agentes.

