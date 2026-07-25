# Distributed Systems Fundamentals
#week 

## Objectivos

- CAP theorem — o que significa realmente na prática e porque é uma simplificação
- Consensus algorithms: Raft em profundidade (mais prático e legível que Paxos)
- Consistent hashing — como os load balancers e caches distribuídas funcionam
- Replication: single-leader, multi-leader, leaderless — trade-offs reais
- Eventual consistency vs strong consistency — como escolher para cada sistema
- Vector clocks e causalidade em sistemas distribuídos

## Recursos

| Tipo    | Recurso                                                                                          |
| ------- | ------------------------------------------------------------------------------------------------ |
| Livro   | _Designing Data-Intensive Applications_ — Martin Kleppmann (caps. 5-9) — o livro mais importante |
| Paper   | "In Search of an Understandable Consensus Algorithm" — Ongaro & Ousterhout (Raft)                |
| Paper   | "Raft Consensus Algorithm"                                                                       |
| Course  | MIT 6.824 Distributed Systems — lectures gratuitas no YouTube                                    |
| Site    | martin.kleppmann.com — posts complementares ao livro                                             |
| Prática | github.com/pingcap/talent-plan — TiKV labs em Go/Rust                                            |

## Projeto
### Distributed Key-Value Store com Raft Consensus

**Tech Stack** 
	Go + `hashicorp/raft` + gRPC + protobuf

**Overview**
	Um distributed key-value store com consensus Raft — basicamente um mini-etcd, o sistema que o Kubernetes usa internamente para armazenar todo o estado do cluster.
	Este é o projecto que separa quem percebe verdadeiramente de distributed systems de quem apenas leu sobre o tema.
	Tens de implementar **leader election**, **log replication**, e **snapshot-based log compaction** de acordo com o paper original do Raft.
	O sistema precisa de correr em 3 nós Docker, sobreviver à perda do leader (eleição nova em menos de 1 segundo), rejeitar escritas quando um nó está isolado em network partition, e quando um nó reúne-se ao cluster após isolamento, tem de fazer catch-up via snapshot sem perder dados.
	O cliente expõe operações GET, SET, DELETE e SCAN via gRPC, mais uma Watch API que notifica subscribers quando uma key muda. Testa obrigatoriamente os cenários de falha: **leader crash**, **network partition de um nó**, e **rejoin após isolamento**.
	É o projecto mais difícil de Q1 — começa pela implementação do paper antes de qualquer outra coisa.

**Core Features**
- Key-value operations: `GET`, `SET`, `DELETE`, `SCAN`
- Distributed consensus via Raft (leader election automático)
- Replication para mínimo 3 nós
- Cluster membership: adicionar/remover nós em runtime
- Failure detection com heartbeats
- Log replication e compaction via snapshots
- Watch API: subscribe a changes numa key (como etcd)
- CLI client e REST API

**Requisitos Técnicos**
- Leader failure → election completa em <1s
- Network partition → nó isolado rejeita writes (strong consistency)
- Node rejoin → catch up via snapshot sem perder dados
- Split brain → não deve acontecer com Raft (verifica e documenta)
- Handle network partitions
- Consistency guarantees
- Performance under load
- Membership changes

**Entregáveis**
- [ ] Sistema funcional (3 nós via Docker Compose)
- [ ] Blog: "Implementing Raft Consensus — What the Paper Doesn't Tell You"
- [ ] Diagrama: leader election e log replication passo a passo
- [ ] Video: demonstração de leader election ao vivo com logs visíveis

---
# _**Bônus [05]**_
