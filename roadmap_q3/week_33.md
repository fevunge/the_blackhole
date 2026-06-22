# Distributed Systems Avançados — CQRS, Event Sourcing & Sagas
#week 

## Objectivos
- Event sourcing: o estado como sequência de eventos imutáveis
- CQRS: separação de reads e writes — quando faz sentido
- Saga pattern: transacções distribuídas sem 2PC
- Outbox pattern: garantia de entrega de eventos
- Idempotency: processa o mesmo evento múltiplas vezes sem efeitos colaterais

## Recursos

| Tipo   | Recurso                                                           |
| ------ | ----------------------------------------------------------------- |
| Livro  | _Designing Data-Intensive Applications_ — Kleppmann (caps. 11-12) |
| Artigo | "Event Sourcing" + "CQRS" — Martin Fowler (martinfowler.com)      |
| Artigo | "Saga Pattern" — Chris Richardson (microservices.io)              |
| Video  | "GOTO 2014: Event Sourcing" — Greg Young (YouTube)                |
| Course | MIT 6.824 — lectures gratuitas no YouTube                         |

## Projeto
### E-commerce Backend com Event Sourcing + Saga

**Tech Stack**
	Go + PostgreSQL + Kafka (ou NATS JetStream — mais leve) + Redis

**Overview**
	O backend de um sistema de e-commerce usando Event Sourcing e Saga pattern — dois dos padrões mais importantes e mal compreendidos de sistemas distribuídos. Event Sourcing significa que o estado de uma encomenda não é guardado directamente; em vez disso, guardas a sequência de eventos que aconteceram (OrderCreated, PaymentConfirmed, OrderShipped, OrderCancelled) e reconstructes o estado actual fazendo replay desses eventos — o que dá auditoria gratuita, time travel para qualquer ponto no histórico, e a capacidade de adicionar novos read models sem migrar dados. O Saga pattern resolve o problema de transacções distribuídas sem Two-Phase Commit: quando uma encomenda é criada, uma série de passos acontecem em serviços diferentes (Order → Inventory → Payment → Notification), e se algum passo falha, as transacções compensadoras desfazem os passos anteriores. O Outbox Pattern garante que eventos são sempre publicados mesmo se o message broker falhar momentaneamente — o evento é escrito na mesma transacção de base de dados e publicado depois. O projecto inclui demonstração obrigatória de uma falha de pagamento e a compensação automática que liberta o stock reservado.

**Core Features**
- E-Commerce all features + bônus 

**Requisitos:**
- **Order Service**: cria e gere encomendas
- **Inventory Service**: reserva e confirma stock
- **Payment Service**: processa pagamentos (simulado)
- **Notification Service**: envia emails (simulado)

- **Event Sourcing:**

```go
// Todos os estados são derivados de eventos
type OrderEvent interface { isOrderEvent() }

type OrderCreated struct { OrderID, UserID string; Items []Item }
type PaymentConfirmed struct { OrderID, PaymentID string }
type OrderShipped struct { OrderID, TrackingCode string }
type OrderCancelled struct { OrderID, Reason string }

// Estado actual = replay de todos os eventos
func (o *Order) Apply(event OrderEvent) {
    switch e := event.(type) {
    case OrderCreated: o.Status = "pending"; o.Items = e.Items
    case PaymentConfirmed: o.Status = "paid"
    // ...
    }
}
```

- **Saga (Choreography-based):**

```
CreateOrder → OrderCreated event
                    ↓
              InventoryService: ReserveStock
                    ↓ (success)
              PaymentService: ProcessPayment
                    ↓ (success)
              NotificationService: SendConfirmation
                    ↓ (failure anywhere)
              Compensating transactions: ReleaseStock, RefundPayment
```

- **Outbox Pattern:** garante que eventos são publicados mesmo se o broker falhar.

## Entregáveis

- [ ] Sistema completo funcional com 4 serviços
- [ ] Blog: "Event Sourcing and Saga Pattern — When Your Distributed Transaction Goes Wrong"
- [ ] Diagram: fluxo completo de uma encomenda com sucesso e com falha
- [ ] Video: demonstração de uma falha de pagamento e compensação automática
