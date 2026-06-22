# PROJECTO SHOWCASE #1 — Cloud-Native Platform
#week 

## Self-Hosted Cloud Platform (Mini Fly.io)

**Descrição:** Plataforma de deployment self-hosted — tipo Fly.io ou Render mas construído por ti.

**Tech Stack**
	Go + Rust + Kubernetes + Buildpacks + React

**Overview**
	Vais construir uma plataforma de deployment self-hosted que permite a qualquer developer fazer deploy de aplicações com um único comando — o tipo de produto que o Fly.io, Render e Railway constroem como negócio, mas que tu vais implementar do zero para entender exactamente como funciona. O API Gateway em Go gere autenticação, routing e rate limiting para todos os serviços da plataforma. O Build Service usa Cloud Native Buildpacks para detectar automaticamente a linguagem do projecto, instalar dependências e produzir uma imagem Docker sem que o developer escreva um Dockerfile. O Deploy Service usa o Kubernetes API para criar Deployments, Services e Ingresses automaticamente com naming conventions consistentes. O Storage Service em Rust implementa uma API S3-compatible (subset do S3) sobre o filesystem local com SHA-256 integrity checking. O Database Service provisiona instâncias PostgreSQL e Redis isoladas por utilizador com credentials geradas automaticamente. O Billing Service calcula uso por CPU-second e GB-month mesmo que não cobres (é a estrutura que precisas de ter). A CLI experience é o que um developer vê: `platform deploy` detecta a linguagem, builda, deploya, e devolve a URL em 60 segundos.

**Core Features**

1. **API Gateway** (Go + Hono): routing, auth, rate limiting
2. **Build Service** (Go): recebe código, usa Buildpacks para criar imagens
3. **Deploy Service** (Go + K8s API): deploy de imagens para o cluster
4. **Storage Service** (Rust): object storage compatível com S3 API (MinIO wrapper)
5. **Database Service** (Go): provisiona PostgreSQL e Redis isolados por utilizador
6. **Monitoring Service** (Go): expõe métricas OTel dos deployments
7. **Billing Service** (Go): tracking de uso e cálculo de custo

**Developer Experience:**

```bash
platform login
platform deploy --app myapp --region us-east   # detecta linguagem, builda, deploya
platform logs myapp
platform scale myapp --instances 3
platform db create myapp --type postgres
platform domain add myapp api.example.com
```

**Security:**
- mTLS entre todos os serviços (cert-manager)
- Secrets encriptados em Vault
- Tenant isolation: namespace K8s por utilizador
- Network policies para zero trust

## Entregáveis

- [ ] Platform funcional (self-hosted num cluster local)
- [ ] Whitepaper técnico: arquitectura e decisões (20+ páginas)
- [ ] Video demo: deploy de uma app real em 60 segundos
- [ ] Blog series (5 posts)
- [ ] Open-source release com documentação

