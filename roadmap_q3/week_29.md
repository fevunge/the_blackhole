# Elixir & Functional Programming — Phoenix LiveView
#week 

## Objectivos

- Elixir: pattern matching, immutability, pipe operator
- OTP: GenServer, Supervisor, Application
- Phoenix: MVC, channels, LiveView
- Ecto: changesets, queries, associations, migrations
- Porque Elixir para real-time: o modelo de actores e BEAM

## Recursos

| Tipo    | Recurso                                                 |
| ------- | ------------------------------------------------------- |
| Livro   | _Programming Elixir 1.6_ — Dave Thomas                  |
| Course  | Elixir School — elixirschool.com (gratuito)             |
| Prática | Exercism Elixir track                                   |
| Docs    | Phoenix Guides — phoenixframework.org                   |
| Video   | "Elixir in 100 Seconds" + "Phoenix LiveView" — Fireship |

## Projeto
### Collaborative Real-time Document Editor (Google Docs básico)

**Tech Stack:** Elixir + Phoenix + LiveView + PostgreSQL (Ecto)

**Overview**
	Um editor de documentos colaborativo em tempo real usando Phoenix LiveView — e o que torna este projecto especialmente interessante é que toda a lógica de colaboração em tempo real acontece no servidor em Elixir sem uma linha de JavaScript custom. LiveView mantém o estado do documento no servidor e sincroniza diffs via WebSocket automático, o que significa que cursors de outros utilizadores, inserções e deleções aparecem em tempo real sem implementares um protocolo de sincronização no frontend. A implementação usa Operational Transformation simplificado para lidar com edições concorrentes: quando dois utilizadores editam o mesmo parágrafo em simultâneo, o servidor resolve o conflito e propaga o resultado correcto. Cada documento é um GenServer Elixir com estado próprio supervisionado pela OTP — se um processo crasha, o supervisor reinicia-o com o estado preservado via PostgreSQL. O Phoenix Presence rastreia quais utilizadores estão activos em cada documento, mostrando os seus avatares e cursors em tempo real. O histórico de versões cria snapshots automáticos a cada 5 minutos.

**Core Features**
- Edição colaborativa em tempo real (Operational Transformation simplificado)
- Presence: avatares dos utilizadores activos no documento
- Cursor tracking: vês onde cada utilizador está a escrever
- Histórico de versões (snapshots automáticos)
- Comentários inline
- Formatação básica: bold, italic, headings, lists
- Export para Markdown e HTML
- Sharing: público, privado, por link com permissão

**Requisitos**
- LiveView faz tudo sem JavaScript custom — o server mantém o estado
- 1M conexões concorrentes num único nó Elixir (BEAM)

```
DocumentSupervisor
├── DocumentServer (GenServer por documento)
│   ├── State: content, users, cursors
│   └── OT: aplica e broadcasting de operações
└── PresenceTracker (Phoenix.Presence)
```


## Entregáveis

- [ ] Editor colaborativo deployado
- [ ] Blog: "Why Phoenix LiveView Changes Everything for Real-time Apps"
- [ ] Video: Dois browsers a editar o mesmo documento em simultâneo
- [ ] Comparison: Elixir/Phoenix vs Node.js/Socket.io para este caso de uso
