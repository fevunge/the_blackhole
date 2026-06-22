# Cybersecurity — Penetration Testing Fundamentals
#week 
## Objectivos
- Reconnaissance: passive (OSINT tools) e active (port scanning com nmap)
- Metodologia de penetration testing: fases, scope, regras de engagement
- Web app pentesting: SQL injection, XSS, IDOR, SSRF, business logic flaws
- Report writing profissional: findings, risk rating CVSS, passos de reprodução, remediação
- Ferramentas: Burp Suite Community, nmap, gobuster, sqlmap
##  Recursos

| Tipo       | Recurso                                                      |
| ---------- | ------------------------------------------------------------ |
| Plataforma | TryHackMe — free paths (OWASP Top 10, Jr Penetration Tester) |
| Plataforma | HackTheBox — free tier (Starting Point machines)             |
| Livro      | _The Web Application Hacker's Handbook_ — Stuttard & Pinto   |
| Tools      | Kali Linux (VM), Burp Suite Community, nmap, gobuster        |
| Plataforma | PortSwigger Academy — todos os labs de SQL injection e XSS   |

## Projeto
### Vulnerable Lab App + Pentest Report Profissional

**Overview**
	Dois sistemas: 
	- primeiro, uma aplicação web intencionalmente vulnerável que implementa exactamente as vulnerabilidades do OWASP Top 10 de forma controlada e pedagógica;
	- segundo, a versão corrigida dessa mesma aplicação com todas as vulnerabilidades mitigadas. 
	Entre os dois sistemas, produzes um relatório de penetration testing completo no formato que uma empresa de segurança real usaria com um cliente.
	A aplicação vulnerável é uma plataforma de blog simples onde cada feature esconde uma vulnerabilidade: *o sistema de login tem SQL injection no campo de utilizador*, *os comentários têm XSS stored*, o sistema de upload de avatares aceita ficheiros PHP, os endpoints da API têm IDOR (qualquer utilizador consegue ler os dados de qualquer outro), e o painel admin está acessível sem autenticação se souberes o path. Para cada vulnerabilidade: documenta o vector de ataque com request/response reais capturados no Burp Suite, o código vulnerável, o CVSS score calculado, e o código corrigido com explicação da mitigação. O relatório final tem de ser profissional o suficiente para incluir no portfolio como demonstração de security mindset.

**Tech Stack:** Node.js + React (app vulnerável) + Kali Linux (pentesting)

**Core Features**
- Vulnerable app (modo lab)
- Pentest report completo (formato OWASP)
- Fixes implementation
- Before/after comparison
- A01 - Broken Access Control: IDOR em `/api/users/:id`, admin path disclosure
- A02 - Cryptographic Failures: passwords em MD5, dados sensíveis sem encryption
- A03 - SQL Injection: query string concatenation directa no login
- A07 - XSS: Stored em comentários, Reflected em search, DOM-based em hash
- A08 - CSRF: formulários sem token
- A09 - Security Misconfiguration: stack traces em produção, debug mode activo
- Broken Authentication: sem brute force protection, JWT `alg: none`

**Entregáveis**
- [ ] App vulnerável + versão corrigida no GitHub (branches separadas)
- [ ] Pentest report profissional em PDF
- [ ] Blog: "OWASP Top 10 Explained With Real Code — Attack and Fix"
- [ ] Video: Demo ao vivo de SQL injection + fix + antes/depois
