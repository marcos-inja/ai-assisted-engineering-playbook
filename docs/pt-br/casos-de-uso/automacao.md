# Casos de uso: automação (triagem, docs, releases, backoffice)

## Quando usar / Quando evitar

- **Quando usar**: triagem de issues, geração de changelog/release notes, atualização de docs, rotinas internas em lote.
- **Quando evitar**: automação “que escreve” sem gates (schema validation, revisão, ou execução determinística).

## Sinais de que está dando errado

- **Conteúdo inconsistentes**: faltou schema/constraints; prompt muito aberto.
- **Custo alto em lote**: faltou roteamento + cache + batching.
- **Erros silenciosos**: falta de observabilidade e “audit log”.

## Checklist operacional

- definir formato estruturado (JSON/YAML) quando possível
- aplicar schema validation
- usar roteamento (cheap-first) e fallback apenas com gate
- registrar input/output (hash), custo e erros

## Trade-offs e decisões

- Automação “barata” tende a ser boa para extração e síntese; ruim para decisões complexas sem evidência.

## Exemplos

### Template: triagem de issue com schema

```json
{
  "severity": "low|medium|high",
  "area": "backend|frontend|devops|docs|other",
  "action": "fix|investigate|question|wontfix",
  "next_steps": ["..."]
}
```

## Referências

- [../custos-e-performance/routing-e-controle-de-custos.md](../custos-e-performance/routing-e-controle-de-custos.md) — roteamento, cache e gates.

