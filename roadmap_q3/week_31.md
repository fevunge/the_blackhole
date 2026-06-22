# Advanced Cybersecurity — Binary Exploitation & Reverse Engineering
#week 

## Objectivos
- Stack-based buffer overflows: smashing the stack, ret2libc
- Return-Oriented Programming (ROP): gadgets, chains
- Format string vulnerabilities: arbitrary read/write
- Reverse engineering: decompilação, analysis de binários
- Mitigações modernas: ASLR, PIE, Stack Canaries, RELRO

## Recursos

| Tipo       | Recurso                                                       |
| ---------- | ------------------------------------------------------------- |
| Plataforma | pwn.college — gratuito, melhor recurso de binary exploitation |
| Livro      | _Hacking: The Art of Exploitation_ — Jon Erickson             |
| Prática    | ROP Emporium — ropemporium.com (gratuito)                     |
| Tools      | GDB + pwndbg, pwntools (Python), Ghidra (gratuito da NSA)     |
| Plataforma | PicoCTF — permanentemente disponível                          |

## Projeto
### Binary Exploitation Challenge Set + Educational Platform

**Tech Stack**
	C (binários vulneráveis) + Python/pwntools (exploits) + Docker (isolamento)

**Overview**
	Um conjunto de 7 challenges de binary exploitation — e a parte que te faz aprender mais do que resolver challenges de outros é ter de criá-los tu mesmo: para construir um bom challenge, tens de entender a vulnerabilidade completamente, implementá-la em C de forma que seja explorável de uma forma específica mas não de outras, e escrever um exploit funcional em Python/pwntools que demonstra a exploração. A progressão vai do stack overflow mais básico (sem mitigações) até chains de ROP para bypass de stack canaries, ASLR e PIE — as mitigações que sistemas modernos têm activadas por default. Para cada challenge: o código C vulnerável comentado pedagogicamente, o exploit Python/pwntools completo, e um write-up detalhado com a análise GDB/pwndbg passo a passo que mostra como identificar a vulnerabilidade, desenvolver a estratégia de exploração, e construir o exploit. A platform Docker isola cada challenge num container separado. Usa Ghidra (gratuito da NSA) para análise de binários e aprende a ler o assembly gerado pelo compilador.

**Core Features**
1. **Stack Smash Básico** — overflow sem mitigações
2. **ret2win** — overflow para chamar função específica
3. **ret2libc** — sem stack executável, usa libc
4. **ROP chain** — encadeia gadgets para system("/bin/sh")
5. **Format String Read** — lê endereços de memória
6. **Format String Write** — escreve em endereços arbitrários
7. **Heap UAF** — use-after-free básico

**Requisitos (Para cada challenge)**
- Código C vulnerável (comentado pedagogicamente)
- Exploit em Python com pwntools
- Write-up detalhado: análise → estratégia → exploit passo a passo
- Versão corrigida com explicação da mitigação
- **Platform Docker:**
	- Cada challenge num container isolado
	- Pode correr localmente ou no servidor

## Entregáveis
- [ ] Challenge set no GitHub (com soluções em branch separada)
- [ ] Write-ups detalhados em Markdown
- [ ] Blog: "Binary Exploitation 101 — From Buffer Overflow to ROP Chain"
- [ ] Video: Live exploitation de 3 challenges com explicação
