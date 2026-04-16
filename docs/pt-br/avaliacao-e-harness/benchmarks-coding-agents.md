# Benchmarks para coding agents (como interpretar e não se enganar)

## Quando usar / Quando evitar

- **Quando usar**: comparar modelos/harnesses, validar mudanças de toolset, medir regressão de agent harness.
- **Quando evitar**: usar leaderboard como proxy direto de “vai funcionar no meu monorepo”. Benchmarks têm vieses.

## Sinais de que está dando errado

- **Você troca o harness e credita ganho ao modelo**: harness é variável dominante em muitos cenários.
- **O benchmark não parece seu trabalho**: linguagem, estilo de prompt, estrutura de repo, tooling e CI são diferentes.
- **Solve rate alto mas PRs ruins**: benchmark mede “passar testes”, mas pode não medir segurança, legibilidade, ou manutenção.

## Checklist operacional

### 1) Diferencie “modelo” de “harness”

Controle:
- toolset (busca, navegação, execução)
- contexto (rules, context files)
- limites (max iterações, budget)

### 2) Prefira sinais execution-based

Sempre que possível:
- falha→passa (F2P)
- regressão (P2P)
- build/typecheck/lint

### 3) Use “benchmarks públicos” como triagem, não como decisão final

Decisão final deve incluir:
- eval interno (pequeno) em código real
- tracing de tool-use
- custo por tarefa

## Trade-offs e decisões

- Benchmarks **repo-level** (tipo SWE-bench) aproximam trabalho real melhor do que benchmarks de função isolada (HumanEval), mas ainda têm viés.
- Benchmarks **multilíngua** ajudam para codebases poliglotas.
- Benchmarks “production-derived” (internos) são ouro, mas difíceis de manter.

## Referências (o que cada um te dá)

- [https://www.swebench.com/](https://www.swebench.com/) — benchmark repo-level com variações (Verified/Lite/etc.) para comparar agentes.
- [https://www.swebench.com/verified.html](https://www.swebench.com/verified.html) — subset humano-validado; melhor para comparação confiável.
- [https://openreview.net/forum?id=n577FC6CKk](https://openreview.net/forum?id=n577FC6CKk) e [https://github.com/amazon-science/SWE-PolyBench](https://github.com/amazon-science/SWE-PolyBench) — SWE-PolyBench (multi-língua), mais próximo de ambientes poliglotas.
- [https://arxiv.org/html/2604.01527v1](https://arxiv.org/html/2604.01527v1) — ProdCodeBench: metodologia para benchmark “production-derived”; evidencia papel de tool-use/validação e impacto do harness.

