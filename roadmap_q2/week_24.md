 
# Game Engine — ECS Architecture & 2D Engine
#s_week 

## Objectivos

- Game loop: fixed timestep vs variable timestep — porquê o fixed timestep é obrigatório para física
- Entity-Component-System (ECS): data-oriented design vs object-oriented — performance implications
- Physics 2D: integração de Verlet, detecção de colisões AABB, collision response
- Spatial partitioning: quadtrees e spatial hashing para broad phase
- Asset pipeline: loading, caching com reference counting, hot-reload em debug

## Recursos

| Tipo   | Recurso                                                 |
| ------ | ------------------------------------------------------- |
| Livro  | _Game Engine Architecture_ (3ª edição) — Jason Gregory  |
| Series | The Cherno — "Game Engine" series (YouTube)             |
| Lib    | raylib.com — biblioteca C simples, ideal para aprender  |
| Artigo | "ECS Back and Forth" — skypjack.github.io (entt author) |
| Código | github.com/skypjack/entt — ler o código é educativo     |

## Projeto
### 2D Game Engine com ECS + Roguelite Demo Game

**Tech Stack**
	C++20 + raylib + Box2D 3.0 + entt

**Overview**
	Um game engine 2D com arquitectura ECS e um jogo demo completo e jogável que prova que a engine funciona para um jogo real — não apenas um demo técnico vazio. A engine usa entt como biblioteca ECS (ler o código do entt é por si só educativo) e expõe sistemas bem definidos: Rendering System para sprites, tilemaps animados e particle systems; Physics System com Box2D 3.0 para collision detection e response realista; Input System com abstracção que suporta teclado, rato e gamepad; Audio System com pool de sons; Animation System com sprite sheet state machine; AI System com behaviour trees básicas para inimigos; e Resource System com hot-reload em modo debug para iterar sem reiniciar o jogo. O jogo demo é um roguelite 2D: dungeons geradas proceduralmente via BSP (Binary Space Partitioning), player com dash e ataque melee/ranged, 3 tipos de inimigos com AI diferente (melee agressivo, ranged que mantém distância, suicida), sistema de loot com raridades, câmera com screen shake e zoom dinâmico, e UI com health bar, inventory e minimap. O jogo é publicado no itch.io via export Emscripten para o browser.


**Core Features**
- Rendering System   → draw sprites, tilemaps, particles
- Physics System     → Box2D integration, collision callbacks
- Input System       → keyboard, mouse, gamepad abstraction
- Audio System       → raylib audio + pool de sons
- Animation System   → sprite sheet animation, state machine
- AI System          → behaviour trees básicas (para enemies)
- Scene System       → load/unload scenes, entity spawning
- Resource System    → asset cache com hot-reload em debug
- **Demo Game — Roguelite 2D:**
	- Geração procedural de dungeons (BSP rooms)
	- Player com dash, ataque melee, ranged
	- 3 tipos de inimigos com AI diferente
	- Sistema de loot
	- Câmera com shake e zoom dinâmico
	- UI: health bar, inventory, minimap

**Requisitos**
- Hot-reload de assets sem reiniciar o jogo (produtividade de desenvolvimento)
- Profiler integrado (frame time, system times)

## Entregáveis

- [ ] Engine + jogo compilável com CMake
- [ ] Jogo publicado no itch.io (export para browser via Emscripten)
- [ ] Blog: "Building a 2D Game Engine with ECS in C++20"
- [ ] Video: Engine architecture + gameplay demo

---

# _**Bônus [09]**_

## Enterprise Architecture & TOGAF (Conceitos)

**Objectivo** 
	Compreender como arquitectura de software se enquadra na arquitectura empresarial.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                                             |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Livro  | _Enterprise Architecture as Strategy_ — Ross, Weill & Robertson (caps. 1–4)                                                                         |
| Artigo | TOGAF Standard Overview — The Open Group (gratuito online)                                                                                          |
| Vídeo  | ["What is Enterprise Architecture?" — The Open Group (YouTube)](https://www.youtube.com/results?search_query=what+is+enterprise+architecture+TOGAF) |
| Livro  | _Software Systems Architecture_ — Rozanski & Woods (caps. 1–5) — excelente sobre viewpoints                                                         |

### PROJECTO: _"Architecture Vision Document"_

**Overview** 
	Para uma organização fictível de média dimensão (ex: cadeia de retalho, hospital, banco regional), cria um Architecture Vision Document contemplando:

- Business Architecture (processos de negócio)
- Data Architecture (dados críticos e fluxo)
- Application Architecture (sistemas e integrações)
- Technology Architecture (infraestrutura)

**Entrega** 
	Documento LaTeX profissional de 10–15 páginas com diagramas

---
