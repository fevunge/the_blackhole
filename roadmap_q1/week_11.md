# Linux Systems & Bash Scripting
#week 

## Objectivos
- Linux internals: processos, threads, signals, file descriptors
- Filesystem hierarchy standard (FHS) e o que está em cada directório
- Bash scripting avançado: arrays, functions, trap, getopts, heredocs
- Process management: `systemd` units, targets, journald
- System calls fundamentais: `fork`, `exec`, `wait`, `pipe` — o que cada uma faz
- Log management: `journald`, `logrotate`
- Cron e `systemd` timers — quando usar cada um

## Recursos

| Tipo    | Recurso                                                                  |
| ------- | ------------------------------------------------------------------------ |
| Livro   | _The Linux Command Line_ — William Shotts (gratuito em linuxcommand.org) |
| Course  | Linux Journey — linuxjourney.com                                         |
| Prática | OverTheWire: Bandit (wargame gratuito, 34 levels)                        |
| Ref     | man pages — `man 2 fork`, `man 7 signal`, etc.                           |
| Video   | "Linux Crash Course" — Learn Linux TV (YouTube)                          |

## Projeto
### System Observability Agent + Dashboard em Tempo Real

**Tech Stack** 
	Python (agente) + Bash (scripts) + Flask (API/SSE) + React (dashboard) + SQLite

**Overview**
	Um agente de monitorização de sistema leve que corre como serviço `systemd` e expõe as métricas do servidor através de um dashboard web com actualização em tempo real — como um Prometheus node_exporter mais simples, mas construído por ti, o que te permite entender exactamente o que está a ser medido e porquê.
	O agente Python recolhe métricas a cada 5 segundos: CPU por core e load average, memória RSS/VSZ/swap, disk I/O e espaço em todos os pontos de montagem, rede por interface, top-N processos por CPU e por memória, e health checks dos serviços `systemd` configurados.
	As métricas são persistidas em SQLite para histórico de 30 dias e enviadas via SSE (Server-Sent Events) para o dashboard React com gráficos em tempo real via Chart.js.
	O sistema de alertas configura thresholds por métrica e envia notificações via SMTP local. Para além do agente, produces quatro scripts Bash que mostras a qualidade do trabalho: 
	**instalação automatizada**, **backup incremental com rsync**, **auditoria de segurança básica**, e **rotação de logs**.
	
**Core Features**
- CPU per-core + load average
- Memory: RSS, VSZ, swap usage
- Disk: I/O, espaço, inodes
- Network: bytes in/out, conexões activas
- Top-N processos por CPU e memória
- Service health checks via `systemd` API
- Log pattern detection (regex configurável)
- Gráficos em tempo real (Chart.js via SSE)
- Histórico de 30 dias em SQLite
- Alertas configuráveis (email via SMTP local)
- Exportação de relatório em PDF

**Requisitos Técnicos**
- `install.sh` — instalação com `systemd` service, verifica dependências
- `backup.sh` — backup incremental com rsync + verificação de checksum
- `security-audit.sh` — permissões suspeitas, portas abertas, utilizadores sem password
- `log-rotate-custom.sh` — rotação com compressão e retenção configurável

**Entregáveis**
- [ ] Agente + dashboard no GitHub com scripts de instalação
- [ ] Blog: "Building a System Monitoring Agent from Scratch in Python"
- [ ] Video: dashboard em tempo real com alertas a funcionar
- [ ] Cheat sheet: "50 Linux Commands Every Developer Must Know" (PDF)
