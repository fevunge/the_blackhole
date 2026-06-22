# C++20 STL & Algorithms + WebAssembly
#week 

## Objectivos

- STL algorithms (`<algorithm>`, `<ranges>`, `<numeric>`) — cada algoritmo e quando usar
- Function objects, lambdas com captures, partial application
- C++20 Ranges e Views — programação funcional em C++ sem overhead
- Concepts — type constraints legíveis que substituem SFINAE
- Complexity analysis real de cada algoritmo STL

##  Recursos

| Tipo    | Recurso                                      |
| ------- | -------------------------------------------- |
| Livro   | _Effective STL_ — Scott Meyers               |
| Prática | Codeforces — contests em C++                 |
| Ref     | cppreference.com/w/cpp/algorithm             |
| Video   | CppCon 2023 — "C++20 Ranges" talks           |
| Site    | compiler-explorer.com — vê o assembly gerado |

## Projeto
### Algorithm Visualizer — C++ compilado para WebAssembly

**Tech Stack**
	C++20 + Emscripten + React + TypeScript + Canvas API
**Overview**
	Um visualizador interativo de algoritmos que corre directamente no browser via WebAssembly — o core dos algoritmos está implementado em C++20 e compilado com Emscripten, enquanto o frontend em React com TypeScript faz a visualização via Canvas API.
	A vantagem de usar Wasm em vez de JavaScript puro é real e mensurável: *os algoritmos correm à velocidade nativa do C++ no browser, sem servidor, sem instalação.* 
	O visualizador tem de mostrar, passo a passo com controlo de velocidade, pelo menos 8 algoritmos de sorting, os principais algoritmos de grafos (**DFS, BFS, Dijkstra, A*, Kruskal, Prim**), e operações em árvores (**AVL rotations, Red-Black insertions**).
	Para cada step, mostras o código-fonte real com highlighting sincronizado com o estado actual da estrutura de dados, estatísticas em tempo real (comparações, swaps, memória usada), e comparação side-by-side de dois algoritmos.
	O projecto é publicado como PWA que funciona offline, e exporta animações como GIF para usar em blog posts.
	
**Core Features:**
- Step-by-step com controlo de velocidade
- Comparação side-by-side de dois algoritmos
- Estatísticas em tempo real: comparações, swaps, memória
- Input customizado (array manual ou gerado)
- Code highlighting sincronizado com o step actual
- Export do resultado como GIF (para blog posts)
- Memory usage tracking

**Requisitos Técnicos**
- Sorting: Bubble, Selection, Insertion, Quick, Merge, Heap, Radix, Tim
- Graph: DFS, BFS, Dijkstra, A*, Bellman-Ford, Kruskal, Prim
- Trees: AVL rotations, Red-Black insertions, B-tree operations
- Templates para genéricos
- Custom iterators
- Performance benchmarks
- Unit tests (Google Test)

**Entregáveis**
- [ ] Web app publicada no GitHub Pages (funciona no browser, zero instalação)
- [ ] Blog: "Compiling C++20 to WebAssembly — Building an Algorithm Visualizer"
- [ ] YouTube: Demo + explicação da arquitectura Wasm
- [ ] Artigo comparativo: complexidade dos algoritmos com benchmarks reais

