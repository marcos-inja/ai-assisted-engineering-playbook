# Prompt engineering avançado (com foco em output verificável)

## Quando usar / Quando evitar

- **Quando usar**: para guiar o agente em formato, restrições, estratégia e critérios de aceitação — especialmente quando o problema é ambíguo.
- **Quando evitar**: como “substituto” de contexto real do repo, testes e ferramentas. Prompt bom não compensa ausência de evidência.

## Sinais de que está dando errado

- **Respostas longas, pouco específicas**: faltou *constraints-first* + limite de output.
- **Faz a coisa errada “corretamente”**: aceites não são verificáveis; faltou ancorar em arquivo/símbolo real.
- **Finge que rodou testes**: não houve exigência explícita de “rodar e reportar saída”.

## Checklist operacional

- **Constraints-first**: declare o que é inegociável (segurança, performance, compatibilidade, não mexer em X).
- **Objetivo verificável**: escreva aceites como checklist (pass/fail).
- **Âncora no repo**: “siga o padrão de `X` em `Y`” + paths reais.
- **Formato do output**: diffs pequenos, lista de arquivos impactados, comandos de validação.
- **Limite de escopo**: “não refatore além do necessário”.

## Trade-offs e decisões

### Prompts “procedurais” vs “contextuais”

- **Procedural** (“faça A, depois B, depois C”) pode piorar modelos menores e aumentar regressão quando vira *cargo cult*.
- **Contextual** (“aqui está o padrão, aqui estão os invariantes, aqui está o oracle”) tende a escalar melhor.

### Exemplos (few-shot) vs regras

- **Few-shot** é poderoso, mas caro. Prefira 1–3 exemplos **canônicos** ao invés de 20 edge cases.
- Regras de estilo extensas: melhor via linter/formatter do que prompt.

## Exemplos (templates prontos)

### Template: mudança de código pequena (diff controlado)

```text
Tarefa: <1 frase>

Escopo:
- Arquivos para tocar: <paths reais>
- Não tocar: <paths/pastas>

Padrão a seguir:
- Veja <arquivo> (função/classe <símbolo>) e replique o padrão.

Aceite:
- [ ] <critério verificável>
- [ ] <critério verificável>

Validação obrigatória:
- Rode: <comandos>
- Se falhar: corrija e rode novamente até passar.

Output:
- Liste arquivos alterados
- Resuma o porquê (1–3 bullets)
```

### Template: depuração com hipótese + instrumentação

```text
Problema: <sintoma e quando ocorre>

Restrições:
- Não mude comportamento (exceto bug)
- Não altere APIs públicas

Faça:
1) Gere 3 hipóteses com sinais observáveis (o que veríamos nos logs/testes)
2) Proponha a instrumentação mínima (logs/flags) para distinguir hipóteses
3) Execute o plano e reporte evidência (saída de teste/log)
4) Aplique correção mínima + teste de regressão
```

### Template: revisão de PR gerada por IA (rubrica)

```text
Revise este diff como se fosse para produção.

Rubrica:
- Correção: invariantes, edge cases, estados nulos, concorrência
- Segurança: secrets, injection, authz/authn, SSRF, path traversal
- Performance: O(n) inesperado, N+1, alocações, hot paths
- Confiabilidade: retries/timeouts, idempotência, flakiness
- Testes: cobre a mudança? evita mocks frágeis?

Entregue:
- 5–15 achados em ordem de risco
- Sugestões específicas (linhas/arquivos) e testes a adicionar
```

## Referências

- `https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development` — mostra como transformar “ticket” em task estruturada (paths + symbols + aceites).
- `https://martinfowler.com/fragments/2026-01-08.html` — reforça TDD como forcing function para manter humano no loop.
- `https://arxiv.org/html/2603.17973v1` — TDAD: evidência de que “TDD prompting” puro pode aumentar regressões; contexto e impact analysis importam.

