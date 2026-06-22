# PostgreSQL Advanced + Query Optimization
#s_week 

## Objectivos

- Índices avançados: B-tree, Hash, GiST, GIN, BRIN — quando usar cada um e porquê
- `EXPLAIN ANALYZE` — leitura e interpretação do query plan em profundidade
- Window functions: `ROW_NUMBER`, `RANK`, `LAG`, `LEAD`, `PARTITION BY`
- CTEs recursivas — hierarquias, grafos, sequências
- Query planner understanding
- Particionamento: range, list, hash — quando faz sentido vs overhead
- `pg_stat_statements` e tuning de `postgresql.conf`
- Connection pooling com PgBouncer

## Recursos

| Tipo    | Recurso                                                                         |
| ------- | ------------------------------------------------------------------------------- |
| Livro   | _SQL Performance Explained_ — Markus Winand (use-the-index-luke.com — gratuito) |
| Prática | pgexercises.com — exercícios progressivos gratuitos                             |
| Docs    | PostgreSQL 16 official documentation                                            |
| Tool    | pgAdmin 4 + `pg_stat_statements` extension                                      |
| Video   | "PostgreSQL Query Optimization" — Hussein Nasser (YouTube)                      |

## Projeto 
### Database Performance Analyser — Query Intelligence CLI

**Tech Stack:** 
	Go + PostgreSQL + `pgx/v5` + SQLite (histórico local)

**Overview**
	Uma ferramenta de linha de comando que se conecta a uma base de dados PostgreSQL existente e produz um relatório completo de performance com recomendações accionáveis — mais útil do que qualquer tutorial porque trabalha com dados reais.
	A ferramenta lê de `pg_stat_statements` as queries mais lentas ou mais frequentes, corre `EXPLAIN ANALYZE` automaticamente em cada uma, **interpreta o query plan** para detectar problemas comuns _(sequential scans em tabelas grandes, nested loop joins sem índice, sorts sem memória suficiente, N+1 patterns por fingerprinting)_, e **sugere os índices específicos que devias criar com o SQL exacto pronto a executar**.
	Para além das queries, a ferramenta detecta índices não usados que estão a desperdiçar espaço, table bloat por excesso de dead tuples, e lock contention por análise de `pg_locks`.
	O output é um relatório estruturado em terminal com código de cores por severidade, exportável como Markdown.

*Output:*

```
=== Performance Report — 2026-06-15 ===
🔴 Critical (3):
  → SELECT * FROM orders WHERE status=? (avg: 2.3s, calls: 12k/day)
    No index on 'status'. Suggested: CREATE INDEX CONCURRENTLY idx_orders_status
  → N+1 pattern detected: 847 similar queries in 10s window
  → Lock contention: orders table locked 340ms avg

🟡 Warning (7):
  → 12 unused indexes consuming ~400MB
  → Table 'events' has 45% dead tuples — VACUUM needed
  → connection pool saturation: 94% avg usage

🟢 OK (12): connection latency, query cache hit rate, replication lag
```

**Core Features**
- Query log parsing de `pg_stat_statements`
- `EXPLAIN ANALYZE` automatizado para as top-N queries lentas
- Slow query detection com threshold configurável
- Index suggestions baseadas em padrões de query
- N+1 detection: agrupa queries similares por fingerprint
- Detecção de table bloat (`pg_relation_size` + dead tuples)
- Unused index report
- Lock contention analysis via `pg_locks`
- Connection pool metrics
## Entregáveis

- [ ] CLI tool open-source no GitHub com README completo
- [ ] Blog: "10 PostgreSQL Performance Problems — How to Find and Fix Them"
- [ ] Video: walkthrough de optimização de uma query real do início ao fim
- [ ] Cheat sheet: índices do PostgreSQL — quando usar qual (PDF)
---
# _**Bônus [03.1]**_

## Modelo C4 & Comunicação Visual de Arquitectura

**Objectivo** 
	Dominar a linguagem visual de arquitectura. Um arquitecto que não consegue comunicar graficamente a sua solução é ineficaz.

### Recursos

| Tipo   | Recurso                                                                                                                      |
| ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Site   | [C4 Model — Simon Brown (c4model.com)](https://c4model.com/) — lê TUDO                                                       |
| Livro  | _Software Architecture for Developers_ — Simon Brown (disponível parcialmente grátis no Leanpub)                             |
| Vídeo  | ["Visualising software architecture with the C4 model" — Simon Brown (YouTube)](https://www.youtube.com/watch?v=x2-rSnhpw0g) |
| Artigo | UML Distilled — Martin Fowler (capítulos sobre diagramas de sequência e componentes)                                         |
| Tool   | [Structurizr Lite](https://structurizr.com/help/lite) — C4 como código, **gratuito**                                         |

### Prática

- Cria os diagramas deste projecto em C4
- Recria os diagramas do projecto anterior em C4 (Context → Container → Component)
- Pratica diagramas de sequência UML para fluxos comuns (login, pagamento, upload)
- Aprende a usar Structurizr DSL para diagramas-como-código

### PROJECTO: _"Sistema de Reservas — C4 Completo"_

**Overview** 
	Desenha a arquitectura de um sistema de reservas de hotel (sem implementar código). Entrega os 4 níveis C4:

- Level 1: Context Diagram
- Level 2: Container Diagram
- Level 3: Component Diagram (para o container principal)
- Level 4: Code Diagram (opcional — apenas classes principais)

**Entrega** 
	Diagramas exportados + documento LaTeX explicando cada decisão em cada nível

# [Parte 1/2]
---
