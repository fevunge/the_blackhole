# PROJECTO INTEGRADOR — Plataforma SaaS Segura
#s_week 

## Objectivo

Integrar TODOS os conhecimentos de Q1 num sistema real de nível production.

# Projeto
### Multi-tenant SaaS Platform — Project Management Tool

**Tech Stack**
- **Frontend:** React 19 + TypeScript + Tailwind CSS + TanStack Query
- **Backend:** Node.js + Hono + TypeScript(usando a API da [[week_2]])
- **Auth:** Microservice da [[week_7]]
- **Database:** PostgreSQL (row-level security) applicado lições da [[week_7]]
- **Cache:** Redis (sessões + rate limiting)
- **Storage:** MinIO (local S3-compatible)
- **Infra:** Docker Compose (usando orchestrator da [[week_10]])
- **Monitoring:** Agente da [[week_11]]

**Overview**
	Uma plataforma SaaS de gestão de projectos multi-tenant — tipo um Jira simplificado mas construído com os padrões de qualidade, segurança e observabilidade que aprendeste durante as 12 semanas anteriores. 
	Multi-tenant significa que organizações diferentes partilham a mesma infraestrutura mas com isolamento total de dados — implementas isso via row-level security no PostgreSQL onde cada query inclui automaticamente o `organization_id` via middleware, tornando impossível a um tenant aceder aos dados de outro mesmo que haja um bug na lógica de negócio. A plataforma tem projects, boards e tasks com drag-and-drop, sistema de comentários com menções, file attachments via MinIO (S3-compatible local), notificações em tempo real via Server-Sent Events, e um analytics dashboard com burn-down charts e métricas de velocity. A infra usa o Docker orchestrator que construíste na [[week_10]], o auth platform da [[week_7]] para autenticação, o PostgreSQL optimizado da [[week_6]] para queries, e o agente de monitoring da [[week_11]] para observabilidade. O CI/CD corre lint, testes unitários, testes de integração, testes E2E com Playwright, e um OWASP ZAP scan automatizado. O sistema vai para produção no Render free tier com SSL automático.

**Core Features**

- Multi-tenancy com row-level security no PostgreSQL
- Projects, Boards, Tasks com drag-and-drop
- Assignments, due dates, priorities, labels
- Comentários, file attachments, notificações em tempo real (SSE)
- Analytics: burn-down charts, velocity, cycle time
- Admin panel com RBAC granular
- Notificações em tempo real (Server-Sent Events)
- Audit log completo de todas as acções

**Requisitos**
- Todas as vulnerabilidades da [[week_12]] mitigadas
- Tenant isolation: row-level security no PostgreSQL
- Security headers completos
- Rate limiting por utilizador e por organização
- Input validation rigorosa em todos os endpoints
- Audit log imutável
- Unit tests: 90%+ coverage
- Integration tests: todos os endpoints críticos
- E2E: Playwright (login, criar task, assign, comentar)
- Security: OWASP ZAP scan no CI
- Load: k6 simulando 100 utilizadores simultâneos
- Docker Compose para desenvolvimento
- CI/CD com Jenkins lint → test → build → deploy
- Deploy no Render free tier (produção acessível)
- SSL/TLS automático (Let's Encrypt)
- Monitoring com o agente da [[week_11]]

**Entregáveis**
- [ ] Sistema completo em produção (URL pública)
- [ ] README profissional com arquitectura, setup e decisões
- [ ] Architecture Decision Records (3+ ADRs)
- [ ] Security audit report
- [ ] Blog series (3 posts): Arquitectura / Segurança / Performance
- [ ] YouTube: Walkthrough completo (15-20min)
- [ ] Pentest report

---
 
# _**Bônus [04]**_
## Design Patterns & Princípios SOLID/DDD

**Objectivo** 
	Compreender os padrões de design que informam decisões arquitecturais.

## Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                                       |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Livro  | _Design Patterns: Elements of Reusable Object-Oriented Software_ — Gang of Four (caps. seleccionados: Factory, Observer, Strategy, Decorator) |
| Livro  | _Domain-Driven Design: Tackling Complexity in the Heart of Software_ — Eric Evans (Parte 1)                                                   |
| Vídeo  | ["Domain Driven Design: The Good Parts" — Jimmy Bogard (YouTube)](https://www.youtube.com/watch?v=U6CeaA-Phqo)                                |
| Artigo | "SOLID Principles" — Robert C. Martin (Wikipedia + blog posts originais)                                                                      |
| Site   | [Refactoring.Guru — Design Patterns](https://refactoring.guru/design-patterns) — **excelente recurso visual gratuito**                        |

### PROJECTO: _"DDD para um Domínio Real"_

**Overview** 
	Aplica Domain-Driven Design ao domínio desse projeto 

- Bounded Contexts
- Entities, Value Objects, Aggregates
- Domain Events
- Context Map com relações entre contextos

**Entrega** 
	Document LaTeX com Context Map visual + glossário do domínio ubíquo (Ubiquitous Language)