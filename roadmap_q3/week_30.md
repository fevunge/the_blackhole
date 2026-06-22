# Zig — Systems Programming Moderno
#week 

## Objectivos
- Zig: syntax, comptime, error handling com error unions
- Interoperabilidade com C: importar headers C directamente
- Allocators explícitos: General Purpose, Fixed Buffer, Arena
- Build system: `build.zig` para projectos cross-platform
- Porque Zig: segurança sem GC, alternativa ao C para sistemas

## Recursos

| Tipo    | Recurso                                                          |
| ------- | ---------------------------------------------------------------- |
| Docs    | ziglang.org/documentation — referência oficial                   |
| Guide   | ziglearn.org — tutorial gratuito                                 |
| Prática | Exercism Zig track                                               |
| Video   | "Zig in 100 Seconds" — Fireship; "Why Zig" — Andrew Kelley talks |
| Site    | zig.news — blog da comunidade                                    |

## Projeto
### CLI DevTools Suite em Zig

**Tech Stack:** 
	Zig 0.13+

**Overview**
	Uma suite de 5 ferramentas de linha de comando em Zig — um file finder, um grep, um JSON formatter/validator, um CSV analyser, e um HTTP client simples — com o objectivo explícito de produzir binários mais rápidos ou comparáveis ao equivalente em Rust e Go, mas com binários mais pequenos e zero dependências. Zig tem uma feature única chamada `comptime` que permite gerar código em tempo de compilação baseado nos tipos — vais usar isso para gerar parsers de argumentos e processamento de schemas automaticamente sem macro magic. A cross-compilation é trivial em Zig: um único `zig build` produz binários estáticos para Linux, macOS e Windows sem Docker, sem sysroots, sem configuração. O sistema de allocators explícitos em Zig é obrigatório para cada operação — usas Arena allocator para cada invocação da CLI (cleanup automático quando o processo termina) e Fixed Buffer Allocator para operações com memória limitada conhecida. Os benchmarks comparativos contra `fd`, `ripgrep`, `jq` e `curl` são parte obrigatória do projecto.


**Core features**
- zfind `zfind <pattern>` File finder 
- zgrep `zgrep <pattern>` Grep com suporte a regex básico
- zjson `zjson <file>` JSON formatter + validator
- zcsv `zcsv <file>` CSV analyser: headers, types, stats
- zhttp `zhttp <url>` HTTP client simples (como curl mas mais legível)

**Requisitos**
- Cross-compilation: um `zig build` produz binários para Linux, macOS, Windows
- Binários estáticos (zero dependências externas)
- Memória: Arena allocator para cada invocação (cleanup automático)
- Performance: benchmarks vs `fd`, `ripgrep`, `curl`, `jq`

- **Comptime showcase**

```zig
// Geração de code em compile-time — o que torna Zig especial
fn generateParser(comptime schema: type) ParserFor(schema) {
    // Parsing gerado em compile-time baseado no tipo
}
```

## Entregáveis

- [ ] Suite compilada com GitHub Actions (Linux/macOS/Windows via Zig cross-compilation)
- [ ] Benchmark report: Zig vs Rust vs Go em cada tool
- [ ] Blog: "Zig in 2026 — Is It Ready to Replace C for Systems Programming?"
- [ ] Video: Comptime magic explicado com exemplos
