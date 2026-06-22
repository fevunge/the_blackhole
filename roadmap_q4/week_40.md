# System Design — URL Shortener Production-Grade
#s_week 
## URL Shortener com Analytics em Tempo Real

**Tech Stack**
	Go + PostgreSQL + Redis + ClickHouse + Kafka + CDN

**Overview**
	Vais construir um URL shortener com analytics completo desenhado para escalar a 10 bilhões de clicks por mês — e o que torna este projecto interessante não é a feature de shortening em si (trivial) mas o capacity planning rigoroso e as decisões de arquitectura que tens de justificar.
	O sistema usa Base62 com Bloom Filter para collision detection durante geração de IDs, CDN com cache de 24h para redirects de links populares (eliminando 99%+ dos hits ao servidor), e Kafka como buffer entre os click events e o ClickHouse (base de dados colunar) onde os analytics ficam disponíveis em menos de 30 segundos.
	O sistema suporta custom slugs com reserva de namespace, QR codes gerados server-side com `go-qrcode`, link expiration, password protection, e edição de links existentes.
	O capacity planning documentado responde: 
	**quantos servidores para 10k writes/segundo?**
	**Quanto storage para 100M URLs?**
	**Qual cache hit rate necessária para o p99 < 5ms nos redirects?**
	O load test com k6 valida as estimativas contra a realidade.

**Core Features**
- Shortening com Base62 + collision detection via Bloom filter
- Analytics em tempo real: clicks, geo, devices, referrers
- Custom slugs com reserva de namespace
- QR codes gerados server-side
- Link expiration, password protection, editing
- Bulk import/export via CSV
- API + Dashboard

**Arquitectura para escala:**

```
Client → CDN (cache de redirects quentes)
           ↓ (cache miss)
        Load Balancer
           ↓
        API Servers (Go, stateless)
           ↓           ↓
        Redis       PostgreSQL
        (cache)     (source of truth)
           ↓
        Kafka → ClickHouse (analytics)
```

**Requisitos de performance:**

- Redirects: <5ms p99 (com cache CDN)
- Writes: 10k+/segundo
- Analytics: dados disponíveis em <30s após click

**Capacity Planning obrigatório:**

- 100M URLs: quanto storage?
- 10B clicks/mês: quanto throughput no Kafka?
- Cache hit rate target: >99%

## Entregáveis

- [ ] Sistema em produção com URL pública
- [ ] Design doc completo (ADRs, capacity planning, trade-offs)
- [ ] Load test results (k6 — 10k requests/segundo)
- [ ] Blog: "Scaling a URL Shortener to 10B Clicks"

---
# **_Bônus [10]_**

API Design & Integration Patterns

**Objectivo** 
	Dominar o design de APIs e padrões de integração entre sistemas.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                             |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| Livro  | _Enterprise Integration Patterns_ — Hohpe & Woolf (caps. seleccionados: Messaging, Routing, Transformation) — **clássico absoluto** |
| Artigo | "REST API Design Best Practices" — Microsoft API Guidelines (GitHub, gratuito)                                                      |
| Artigo | "Understanding gRPC" — grpc.io (documentação oficial)                                                                               |
| Artigo | "GraphQL vs REST vs gRPC" — comparações em posts de engenharia                                                                      |
| Site   | [Postman Learning Center](https://learning.postman.com/) — gratuito                                                                 |

### PROJECTO : _"API Gateway & Integration Design"_

**Overview** 
	Desenha a estratégia de API para uma empresa com 5 sistemas legados que precisam de ser integrados com uma nova aplicação mobile. Inclui:

- Escolha de padrão de integração (REST, GraphQL, gRPC, eventos)
- Design do API Gateway
- Padrões: Circuit Breaker, Retry, Rate Limiting
- Versionamento de APIs
- Documentação OpenAPI (Swagger) — pelo menos 1 endpoint documentado

**Entrega:** 
	Documento LaTeX + especificação OpenAPI em YAML + diagramas de integração