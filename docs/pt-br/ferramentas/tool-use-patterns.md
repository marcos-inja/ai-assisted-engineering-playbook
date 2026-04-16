# Tool use (function calling, RAG, agentes) — padrões para engenharia

## Quando usar / Quando evitar

- **Quando usar**: sempre que o agente precisa de evidência (repo, logs, métricas) ou precisa agir (rodar testes, abrir PR, consultar DB).
- **Quando evitar**: toolset inflado e sobreposto. Melhor poucas tools, bem definidas, do que “uma tool para cada ideia”.

## Sinais de que está dando errado

- **Agente não sabe qual tool usar**: sobreposição funcional; nomes/descrições ruins.
- **Alucinação de argumentos**: validação fraca de parâmetros; falta de enums e constraints.
- **Outputs enormes**: tool não é token-eficiente; falta “top-k” e “files-only”.

## Checklist operacional

### Design de tools (contrato)

- **Atomicidade**: uma responsabilidade por tool.
- **Parâmetros restritos**: enums, limites, formatos.
- **Erros recuperáveis**: mensagens claras e orientadas a ação.
- **Saída mínima**: resumo + pointers (path/linha/ID).

### Agent loop saudável

1) planejar (impact map / tarefa)
2) agir (editar/executar)
3) observar (saída de teste/lint/consulta)
4) corrigir (até oráculo verde)

### RAG vs JIT file refs

- **RAG**: melhor para docs dispersas e conhecimento fora do repo.
- **JIT file refs**: melhor quando o repo é fonte da verdade (evita chunking e stale).

## Trade-offs e decisões

- Mais tools aumenta capacidade, mas aumenta ambiguidade e custo.
- Tool errors bons permitem “autocorreção” do agente com poucas iterações.

## Exemplos

### Padrão: “resumo + evidência”

```text
Tool output:
- summary: <3–5 linhas>
- evidence:
  - file: <path>
    lines: <n..m>
    note: <por que importa>
```

### Padrão: validação de argumentos (anti-hallucination)

```text
- rejeitar parâmetros fora de enum
- rejeitar paths inexistentes (ou exigir descoberta prévia)
- exigir dry-run para ações destrutivas
```

## Referências

- `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents` — toolsets mínimos, overlap baixo, JIT context.
- `https://www.promptingguide.ai/agents/function-calling` — visão geral prática de function calling em agentes.

