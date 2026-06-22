# Real-time Multiplayer Platform (Enhanced)
#week 

### Gaming Platform com 4 Jogos + Sistema de Torneios

**Tech Stack:**
- Engine (C++20 + Emscripten → Wasm) — reutiliza [[week_26]]
- Backend (Rust + Axum + WebSocket) — reutiliza [[week_26]]
- Streaming: WebRTC para spectators
- Novos: sistema de torneios + betting com moeda virtual

**Overview**
	Vais evoluir a plataforma de jogos multiplayer da semana 26 adicionando um sistema de torneios com brackets automáticos, live spectating via WebRTC para zero latência, e um sistema de clan wars. O sistema de torneios suporta dois formatos: Single Elimination com brackets automáticos gerados após registo, e Swiss System onde cada jogador encontra adversários com score similar — o Swiss é matematicamente mais justo para determinar o melhor jogador sem eliminar ninguém cedo demais. O live spectating usa WebRTC data channels para retransmitir o estado do jogo com menos de 100ms de latência para até 100 spectators simultâneos sem passar pelo servidor autoritativo — os clientes dos spectators recebem o game state directamente do cliente do jogador via P2P mesh gerido pelo servidor de sinalização. O replay system guarda todos os inputs com timestamps e reproduz-os no cliente usando a mesma engine determinística — o que significa que podes saltar para qualquer momento de uma partida. O clan system permite grupos de 10+ jogadores, Wars entre clans com pontuação acumulada, e leaderboard de clans global.

**Novidades:**

- 1. Pong (classic), Snake multiplayer, Tetris battle, Card game (simple)
- 2 novos jogos (escolha: Breakout 1v1, Connect Four, Wordle Battle)
- Tournament brackets automáticos com Swiss ou Single Elimination
- Live spectating via WebRTC (zero latência para 100 spectators)
- Replay system: guarda inputs → reproduz server-side
- Clan system: grupos de jogadores, wars entre clans
- In-game economy: moeda virtual por ganhar partidas, gastar em cosmetics

## Entregáveis
- [ ] Platform completa e melhorada (URL pública)
- [ ] Blog: "WebRTC for Game Spectating — Architecture and Challenges"
- [ ] Video: torneio ao vivo com spectators
