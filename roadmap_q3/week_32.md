# Compiler Design — Interpreter + Language Server Protocol
#week 

## Objectivos
- Lexical analysis: tokenização, DFAs
- Parsing: recursive descent, Pratt parsing para expressões
- AST: design, visitor pattern
- Type checking: type inference básica
- Code generation: bytecode ou LLVM IR
- Language Server Protocol (LSP): como funciona o autocomplete do VS Code

## Recursos

| Tipo    | Recurso                                                                      |
| ------- | ---------------------------------------------------------------------------- |
| Livro   | _Crafting Interpreters_ — Bob Nystrom (gratuito em craftinginterpreters.com) |
| Docs    | LLVM Tutorial — llvm.org/docs/tutorial                                       |
| Spec    | Language Server Protocol — microsoft.github.io/language-server-protocol      |
| Video   | "Writing an Interpreter in Go" — Thorsten Ball book walkthrough              |
| Prática | Implement cada capítulo de Crafting Interpreters                             |

## Projeto
### Linguagem de Programação + LSP Server

**Tech Stack** 
	Rust ou C++ (interpretador) + TypeScript (LSP extension VS Code)

**Overview**
	uma linguagem de programação completa com interpretador e um language server que se integra com o VS Code — o projecto que te faz perceber como o teu editor funciona por dentro quando sublinha erros em tempo real, oferece autocomplete, e navega para definições. A linguagem tem tipagem estática com inferência (não precisas de declarar o tipo de tudo), funções de primeira classe, pattern matching, e um sistema de módulos simples. O pipeline de compilação segue as fases canónicas: Lexer transforma o source em tokens com error recovery (não para no primeiro erro), Parser usa Pratt parsing para lidar com precedência de operadores de forma elegante, o Type Checker faz inferência de tipos e produz erros detalhados com sugestões, e a Bytecode VM executa o código compilado numa stack-based virtual machine. O LSP server implementa os endpoints mais importantes: textDocument/hover (mostra o tipo de uma expressão), textDocument/diagnostic (erros em tempo real enquanto escreves), textDocument/completion (autocomplete de variáveis e funções no scope), e textDocument/definition (go-to-definition). A VS Code extension empacota o LSP server e activa-o para ficheiros `.tualnguagem`. O REPL permite experimentar interactivamente.

**Core Feature**
- Variables e tipos (int, float, string, bool)
- Control flow (if, while)
- Functions
- Arrays/Lists
- Hash maps
- Standard library

**Requisitos**
- Lexer: tokenização com error recovery
- Parser: recursive descent com Pratt parsing para precedência de operadores
- AST: nodes tipados, visitor pattern
- Type checker: inferência de tipos básica
- Bytecode VM: stack-based virtual machine
- REPL interactivo
- **LSP Server **
	- Hover: mostra tipo de variáveis
	- Diagnostics: erros de tipo em tempo real
	- Completion: sugestões de variáveis e funções
	- Go to definition
	- VS Code extension que usa o LSP
## Entregáveis

- [ ] Interpretador funcional + VS Code extension
- [ ] Language specification em Markdown
- [ ] Blog series (4 partes): Lexer / Parser / Type System / LSP
- [ ] Video: Escrever código na linguagem própria com autocomplete no VS Code
