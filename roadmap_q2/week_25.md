# WebAssembly — Rust para Browser + SIMD
#week

## Objectivos
- WebAssembly: formato binário, text format (WAT), módulos
- `wasm-bindgen`: Rust → JavaScript interop
- `web-sys` e `js-sys`: acesso às Web APIs a partir de Rust
- WASI: WebAssembly fora do browser
- Performance: onde Wasm brilha e onde não

## Recursos

| Tipo      | Recurso                                                |
| --------- | ------------------------------------------------------ |
| Docs      | rustwasm.github.io/book — Rust and WebAssembly oficial |
| Tool      | wasm-pack — build tool standard                        |
| Docs      | webassembly.org — spec e overview                      |
| Exercício | "Game of Life in Rust+Wasm" — tutorial oficial         |
| Video     | "WebAssembly from Ground Up" — Lin Clark (YouTube)     |

## Projeto
### Image Processing Studio — Rust + Wasm + React

**Tech Stack** 
	Rust + wasm-bindgen + SIMD + React + TypeScript + Web Workers

**Overview** 
	Um editor de imagem completo que corre inteiramente no browser sem servidor, com o processamento de imagem implementado em Rust compilado para WebAssembly com instruções SIMD — o que produz performance comparável a software nativo para operações intensivas em pixeis. O editor suporta upload de JPEG, PNG, WebP e AVIF, e expõe todos os filtros e ajustes processados em Rust via Wasm: Gaussian blur com kernel configurável, Sharpen, Edge detection com Sobel e Laplacian, Color grading (brightness, contrast, saturation, hue, curves), Sepia, Grayscale, Invert, Vignette, e Chromatic aberration. O histograma é também calculado em Rust e actualizado em tempo real enquanto ajustas parâmetros. Todo o processamento corre num Web Worker para não bloquear a thread UI — o utilizador consegue usar a interface enquanto um blur de 20px é aplicado a uma imagem 4K. O Before/After slider mostra o resultado vs original. O batch processing processa múltiplos ficheiros com as mesmas configurações. O benchmark obrigatório compara Rust+Wasm vs JavaScript puro para blur gaussiano em imagens de diferentes tamanhos, e mostra o speedup das instruções SIMD vs Wasm sem SIMD.


**Core Features**
- Upload e preview de imagens (JPEG, PNG, WebP, AVIF)
- Filtros implementados em Rust (compilados para Wasm):
    - Blur gaussiano (kernel configurável)
    - Sharpen, Edge detection (Sobel, Laplacian)
    - Color grading: brightness, contrast, saturation, hue
    - Sepia, grayscale, invert
    - Vignette, chromatic aberration
- Histogram em tempo real (implementado em Rust)
- Before/after slider
- Batch processing de múltiplos ficheiros
- Export: PNG, JPEG (qualidade configurável), WebP

**Requisitos**
- Rust core via Wasm: processamento no Web Worker (não bloqueia UI)
- SIMD instructions onde disponível (`packed_simd` crate)
- Benchmark: Rust+Wasm vs JavaScript puro para blur em imagem 4K

## Entregáveis

- [ ] Web app publicada (GitHub Pages ou Cloudflare Pages — gratuito)
- [ ] Blog: "Why Rust + WebAssembly is the Future of Performance-Critical Web Apps"
- [ ] Benchmark detalhado: Wasm vs JS em diferentes operações e tamanhos
- [ ] Video: "Building a Fast Image Editor with Rust and WebAssembly"
