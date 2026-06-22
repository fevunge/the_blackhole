# C++ Advanced — Templates & Memory Allocators
#week 

## Objectivos
- Template specialization (full e partial) e quando usar cada uma
- SFINAE e `if contexpr`
- C++20 Concepts — substituição legível do SFINAE
- Variadic templates e fold expressions
- `constexpr` e `consteval` — computação garantida em compile-time
- Type traits e meta-programming

## Recursos

| Tipo    | Recurso                                                                 |
| ------- | ----------------------------------------------------------------------- |
| Livro   | _C++ Templates: The Complete Guide_ (2ª edição) — Vandevoorde, Josuttis |
| Ref     | cppreference.com — Concepts, Templates                                  |
| Prática | Template metaprogramming katas no Exercism                              |
| Site    | compiler-explorer.com — vê o que o compilador faz                       |
| Video   | CppCon 2023 — "C++20 Concepts in Practice"                              |

## Projeto
### Custom Memory Allocator Framework + Visualizador Web

**Tech Stack** 
	C++20 + Emscripten (Wasm) + React (visualizador) + Google Benchmark

**Overview**
	Um framework de allocators de memória customizáveis em C++20 com um visualizador web que mostra o layout de memória em tempo real via WebAssembly — um dos projectos mais instrutivos que podes fazer para entender performance de software a baixo nível. 
	Implementas quatro allocators com trade-offs distintos: 
	**Pool Allocator** para objectos de tamanho fixo com zero fragmentação e O(1) alloc/free; 
	**Stack/Linear Allocator** para alocações temporárias onde liberas tudo de uma vez em O(1); 
	**Free List Allocator** para alocações de propósito geral com baixa fragmentação;
	**Buddy System** para alocações em potências de dois com coalescing eficiente. 
	O visualizador React+Wasm mostra cada byte de memória colorido por estado (livre, alocado, metadata), uma timeline de allocs e frees, e a fragmentação calculada em tempo real. 
	Para cada allocator, produzes benchmarks comparativos contra `malloc` standard usando Google Benchmark, e versões thread-safe com `std::atomic`. O projecto usa Concepts para garantir em compile-time que só tipos corretos podem usar cada allocator.

**Core Features**
- Mapa de memória em tempo real (cada byte colorido por estado)
- Timeline de allocs/frees
- Fragmentação calculada ao vivo
- Memory tracking & leak detection
- Alignment suppor
- Comparação de performance: `malloc` vs cada allocator
- Thread-safe versions com `std::atomic` e lock-free queues
- Benchmark automático com critério de performance
- Detecção de double-free e use-after-free (debug mode)
	
**Requisitos**

```cpp
template<typename T, size_t PoolSize>
  requires std::is_trivially_destructible_v<T>
class PoolAllocator;          // Fixed-size, zero fragmentation

template<size_t Size>
class LinearAllocator;        // O(1) alloc, O(1) free-all

template<typename T>
class FreeListAllocator;      // General purpose, low fragmentation

template<size_t TotalSize, size_t MinBlock = 16>
class BuddyAllocator;         // Power-of-two, easy coalescing
```

**Entregáveis**
- [ ] Header-only library + visualizador web publicado
- [ ] Benchmark report vs malloc em operações típicas
- [ ] Blog: "Memory Allocators in C++20 — From Theory to Implementation"
- [ ] Video: visualizador em acção explicando fragmentação visualmente