# PROJECTO INTEGRADOR — Multiplayer Game Platform
#s_week 

## Projeto 
### Real-time Multiplayer Gaming Platform

**Tech Stack**
- **Engine:** C++20 + raylib ([[week_24]]) → compilado para Wasm com Emscripten
- **Backend:** Rust + Axum + WebSocket ([[week_17]])
- **Auth:** Sistema da [[week_7]] (Passkeys + OAuth)
- **DB:** PostgreSQL + Redis
- **Frontend:** React (lobby, perfil, leaderboard — a engine corre no Canvas)

**Overview**
	Uma plataforma completa de jogos multiplayer em tempo real onde o código dos jogos corre no browser via WebAssembly (compilado de C++) e o servidor autoritativo está em Rust com WebSocket — a arquitectura que plataformas de jogos reais usam. 
	A engine C++ da [[week_24]] é compilada para Wasm com Emscripten e corre no browser Canvas, enquanto o servidor Rust com Axum mantém o estado autoritativo de cada partida e faz broadcast para todos os clientes.
	O protocolo de rede usa client-side prediction — o cliente executa a lógica localmente para resposta imediata — e server reconciliation para corrigir divergências.
	Implementas três jogos: **Pong Multiplayer** (2 jogadores, física simples), **Snake Battle** (até 4 jogadores com power-ups), e **Tetris Attack** (manda linhas para o adversário).
	A plataforma inclui um sistema de matchmaking com ELO rating por jogo, lobby com chat em tempo real, spectator mode via WebTC data channels, replay system que guarda os inputs e reproduz no cliente, leaderboard global e por amigos, e um sistema de achievements com critérios configuráveis. O desafio técnico mais interessante é o lag compensation: o servidor mantém um histórico de estados para fazer hit detection justo quando há latência.

**Jogos:**

1. **Pong Multiplayer** — clássico, 2 jogadores
2. **Snake Battle** — até 4 jogadores, power-ups
3. **Tetris Attack** — manda linhas para o adversário

**Arquitectura de Rede (Authoritative Server):**

```
Client (Wasm) → WebSocket → Game Server (Rust)
                                  ↓
                          State Broadcast
                                  ↓
                     Client-side Prediction + Reconciliation
```

**Core Features**

- Matchmaking com ELO rating por jogo
- Spectator mode
- Chat em tempo real (durante o jogo e no lobby)
- Replay system (guarda inputs, reproduz no cliente)
- Leaderboard global e por amigos
- Achievements com critérios configuráveis
- Torneiro system: brackets automáticos

**Requisitos**

- Client-side prediction: o cliente antecipa o servidor
- Server reconciliation: corrige o estado do cliente quando diverge
- Lag compensation: histórico de estados para hit detection justo
- UDP-like sobre WebSocket: mensagens não críticas sem ACK

## Entregáveis

- [ ] Platform completa e jogável (URL pública)
- [ ] Blog series (4 posts): Network Protocol / Client Prediction / Engine Architecture / Optimization
- [ ] YouTube: Gameplay demo + code review do sistema de rede
- [ ] itch.io: release pública dos jogos
- [ ] Whitepaper técnico: decisões de arquitectura

---
# _**Bônus [06]**_

## Microserviços & Event-Driven Architecture

**Objectivo** 
	Dominar os padrões modernos de decomposição de sistemas.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                                 |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| Livro  | _Building Microservices_ — Sam Newman (2ª edição) (caps. 1–8)                                                                           |
| Livro  | _Designing Event-Driven Systems_ — Ben Stopford (gratuito no Confluent website)                                                         |
| Vídeo  | ["GOTO 2019 — "The Many Meanings of Event-Driven Architecture"" — Martin Fowler (YouTube)](https://www.youtube.com/watch?v=STKCRSUsyP0) |
| Artigo | "Saga Pattern" — Chris Richardson (microservices.io)                                                                                    |
| Site   | [microservices.io](https://microservices.io/) — catálogo completo de padrões, por Chris Richardson                                      |

### PROJECTO: _"Decomposição de Monólito em Microserviços"_

**Overview** 
	Parte de um projeto web open-source monólito do github. Faz um fork aplicando a técnica Strangler Fig Pattern para decompor gradualmente em micro serviços. Documenta:

- Identificação de bounded contexts
- Estratégia de decomposição (por domínio, capacidade, etc.)
- Gestão de dados distribuídos (cada serviço tem a sua DB)
- Comunicação: sync (REST/gRPC) vs async (eventos)
- Padrão Saga para transacções distribuídas

**Entrega** 
	Documento LaTeX + diagramas C4 antes/depois + diagrama de eventos

