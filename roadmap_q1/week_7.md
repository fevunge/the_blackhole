# Authentication & Authorization Deep Dive
#s_week 

## Objectivos
- OAuth 2.0: todos os flows com Authorization Code + PKCE, Client Credentials, Device Authorization
- OpenID Connect: ID tokens, UserInfo endpoint, discovery document
- JWT: estrutura, algoritmos (HS256 vs RS256 vs ES256), vulnerabilidades conhecidas
- RBAC vs ABAC — modelação e implementação em bases de dados relacionais
- Session management seguro em sistemas distribuídos
- Passkeys / WebAuthn — arquitectura e implementação completa
- Passwordless authentication

## Recursos

| Tipo  | Recurso                                                             |
| ----- | ------------------------------------------------------------------- |
| Spec  | OAuth 2.0 RFC 6749 + RFC 7636 (PKCE)                                |
| Site  | oauth.net — guias práticos do Aaron Parecki                         |
| Site  | webauthn.guide — introdução a Passkeys                              |
| Docs  | OWASP Authentication Cheat Sheet                                    |
| Video | "OAuth 2.0 and OpenID Connect in Plain English" — OktaDev (YouTube) |

## Projeto
### Auth Platform Production-Ready com Passkeys

**Tech Stack** 
	Node.js + TypeScript + Hono + PostgreSQL + Redis + `@simplewebauthn/server`

**Overview**
	Um serviço de autenticação completo e independente — o tipo de solução que a maioria das empresas compra ao Auth0 ou Clerk por centenas de dólares por mês, mas que tu vais construir do zero e entender completamente.
	O serviço actua como um **OAuth 2.0 Authorization Server** próprio, capaz de emitir tokens para as tuas aplicações, com **OpenID Connect** completo e **discovery document** no endpoint padrão `.well-known/openid-configuration`.
	Implementas todos os flows de autenticação relevantes: **email/password** com Argon2id, OAuth social via Google e GitHub, magic links **passwordless**, **2FA com TOTP**, e o diferencial crítico de 2026 — Passkeys (WebAuthn) completo com registo de authenticators, verificação de assinatura de desafio, e suporte a multiple authenticators por utilizador.
	O sistema de sessões usa Redis para distribuição, tokens têm curta duração (15min access, 7 dias refresh com rotação automática), e o audit log usa hash chaining para garantir imutabilidade.
	O projecto termina dockerizado e funcional, com OpenAPI spec completa e testes de todos os fluxos críticos.

**Core Features**
- OAuth 2.0 Authorization Server próprio (emite tokens para as tuas apps)
- OpenID Connect completo com discovery document
- Passkeys (WebAuthn): registo e autenticação sem password
- Strategies: local (email+password), Google, GitHub OAuth
- 2FA com TOTP + magic links passwordless
- Refresh token rotation automática com revogação por Redis
- Session management distribuído via Redis
- RBAC com permissions granulares por recurso e organização
- Brute force protection com lockout progressivo
- Audit log imutável com hash chaining
- Rate limiting por utilizador, por IP e por endpoint
- Email verification + password reset flow com tokens de uso único
- Magic links (passwordless via email)

**Requisitos Técnicos**
- Argon2id para hashing de passwords
- PKCE obrigatório para todos os Authorization Code flows
- Tokens de curta duração (15min access, 7d refresh)
- Secure cookies: `HttpOnly`, `Secure`, `SameSite=Strict`

**Entregáveis**
- [ ] Microservice dockerizado com `docker-compose` funcional
- [ ] OpenAPI 3.1 spec completa com Swagger UI
- [ ] Blog: "Building a Production Auth System with Passkeys in 2026"
- [ ] Video: Demo de registo e login via Passkey (do zero)
---
# _**Bônus [03.2]**_

## Modelo C4 & Comunicação Visual de Arquitectura

**Objectivo** 
	Dominar a linguagem visual de arquitectura. Um arquitecto que não consegue comunicar graficamente a sua solução é ineficaz.

### Recursos

| Tipo   | Recurso                                                                                                                      |
| ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Site   | [C4 Model — Simon Brown (c4model.com)](https://c4model.com/) — lê TUDO                                                       |
| Livro  | _Software Architecture for Developers_ — Simon Brown (disponível parcialmente grátis no Leanpub)                             |
| Vídeo  | ["Visualising software architecture with the C4 model" — Simon Brown (YouTube)](https://www.youtube.com/watch?v=x2-rSnhpw0g) |
| Artigo | UML Distilled — Martin Fowler (capítulos sobre diagramas de sequência e componentes)                                         |
| Tool   | [Structurizr Lite](https://structurizr.com/help/lite) — C4 como código, **gratuito**                                         |

### Prática

- Cria os diagramas deste projecto em C4
- Recria os diagramas do projecto anterior em C4 (Context → Container → Component)
- Pratica diagramas de sequência UML para fluxos comuns (login, pagamento, upload)
- Aprende a usar Structurizr DSL para diagramas-como-código

### PROJECTO: _"Sistema de Reservas — C4 Completo"_

**Overview** 
	Desenha a arquitectura de um sistema de reservas de hotel (sem implementar código). Entrega os 4 níveis C4:

- Level 1: Context Diagram
- Level 2: Container Diagram
- Level 3: Component Diagram (para o container principal)
- Level 4: Code Diagram (opcional — apenas classes principais)

**Entrega** 
	Diagramas exportados + documento LaTeX explicando cada decisão em cada nível

# [Parte 2/2]