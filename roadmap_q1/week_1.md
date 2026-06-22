# TypeScript Avançado + System Design Basics
#s_week 

## Objectivos

- **TypeScript avançado**: Generics, Conditional Types, Mapped Types, Template Literal Types
- **Design Patterns**: Factory, Singleton, Observer, Strategy
- **SOLID principles** — teoria + aplicação prática
- **Git workflow profissional**: conventional commits, semantic versioning, branching strategy

## Recursos

| Tipo    | Recurso                                                   |
| ------- | --------------------------------------------------------- |
| Docs    | TypeScript Handbook — Advanced Types (typescriptlang.org) |
| Livro   | _Design Patterns_ — Gang of Four (caps. 1–3)              |
| Video   | freeCodeCamp — TypeScript Full Course (YouTube)           |
| Prática | github.com/typescript-exercises                           |
| Artigo  | patterns.dev — Lydia Hallie & Addy Osmani (gratuito)      |

## Projeto  [Tache]

### CLI Task Management System com AI Local

**Oveview**
	Sistema de gestão de tarefas de linha de comando com qualidade enterprise — uma developer usaria no dia-a-dia a sério.
	O sistema precisa de **gerir tarefas com prioridades**, **datas**, **tags** e dependências entre si, com persistência em SQLite através do Drizzle ORM.
	A parte que o diferencia: _integração com Ollama para sugestões inteligentes de priorização baseadas nos padrões históricos do utilizador_ — sem custo de API, tudo corre localmente.

**Tech Stack**
	TypeScript + Node.js + SQLite(via Drizzle ORM) + Ollama + Vitest + Commander.js

**Core Features**
- CRUD completo com validação via Zod e schemas tipados
- Task scheduling com cron jobs nativos do Node.js
- Real-time notifications via EventEmitter pattern
- Export/Import em JSON, CSV e Markdown
- Full-text search com índices SQLite FTS5
- Undo/Redo via Command Pattern com histórico ilimitado
- Sugestões de priorização via Ollama (llama3 local — sem API key)
- Métricas de produtividade: tasks/dia, streaks, tempo médio

**Requisitos Técnicos:**
- Clean Architecture rigorosa
- 90%+ test coverage (Vitest — mais rápido que Jest em 2026)
- CI/CD com GitHub Actions
- Semantic versioning + CHANGELOG automático
- Published no NPM como package

**Arquitectura:**
```
src/
├── domain/          # Entities, Value Objects
├── application/     # Use Cases (CQRS básico)
├── infrastructure/  # SQLite, FileSystem, Ollama client
├── presentation/    # CLI Interface (commander.js)
└── shared/          # Utilities, Types
```

**Entregáveis**
- [ ] Package publicado no NPM funcional
- [ ] README profissional com badges de CI, cobertura, versão
- [ ] Blog post no DEV.to explicando arquitectura e decisões
- [ ] Video demo (5min) no YouTube
- [ ] LinkedIn post sobre aprendizados

**Bonús**
- Linter custom (regras de estilo próprias via ESLint plugin)
- Logging estruturado (pino) com níveis configuráveis
---

# _**Bônus [01]**_

## Pensamento de Sistemas & Mindset do Arquitecto

**Objectivo** 
	Mudar o chip de "programador que resolve problemas de código" para "arquitecto que resolve problemas de negócio com tecnologia."

### Recursos

| Tipo   | Recurso                                                                                                                                    |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Livro  | _Thinking in Systems_ — Donella Meadows (caps. 1–4)                                                                                        |
| Livro  | _The Art of Systems Thinking_ — Joseph O'Connor & Ian McDermott (caps. 1–3)                                                                |
| Vídeo  | [Systems Thinking Introduction — MIT OpenCourseWare](https://ocw.mit.edu/courses/15-988-system-dynamics-self-study-fall-1998-spring-1999/) |
| Artigo | "Who Needs an Architect?" — Martin Fowler (martinfowler.com)                                                                               |
| Artigo | "Making Architecture Matter" — Martin Fowler (IEEE Software)                                                                               |
| Canal  | [Mark Richards — YouTube (Software Architecture Monday)](https://www.youtube.com/@markrichards5765)                                        |

### Prática
- Lê _Thinking in Systems_ + cria flashcards Anki dos conceitos-chave (feedback loops, stocks, flows)
- Lê artigos do Fowler + esboça num papel: "Como funciona um sistema que do **projeto** feito e outros parecidos?"
- Analisa 2 arquitecturas reais documentadas publicamente (Netflix Tech Blog, Uber Engineering)
- Trabalha no projecto

### PROJECTO: _"Autopsia de Sistema"_

**Overview**
	Escolhe um sistema real e público (ex: Twitter/X, Spotify, YouTube). Pesquisa a sua arquitectura através de posts de engenharia, talks e artigos públicos. Documenta:
- Que problema de negócio resolve?
- Que decisões de arquitectura foram feitas e porquê?
- Que trade-offs existem?
- Que mudarias com o conhecimento de hoje?

**Entrega** 
	Documento LaTeX (5–8 páginas) + 1 diagrama de alto nível no draw.io

**Fontes para pesquisa:**
- [High Scalability Blog](http://highscalability.com/)
- [The Netflix Tech Blog](https://netflixtechblog.com/)
- [Uber Engineering Blog](https://www.uber.com/en-US/blog/engineering/)

---