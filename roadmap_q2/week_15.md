# Network Programming em C — HTTP Server do Zero
#s_week 
## Objectivos
- Berkeley sockets API: `socket`, `bind`, `listen`, `accept`, `connect`
- I/O multiplexing: `select`, `poll`, `epoll` — diferenças de performance
- Non-blocking I/O e event loops — como nginx e Node.js funcionam por baixo
- HTTP/1.1: método, headers, body, status codes, keep-alive, chunked encoding
- Protocol design: framing de mensagens binárias
- Serialização: big-endian vs little-endian, length-prefixed vs delimitado

## Recursos

| Tipo  | Recurso                                                     |
| ----- | ----------------------------------------------------------- |
| Livro | _Beej's Guide to Network Programming_ — gratuito em beej.us |
| Docs  | RFC 9110 — HTTP Semantics (o RFC actual do HTTP)            |
| Tool  | Wireshark — análise de pacotes real                         |
| Site  | man7.org — man pages Linux online                           |
| Video | "TCP/IP Explained" — Practical Networking (YouTube)         |

## Projeto
###  HTTP/1.1 Server em C Puro + WebSocket Support

**Tech Stack**
	C11 puro + sockets POSIX

**Overview**
	Um web server completo em C11 puro usando apenas a API de sockets POSIX — sem frameworks, sem bibliotecas de HTTP, sem abstrações. 
	Este é o projecto que prova definitivamente que entendes o que acontece por baixo de qualquer framework web que uses. O servidor precisa de lidar com 10.000+ conexões simultâneas usando `epoll` (o mecanismo que o Linux usa internamente para I/O assíncrono de alta performance), processar todas as 6 methods HTTP mais comuns, servir ficheiros estáticos com MIME type detection, suportar virtual hosts configuráveis via ficheiro de configuração estilo nginx, e implementar todas as features que os clientes HTTP modernos esperam: keep-alive connections, chunked transfer encoding, range requests para streaming de ficheiros grandes.
	O diferencial adicional é o upgrade HTTP → WebSocket (RFC 6455) — o protocolo que os browsers usam para comunicação bidireccional em tempo real.
	O projecto termina com benchmarks rigorosos comparando o teu servidor contra nginx nas mesmas condições de hardware, com análise de Wireshark mostrando os packets HTTP reais.

**Core Features**
- `GET`, `POST`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`
- Static file serving com MIME type detection
- CGI support (executa Python/Bash scripts)
- Virtual hosts configuráveis
- Keep-alive connections (persistent connections)
- Chunked Transfer Encoding
- Range requests (streaming de ficheiros grandes)
- Error pages customizáveis
- Access log em formato CLF (Common Log Format)
- Ficheiro de configuração estilo nginx
- HTTP → WebSocket upgrade (RFC 6455)
- Framing, masking, ping/pong
- Echo server demo em WebSocket

**Requisitos**
- `epoll` para I/O multiplexing (handle 10k+ conexões)
- Thread pool para CGI (não bloqueia o event loop)
- Connection state machine (parsing do HTTP request)
- Memory pool para requests (sem malloc por request)
- Graceful shutdown
- Handle 10k+ concurrent connections
- Benchmark vs nginx (simple cases)
- Memory efficiency

```bash
wrk -t4 -c100 -d30s http://localhost:8080/static/index.html
# Meta: >50% da performance do nginx para ficheiros estáticos no mesmo hardware
```

**Entregáveis** 
- [ ] Servidor compilável com Makefile, zero warnings com `-Wall -Wextra -Werror`
- [ ] Benchmark report vs nginx com análise de onde está a diferença
- [ ] Blog: "Building an HTTP Server from Scratch in C — How nginx Works Under the Hood"
- [ ] Video: arquitectura explicada com Wireshark ao vivo

---

# **_Bônus [07]_**
## Cloud Architecture & Infrastructure as Code

**Objectivo** 
	Compreender como arquitecturas se mapeiam para cloud sem depender de uma cloud específica.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                 |
| ------ | ----------------------------------------------------------------------------------------------------------------------- |
| Livro  | _Cloud Native Patterns_ — Cornelia Davis (caps. 1–6)                                                                    |
| Vídeo  | [AWS Architecture Center — Case Studies (aws.amazon.com/architecture)](https://aws.amazon.com/architecture/) — gratuito |
| Artigo | "The Twelve-Factor App" — Heroku (12factor.net) — **leitura obrigatória**                                               |
| Artigo | "Cloud Design Patterns" — Microsoft Azure Architecture Center (learn.microsoft.com)                                     |
| Canal  | [Fireship — YouTube](https://www.youtube.com/@Fireship) (vídeos de 10min sobre tecnologias cloud)                       |

### PROJECTO: _"Well-Architected Review"_

**Overview** 
	Usando o AWS Well-Architected Framework (ou equivalente Azure/GCP — todos gratuitos), avalia a arquitectura do Projecto 6 contra os 6 pilares:

1. Operational Excellence
2. Security
3. Reliability
4. Performance Efficiency
5. Cost Optimization
6. Sustainability

Identifica gaps e propõe melhorias concretas.

**Entrega:** 
	Documento LaTeX estruturado como relatório de revisão profissional