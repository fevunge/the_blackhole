# PROJECTO INTEGRADOR — AI-Powered Developer Platform
#week 

## Projeto
### AI Developer Platform — Codespaces + AI Assistant

**Overview**
	Vais construir uma plataforma de desenvolvimento cloud com um AI assistant integrado — o tipo de produto que o GitHub Codespaces combinado com GitHub Copilot representa, mas construído por ti com componentes que já construíste ao longo do roadmap. O Workspace Service em Go usa o Docker SDK para criar e gerir ambientes de desenvolvimento isolados — cada workspace é um container com a stack correcta, persistent volumes para os ficheiros, e exposição de portas configurável. O AI Assistant Service em Python usa Ollama com o modelo `deepseek-coder` ou `codellama` para code completion contextual (envia o ficheiro aberto + cursor position), explain selected code em linguagem simples, generate tests para a função seleccionada, e "fix this error" com o stack trace como input. A edição colaborativa em tempo real usa Phoenix LiveView ([[week_29]]) para múltiplos cursors. O frontend tem o Monaco Editor (o editor do VS Code na web), terminal integrado com xterm.js conectado via WebSocket ao container, e um file explorer. A infraestrutura Kubernetes ([[week_27]]) isola workspaces em namespaces separados com resource quotas.

**Tech Stack**
	Full-stack multi-language

**Backend Services:**
- **Workspace Service** (Go): cria e gere ambientes de desenvolvimento em Docker
- **AI Assistant Service** (Python + Ollama): code completion, explanation, review
- **Storage Service** (Go + MinIO): ficheiros de projectos
- **Collaboration Service** (Elixir + Phoenix): edição colaborativa em tempo real

**Frontend (React + TypeScript):**
- Monaco Editor (o editor do VS Code na web)
- Terminal integrado (xterm.js)
- File explorer
- AI chat sidebar

**AI Features (com Ollama local — gratuito):**
- Code completion (modelo `codellama` ou `deepseek-coder`)
- Explain selected code
- Generate tests para função seleccionada
- Code review automático ao fazer commit
- "Fix this error" — cola o stack trace, recebe sugestão

**Infraestrutura:**
- Kubernetes: cada workspace é um Pod isolado
- Namespace per user para isolamento
- Resource quotas (CPU/memory por workspace)
- Persistent volumes para projectos

## Entregáveis

- [ ] Platform funcionando em cluster local (k3d)
- [ ] Blog series (5 posts): Workspace Service / AI Integration / Collaborative Editing / Kubernetes Setup / Production Lessons
- [ ] YouTube: demo completo — cria workspace, escreve código com AI, faz deploy
- [ ] Technical whitepaper
