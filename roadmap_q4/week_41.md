# High-Performance Web Server (C++)
#week 

### HTTP/2 Server em C++20

**Tech Stack:** C++20 + OpenSSL + nghttp2 + epoll

**Overview**
	Vais evoluir o servidor HTTP da [[week_15]] para suportar HTTP/2 com TLS 1.3 e funcionalidade de reverse proxy — tornando-o um servidor que podes usar em produção real para servir as tuas aplicações. HTTP/2 muda fundamentalmente o modelo de comunicação: um único connection TCP multiplexes múltiplos streams em paralelo, server push envia recursos antes de serem pedidos, e HPACK comprime headers de forma que requests repetidos ficam tiny. A implementação usa a biblioteca `nghttp2` para o framing HTTP/2 (o protocolo de framing é complexo demais para implementar do zero num prazo razoável) e OpenSSL para TLS 1.3. O reverse proxy load balancing usa round-robin com health checks activos, e o response caching respeita os headers Cache-Control e ETag para cache validation. Brotli compression reduz o tamanho dos responses em 20-30% vs gzip. O endpoint `/metrics` expõe métricas Prometheus para integrar com o stack de observabilidade da [[week_28]]. O benchmark final compara com nginx nas mesmas condições para requests de ficheiros estáticos e para proxying para um backend Go.

**Core Features**

- Todas features da [[week_15]]
- HTTP/2: multiplexing, server push, header compression (HPACK)
- TLS 1.3 via OpenSSL (self-signed para dev, Let's Encrypt para prod)
- WebSocket upgrade (RFC 6455)
- Reverse proxy: balanceamento de carga entre backends
- Response caching: in-memory + disk (Cache-Control respeitado)
- Compression: gzip + brotli
- Metrics endpoint `/metrics` compatível com Prometheus

**Performance target:**

```bash
# Meta: >80% da performance do nginx para static files
wrk -t4 -c400 -d30s https://localhost:443/index.html

# nginx: ~150k req/s
# Teu server: >120k req/s
```

## Entregáveis

- [ ] Servidor production-ready com TLS funcional
- [ ] Benchmark report vs nginx (mesmas condições)
- [ ] Blog: "Building an HTTP/2 Server in C++20 — How nginx Actually Works"
- [ ] Video: arquitectura explicada com Wireshark mostrando frames HTTP/2
