# Rust Advanced — Async, Tokio & Actor Model
#week 

## Objectivos
- `async`/`await` — como funciona por baixo: Futures, polling, wakers, executors
- Tokio runtime: tasks, `spawn`, `spawn_blocking`, canais typed e untyped
- `tokio::select!` — multiplexing de futures com cancellation
- Actor model com channels Tokio — alternativa sem framework
- Lock-free data structures: `DashMap`, `crossbeam-channel`
- Backpressure e bounded channels

## Recursos

| Tipo    | Recurso                                                          |
| ------- | ---------------------------------------------------------------- |
| Livro   | _Async Rust_ — gratuito em rust-lang.github.io/async-book        |
| Docs    | Tokio tutorial — tokio.rs/tokio/tutorial                         |
| Video   | Jon Gjengset — "Implementing Futures from Scratch" (YouTube)     |
| Blog    | fasterthanlime.com — posts sobre async Rust                      |
| Prática | Tokio exercises — github.com/tokio-rs/tokio/tree/master/examples |
## Projeto
### Distributed Task Queue System — Zero-Cost Job Processing

**Tech Stack** 
	Rust + Tokio + Axum + Redis + PostgreSQL + Prometheus
	
**Overview**
	Um sistema de filas de tarefas distribuído em Rust usando o modelo de actores — o tipo de sistema que o BullMQ ou o Celery implementam, mas com as garantias de segurança e a performance de Rust. O sistema usa actores Tokio (não o framework Actix — implementas actores com channels e tasks puras) para isolar responsabilidades: um Queue Actor gere o ciclo de vida dos jobs e expõe uma API Axum; Worker Actors processam os jobs em paralelo com pool dinâmico que escala com a carga; um Scheduler Actor gere jobs cron-based e delayed; um Storage Actor abstrai Redis (estado runtime) e PostgreSQL (persistência); e um Metrics Actor exporta métricas Prometheus. O sistema garante at-least-once delivery, suporta idempotency keys para semântica exactly-once quando o worker é idempotente, e faz retry com exponential backoff com jitter. Jobs cancelados têm graceful cancellation via `CancellationToken`. O benchmarking final compara throughput (jobs/segundo) e latência contra BullMQ em Node.js e Celery em Python nas mesmas condições.

**Core Features**
- Job scheduling: imediato, delayed, cron-based
- Priority queues com N prioridades configuráveis
- Retry com exponential backoff + jitter
- Dead letter queue com reprocessamento manual
- Worker pool dinâmico (escala com a carga)
- Job cancellation e timeout
- Progress tracking em tempo real (SSE)
- Rate limiting por job type com token bucket
- Métricas Prometheus: throughput, latência, error rate

```
Client API (Axum)
     ↓
Queue Actor (job lifecycle)
     ↓              ↓
Worker Actors    Scheduler Actor
     ↓              ↓
Storage Actor (Redis hot + PostgreSQL persistence)
     ↓
Metrics Actor (Prometheus exporter)
```

**Requisitos**
- At-least-once delivery
- Idempotency keys para exactly-once semântico
- Graceful shutdown: drain da queue antes de sair
- Error handling robusto

## Entregáveis

- [ ] Crate no crates.io com documentação completa
- [ ] Benchmark: jobs/segundo vs BullMQ vs Celery (gráfico comparativo)
- [ ] Blog: "Building a Distributed Task Queue in Rust with the Actor Model"
- [ ] Video: arquitectura + demo de workers a processar jobs em paralelo