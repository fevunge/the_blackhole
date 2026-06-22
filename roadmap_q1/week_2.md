# Network Security Fundamentals + API Hardening
#s_week 

## Objectivos
- OWASP Top 10 (2021) em profundidade — ataque e defesa de cada item
- HTTP security headers e o que cada um faz na prática
- Rate limiting: sliding window vs token bucket vs leaky bucket
- Input validation, sanitização e output encoding contextual
- JWT: anatomia, ataques comuns (algorithm confusion, none algorithm), mitigações
- SQL Injection, XSS, CSRF — vector de ataque completo + defesa

## Recursos

| Tipo       | Recurso                                                                                   |
| ---------- | ----------------------------------------------------------------------------------------- |
| Plataforma | PortSwigger Web Security Academy — 100% gratuito, melhor recurso do mundo em web security |
| Livro      | _Web Application Security_ — Andrew Hoffman (O'Reilly)                                    |
| Docs       | OWASP Cheat Sheet Series (cheatsheetseries.owasp.org)                                     |
| Prática    | HackTheBox — free tier (máquinas web)                                                     |
| Video      | LiveOverflow — YouTube (web hacking explicado)                                            |

## Projeto 
### Secure API Framework & Security Middleware Library

**Tech Stack**
	Node.js + Hono + TypeScript + PostgreSQL + Redis + `@simplewebauthn/server`

**Overview**
	Um Framework de API seguro e reutilizável — _o tipo de biblioteca que qualquer empresa séria deveria ter mas raramente constrói porque normalmente junta middlewares de segurança de forma ad-hoc._
	 O teu Framework precisa de ser uma camada de segurança compulsável que qualquer projeto Node.js pode adotar: **middlewares encadeáveis**, **configuração declarativa**, e **zero decisões de segurança deixadas ao desenolvedor** de aplicação.
	 O projecto usa Hono e implementa de raiz rate limiting via Redis com fallback in-memory, **rotação automática de JWT com revogação**, **prevenção de XSS contextual**, **CSRF com double submit cookie**, **suporte completo a Passkeys (WebAuthn)** como alternativa às passwords.

**Core Features**
- Middleware chain de segurança compulsável e declarativa
- Rate limiting: sliding window com Redis, fallback in-memory automático
- JWT com refresh tokens — rotação automática, revogação via Redis
- Input validation automática via Zod schemas declarativos no router
- Parameterized queries obrigatórios via wrapper tipado (impossível fazer SQL injection)
- XSS prevention: sanitização de output contextual (HTML, JS, CSS, URL)
- CSRF tokens: double submit cookie pattern
- Security headers completos (CSP, HSTS, X-Frame-Options, Permissions-Policy)
- Logging de tentativas maliciosas com fingerprinting de attackers
- IP allowlist/blocklist dinâmica com Redis
- 2FA com TOTP (Google Authenticator compatível)
- Passkeys support (WebAuthn) — o padrão que está a substituir passwords
- API key management com escopos, expiração e rotação
- Request signing via HMAC para webhooks
- Audit log imutável com hash chaining

**Testing:**
- Unit tests (segurança de cada middleware isolado)
- Integration tests de fluxos de autenticação
- OWASP ZAP automated scan no CI
- Relatório de penetration test próprio

**Entregáveis**
- [ ] NPM package publicado com documentação completa
- [ ] Security audit report em PDF\
- [ ] Blog: "Building a Production-Grade API Security Layer in 2026"
- [ ] Post LinkedIn sobre OWASP Top 10 com exemplos visuais


---

# **_Bônus [08]_**
## Segurança em Arquitectura (Security by Design)

**Objectivo** 
	Incorporar segurança desde o design, não como afterthought.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------- |
| Livro  | _The Web Application Hacker's Handbook_ — Stuttard & Pinto (caps. 1–5)                                                    |
| Artigo | OWASP Top 10 (owasp.org) — **leitura obrigatória e gratuita**                                                             |
| Artigo | "Threat Modeling" — Microsoft (docs.microsoft.com)                                                                        |
| Vídeo  | ["STRIDE Threat Modeling" — Adam Shostack (YouTube)](https://www.youtube.com/results?search_query=STRIDE+threat+modeling) |
| Site   | [OWASP Architecture Cheat Sheet (cheatsheetseries.owasp.org)](https://cheatsheetseries.owasp.org/)                        |

### PROJECTO 8: _"Threat Model de Sistema Real"_

**Overview** 
	Aplica a metodologia STRIDE ao sistema desse projeto. Produz:
- Data Flow Diagram (DFD) do sistema
- Tabela de ameaças identificadas por categoria STRIDE
- Mitigações propostas para cada ameaça
- Revisão da arquitectura com controlos de segurança

**Entrega** 
	Documento LaTeX de Threat Model + DFD + matriz de risco
