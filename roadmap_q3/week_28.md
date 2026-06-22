# Observability — OpenTelemetry & Grafana Stack
#s_week 

## Objectivos

- OpenTelemetry: o standard unificado para telemetria (substitui instrumentação custom)
- Metrics (Prometheus), Logs (Loki), Traces (Tempo) — Grafana Stack
- SLO/SLI/SLA: como definir e medir
- Golden Signals: latency, traffic, errors, saturation
- Alerting baseado em SLO (não apenas thresholds estáticos)

## Recursos

| Tipo   | Recurso                                                   |
| ------ | --------------------------------------------------------- |
| Docs   | opentelemetry.io — spec e SDKs                            |
| Livro  | _Observability Engineering_ — Majors, Fong-Jones, Miranda |
| Course | Grafana fundamentals — grafana.com/tutorials              |
| Blog   | "SLO Fundamentals" — Google SRE resources                 |
| Tool   | Grafana Cloud free tier — 3 users grátis, suficiente      |

## Projeto
### OpenTelemetry Observability Stack

**Tech Stack:** 
	OpenTelemetry Collector + Prometheus + Loki + Tempo + Grafana

**Overview**
	Construir e instrumentar uma stack de observabilidade completa usando OpenTelemetry como camada de abstracção unificada — o standard que ganhou em 2026 e que evita vendor lock-in. O OpenTelemetry Collector recebe métricas, logs e traces de todos os serviços via protocolo OTLP e encaminha para os backends específicos: Prometheus para armazenamento de métricas (com PromQL para queries), Loki para logs com structured logging e LogQL para queries complexas, e Tempo para distributed traces sem limite de storage baseado em objectos. O Grafana unifica os três pilares num único dashboard e permite correlação — de uma trace clicas e vês os logs do mesmo request, e depois vês as métricas do serviço naquele intervalo de tempo. A instrumentação é automática para Node.js, Go e Python sem alterar o código da aplicação. Os dashboards SLO mostram burn rate e error budget remaining em vez de thresholds estáticos que criam alert fatigue. Produz um `docker-compose up` que levanta toda a stack numa linha.

**Requisitos**

- **OTel Collector**: recebe métricas/logs/traces de todos os serviços e encaminha
- **Prometheus**: armazenamento de métricas com PromQL
- **Loki**: logs aggregation com LogQL
- **Tempo**: distributed traces sem limits de storage
- **Grafana**: dashboards, alertas, correlação entre os três pilares
- **Instrumentação (automática com OTel):**
	- Node.js: `@opentelemetry/auto-instrumentations-node`
	- Go: `go.opentelemetry.io/contrib/instrumentation`
	- Python: `opentelemetry-distro`
- **Dashboards**
	- RED metrics por serviço (Rate, Errors, Duration)
	- Infrastructure: CPU, memory, disk, network
	- Business metrics: orders/min, revenue/hour, DAU
	- SLO dashboard: burn rate, error budget remaining
- **Alertas SLO-based:**

```yaml
# Alerta se consumir >5% do error budget em 1 hora
alert: ErrorBudgetBurnRateTooHigh
expr: error_budget_burn_rate > 14.4  # 5% em 1h = 14.4x burn rate
```

## Entregáveis

- [ ] Stack completa em `docker-compose` — um `docker-compose up` e funciona tudo
- [ ] Dashboards exportados como JSON (importáveis)
- [ ] Blog: "OpenTelemetry in 2026 — The Standard That Finally Won"
- [ ] Playbooks de alertas (runbooks para cada alerta configurado)
---
# **_Bônus [12]_**

## DevOps, CI/CD & Observabilidade para Arquitectos

**Objectivo** 
	Compreender como arquitetura impacta (e é impactada por) DevOps e observabilidade.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                      |
| ------ | -------------------------------------------------------------------------------------------- |
| Livro  | _The Phoenix Project_ — Gene Kim (ficção técnica — lê completo, é rápido)                    |
| Livro  | _Accelerate_ — Nicole Forsgren, Jez Humble & Gene Kim (caps. 1–5)                            |
| Artigo | "Observability vs Monitoring" — Charity Majors (honeycomb.io blog)                           |
| Vídeo  | [DevOps Roadmap — TechWorld with Nana (YouTube)](https://www.youtube.com/@TechWorldwithNana) |
| Artigo | DORA Metrics — Google (cloud.google.com/devops)                                              |

### PROJECTO: _"DevOps Architecture Blueprint"_

**Overview** 
	Desenha o pipeline completo de DevOps para o sistema e-commerce dos blocos anteriores:

- Pipeline CI/CD (build, test, deploy)
- Estratégia de ambientes (dev, staging, prod)
- Observability stack: logs, métricas, traces (escolha gratuita: Grafana + Prometheus + Jaeger)
- Alerting e SLO/SLA definitions
- Runbook de incidente

**Entrega** 
	Documento LaTeX + diagrama do pipeline + diagrama da observability stack

