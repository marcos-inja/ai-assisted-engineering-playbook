# Arquiteturas agentic (single agent, multi-agent, contratos e observabilidade)

## Quando usar / Quando evitar

- **Single agent**: implementar tarefas pequenas/médias com validação no loop.
- **Multi-agent**: pesquisa ampla, auditorias, migrações, incidentes, e problemas com alto “search depth”.
- **Evitar multi-agent** quando o problema é simples e local: custo e divergência aumentam.

## Sinais de que está dando errado

- **Agente preso em busca**: falta de navegação melhor (LSP), falta de índice, ou pedido não está ancorado.
- **Escolha errada de ferramenta**: toolset sobreposto; contrato de tool confuso.
- **Execução “black box”**: sem tracing/logs de tool calls; impossível ajustar.

## Checklist operacional

### Contratos de ferramentas (tool contract)

Para cada tool (inclui scripts internos):
- **1 responsabilidade** (atomicidade)
- **entrada validada** (enums/constraints)
- **erro recuperável** (mensagens claras para o agente)
- **saída token-eficiente** (resumo + pointers)
- **baixa sobreposição** com outras tools

### Padrão “generator → evaluator”

Separar papéis:
- **Generator**: propõe mudança e implementa.
- **Evaluator**: valida contra rubrica e oráculos (tests/lint/security).

### Observabilidade

Registre (mínimo):
- modelo, versão, temperatura (se aplicável)
- prompt + contexto (hash/versão)
- tools chamadas + argumentos + duração
- custo (tokens) por etapa
- resultado de validação (testes, lint, etc.)

## Trade-offs e decisões

- **Mais ferramentas** ≠ melhor. Toolset grande aumenta ambiguidade e custo.
- **Subagents** reduzem poluição de contexto do lead agent, mas exigem síntese e critérios.

## Exemplos (padrões de arquitetura)

### Multi-agent para discovery + implementação

```text
Lead:
  - define objetivo e aceites
  - delega discovery para subagent A (codebase map)
  - delega risks/security para subagent B
  - consolida e produz impact map + tasks

Builder:
  - implementa uma task
  - roda testes e corrige até verde

Reviewer:
  - aplica rubrica e sugere ajustes
```

### “Tool output minimization”

Ao projetar tools internas, prefira:
- retornar **IDs/paths/linhas** ao invés de dumps
- retornar **top-k** resultados
- incluir **modo count/files_only** para buscas

## Referências

- `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents` — design de toolsets mínimos, JIT context e subagents.
- `https://arxiv.org/html/2604.01527v1` — harness forte (IDE-like) melhora performance; validação por ferramentas correlaciona com solve rate.

