# PROJECTO SHOWCASE #3 — Security Operations Platform
#week 

## SecOps Platform — Scanner + WAF + SIEM

**Descrição:** Suite de ferramentas de segurança integradas — o tipo de coisa que as empresas pagam centenas de milhares de dólares por ano mas que tu podes construir.

**Tech Stack**
	Go + Python + Rust + PostgreSQL + ClickHouse + Nginx

**Overview**
	Vais construir uma suite de quatro ferramentas de segurança integradas — o tipo de produtos que empresas vendem separadamente por centenas de milhares por ano. O Vulnerability Scanner em Go faz port scanning via nmap API, service fingerprinting, CVE lookup na NVD API gratuita, e análise da configuração de segurança HTTP (headers, TLS config, CORS policy), produzindo relatórios em Markdown e PDF com findings ordenados por CVSS score. O Web Application Firewall em Go com Nginx aplica um rules engine baseado no OWASP Core Rule Set com anomaly scoring configurável, bot detection por padrões de behaviour, e um dashboard de ataques bloqueados em tempo real. O SIEM Light em Python com ClickHouse colecciona logs de múltiplas fontes em formatos diferentes (JSON, syslog, CEF), aplica regras de correlação configuráveis ("X eventos de tipo Y em Z segundos = alerta"), usa Isolation Forest para anomaly detection, e roteia alertas para email, webhook ou Slack. O Secrets Vault em Rust com AES-256-GCM guarda secrets encriptados com RBAC por namespace, audit log com hash chaining, rotação automática de secrets, e uma CLI + API. A integração entre os quatro: o SIEM detecta um ataque e instrui o WAF a bloquear automaticamente o IP atacante.

**Tools:**

**1. Vulnerability Scanner (Go):**
- Port scanning via `nmap` API
- Service fingerprinting
- CVE lookup via NVD API (gratuita)
- Web app scanning: headers, SSL/TLS config, CORS
- Relatório em Markdown e PDF

**2. Web Application Firewall — WAF (Go + Nginx):**
- Rules engine baseado em OWASP Core Rule Set
- Rate limiting por IP, user, endpoint
- Anomaly scoring (bloqueia se score > threshold)
- Bot detection (user-agent, behaviour patterns)
- Dashboard de ataques bloqueados

**3. SIEM Light (Python + ClickHouse):**
- Log collection de múltiplas fontes (JSON, syslog, CEF)
- Correlation rules: "se X eventos em Y segundos → alerta"
- Anomaly detection com ML simples (isolation forest)
- Dashboard de incidents (Grafana)
- Alert routing: email, webhook, Slack

**4. Secrets Vault (Rust + AES-256-GCM):**
- Storage encriptado de secrets
- Access control por RBAC
- Audit log imutável
- CLI + API
- Rotação automática de secrets (configurable)

**Integration:**

- API unificada para todas as tools
- Central dashboard com risk score global
- Automated response: block IP no WAF quando SIEM detecta ataque

## Entregáveis

- [ ] Security suite completa e open-source
- [ ] Blog series: uma post por tool
- [ ] Video demos individuais
- [ ] Security best practices guide (baseada nas lições de construir as tools)
- [ ] CTF environment usando as ferramentas para testar
