# Rust Fundamentals + Memory Safety
#week 

## Objectivos

- Ownership, borrowing, lifetimes — os três pilares; entender o porquê de cada regra
- Error handling idiomático: `Result<T, E>`, `?` operator, `thiserror`, `anyhow`
- Pattern matching exaustivo — mais poderoso que switch em qualquer outra linguagem
- Traits e generics com bounds — como Rust faz polimorfismo sem vtables obrigatórias
- Cargo, crates.io, workspaces — o ecossistema de packages

##  Recursos

| Tipo       | Recurso                                                              |
| ---------- | -------------------------------------------------------------------- |
| Livro      | _The Rust Programming Language_ — gratuito em doc.rust-lang.org/book |
| Exercícios | Rustlings — github.com/rust-lang/rustlings                           |
| Video      | Jon Gjengset — "Rust for Rustaceans" talks no YouTube                |
| Tool       | rust-analyzer + Clippy com linting agressivo                         |
| Blog       | This Week in Rust — this-week-in-rust.org                            |

## Projeto

### Memory-Safe Terminal Text Editor (Vim-like core)

**Tech Stack:** 
	Rust + `crossterm` + `tree-sitter` + `tokio`
	
**Overview**
	Um editor de texto para terminal em Rust que usa um **Gap Buffer** como estrutura de dados central.
	O Gap Buffer é o projecto perfeito para aprender Rust a sério porque força-te a lidar com **lifetimes não triviais**, **ownership de blocos de memória mutável**, e a correcta separação entre **lógica de edição** e **I/O**.
	O editor precisa de suportar **modos Normal/Insert/Visual** ao estilo Vi, undo/redo ilimitado via Command Pattern (cada operação é um comando reversível), search e replace com regex, e syntax highlighting para as 5 linguagens mais comuns via integração com `tree-sitter`.
	O I/O com o terminal usa `crossterm` para cross-platform compatibility. A parte mais desafiante é integrar o event loop do `crossterm` com o runtime assíncrono do `tokio` para file I/O — tens de resolver este problema sem referencias circulares ou deadlocks.
	O projecto é publicado no crates.io com documentação completa e benchmarks de operações de edição.
	
**Core Features**
- Gap buffer para edição eficiente de texto de qualquer tamanho
- Undo/Redo com Command Pattern e histórico ilimitado
- Search & replace com regex (`regex` crate)
- Syntax highlighting via `tree-sitter` para Rust, Python, JS, Go, C
- File I/O assíncrono com `tokio::fs`
- Unicode completo: grapheme clusters correctos
- Modo Normal/Insert/Visual (estilo Vi)
- Status bar com nome do ficheiro, linha/coluna, modo actual

**Requisitos Técnicos**
- Gap buffer requer lifetimes não triviais
- Tree-sitter bindings via `unsafe` controlado
- `crossterm` event loop com `tokio` — integração de runtimes
- Zero cópias desnecessárias nos hot paths

**Entregáveis**
- [ ] Crate publicado no crates.io
- [ ] Benchmark: operações de edição vs nano (usando criterion)
- [ ] Blog: "Implementing a Gap Buffer in Rust — Fighting the Borrow Checker"
- [ ] Diagrama de ownership e lifetimes das structs principais
