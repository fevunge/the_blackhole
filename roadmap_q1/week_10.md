#  Docker & Containerization
#week 

## Objectivos
- Docker architecture: daemon, containerd, runc — camadas de abstracção
- Dockerfile best practices: multi-stage builds, layer caching, .dockerignore
- Docker Compose v2 — sintaxe moderna e diferenças do v1
- Networking em Docker: bridge, host, overlay — quando usar cada um
- Volumes, bind mounts, tmpfs — persistência e performance
- Container security: rootless containers, capabilities, seccomp profiles

## Recursos

| Tipo    | Recurso                                                      |
| ------- | ------------------------------------------------------------ |
| Docs    | Docker official documentation — docs.docker.com              |
| Video   | TechWorld with Nana — Docker Crash Course (YouTube)          |
| Artigo  | "Docker Security Best Practices" — Snyk blog                 |
| Prática | Play with Docker — labs.play-with-docker.com (gratuito)      |
| Tool    | Dive — github.com/wagoodman/dive (analisa layers de imagens) |
## Projeto
### Dev Environment Orchestrator CLI

**Tech Stack**
	Go + Docker SDK + Docker Compose + cobra (CLI framework)

**Overview**
	Uma CLI em Go que cria e gere ambientes de desenvolvimento completos com um único comando — o tipo de ferramenta que toda a equipa usa mas ninguém constrói porque parece demasiado simples até perceberes o que é necessário para funcionar bem. A ferramenta precisa de detectar automaticamente o tipo de projecto (lendo `package.json`, `Cargo.toml`, `go.mod`, `pyproject.toml`, `requirements.txt`) e criar o ambiente Docker correspondente sem configuração manual.
	Para um projecto TypeScript, levanta automaticamente Node.js, PostgreSQL e Redis com as versões correctas, healthchecks inteligentes antes de marcar como "ready", e port collision detection para evitar conflitos com outros projectos que possas ter em execução.
	O sistema de snapshots permite guardar e restaurar o estado da base de dados durante desenvolvimento, e os profiles (dev, test, staging) têm configurações diferentes como volumes, variáveis de ambiente e réplicas.
	A experiência de developer tem de ser tão simples que um colega sem experiência Docker consiga usar a ferramenta sem documentação.

**Core Features**
- Templates de projetos (React, Node, Python, etc)
- One-command setup (DB + Cache + App)
- Hot reload configuration
- Logs aggregation
- Backup/restore de volumes
- Network isolation
- Detecção automática do projecto (lê package.json, Cargo.toml, go.mod)
- Health checks inteligentes antes de marcar como "ready"
- Port collision detection automática
- Profiles: `dev`, `test`, `staging` com configs diferentes

```bash
devup init react-fullstack    # detecta e cria o ambiente
devup start                   # inicia com healthchecks
devup logs api --follow       # logs em tempo real
devup db shell                # psql no container directamente
devup snapshot save backup1   # guarda estado da DB
devup snapshot restore backup1
devup clean --keep-data       # remove containers, preserva dados
```

**Requisitos Técnicos(templates)**
- TypeScript + Hono + PostgreSQL + Redis
- React + Vite + API backend
- Python + FastAPI + PostgreSQL
- Go microservices (3 serviços + API gateway)
- Rust + Axum + PostgreSQL

**Entregáveis**
- [ ] CLI com binários para Linux/macOS/Windows via GitHub Releases
- [ ] Blog: "Replacing docker-compose run with a Smart CLI in Go"
- [ ] YouTube: "Setup a Full Dev Environment in 30 Seconds"
- [ ] Collection de templates no repositório
