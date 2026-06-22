# Go + Concurrency Patterns
#s_week 

## Objectivos

- Go idioms modernos (Go 1.22+): range over integers, structured logging com `slog`
- Goroutines e channels — lifecycle, garbage collection, leak detection
- `context` package — propagação de cancelamento e deadlines em profundidade
- `sync` package: Mutex, RWMutex, WaitGroup, Pool, Once
- Concurrency patterns: Fan-in, Fan-out, Pipeline, Worker Pool, Semaphore, Circuit Breaker
- Graceful shutdown com `os.Signal` e `context.WithCancel`
## Recursos

| Tipo    | Recurso                                               |
| ------- | ----------------------------------------------------- |
| Livro   | _Concurrency in Go_ — Katherine Cox-Buday             |
| Course  | Learn Go with Tests — quii.gitbook.io (100% gratuito) |
| Prática | Exercism Go track                                     |
| Blog    | Official Go Blog — go.dev/blog                        |
| Video   | "Concurrency is not Parallelism" — Rob Pike (YouTube) |

## Projeto
## Distributed Web Crawler com Pipeline Architecture

**Tech Stack**
	Go (modern) + Redis + PostgreSQL + colly

**Overview**
	Um Web Crawler distribuído _**production-ready**_, que consegue processar centenas de URL's por segundo de forma concorrente e respeitosa com os servidores-alvo.
	O sistema tem de ser construído como um **pipeline de goroutines com backpressure**: _um Frontier_ mantém a fila de URL's a visitar em Redis, _um pool de Fetcher goroutines_ descarrega o HTML de forma concorrente com rate limiting por domínio, _um pool de Parser goroutines_ extrai links e texto, e _um Storage Worker_ persiste o link graph no PostgreSQL.
	O diferencial técnico está em dois lugares: 
	- primeiro, **implementas um Bloom Filter do zero** (não importas uma biblioteca) para reduplicação de URLs em memória com zero false negatives; 
	- segundo, implementas o protocolo `robots.txt` completo incluindo `Crawl-delay`.
	O sistema é resumível — podes parar e retomar sem perder estado.
	O projecto termina com benchmarks de URLs processadas por segundo em função do número de workers, e um diagrama detalhado das decisões de arquitectura do pipeline.

**Core Features**
- Concurrent crawling com goroutine pool de tamanho configurável
- Bloom filter implementado do zero (não biblioteca)
- `robots.txt` parsing completo com `Crawl-delay`
- Rate limiting por domínio: token bucket com Redis
- HTML parsing + extracção de links, texto, metadata OpenGraph
- Resumable crawling: estado persistido no Redis
- `context` propagation para cancelamento limpo de toda a pipeline
- Link graph storage (adjacency list no PostgreSQL)
- Métricas em tempo real: URLs/segundo, erros, queue depth
- Circuit breaker por domínio: pausa quando error rate > threshold
- Lidar com redireccionamentos circulares
- Backpressure quando o storage é mais lento que o fetch

**Arquitectura**

```
Seed URLs → Frontier (Redis Queue)
               ↓
         Fetcher Pool (N goroutines com rate limit por domínio)
               ↓
         Parser Pool (M goroutines)
               ↓
         Storage Worker → PostgreSQL (link graph)
               ↓
         Robots Cache (Redis) ← consultado antes de cada fetch
```

**Entregáveis**
- [ ] CLI tool funcional com flags configuráveis
- [ ] Benchmark: URLs processadas por segundo com N workers (gráfico)
- [ ] Blog: "Building a Production Web Crawler in Go — Concurrency Patterns Explained"
- [ ] Diagrama de arquitectura do pipeline com decisões justificadas
---
# _**Bônus [02]**_

## Fundamentos de Arquitectura de Software

**Objectivo**
	Dominar os estilos arquitecturais clássicos e modernos, e saber quando aplicar cada um.

### Recursos

| Tipo   | Recurso                                                                                                          |
| ------ | ---------------------------------------------------------------------------------------------------------------- |
| Livro  | _Fundamentals of Software Architecture_ — Mark Richards & Neal Ford (caps. 1–8) — **O livro central do roadmap** |
| Vídeo  | [Mark Richards — Architectural Patterns Playlist (YouTube)](https://www.youtube.com/@markrichards5765)           |
| Artigo | "Microservices" — Martin Fowler & James Lewis (martinfowler.com)                                                 |
| Artigo | "Monolith First" — Martin Fowler (martinfowler.com)                                                              |
| Site   | [Software Architecture Guide — martinfowler.com](https://martinfowler.com/architecture/)                         |

### Prática Diária

- Cria um "cheat sheet" comparativo: Monolito vs SOA vs Microserviços vs Event-Driven
- Para cada estilo: desenha um diagrama de exemplo no draw.io
- Adiciona 10 flashcards Anki por dia sobre padrões arquitecturais

### PROJECTO: _"Arquitectura Decision Record (ADR) — Escolhe o Estilo"_

**Overview**
	Recebe este brief fictício de cliente:

> _"Somos uma startup de e-commerce com 2 programadores. Temos 500 utilizadores por dia mas queremos crescer para 50.000 em 1 ano. Precisamos de um sistema de vendas, inventário e notificações."_

Produz um ADR completo justificando a arquitectura escolhida. Mínimo 3 alternativas comparadas.

**Entrega** 
	Documento LaTeX usando o template de ADR + diagramas C4 Level 1 e Level 2
