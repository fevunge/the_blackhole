# C++ Fundamentals + Memory Management
#week 

## Objectivos
- C++ moderno (C++20/23): syntax, compilation model, standards
- Smart pointers: `unique_ptr`, `shared_ptr`, `weak_ptr` — quando usar cada um
- RAII pattern — o princípio mais importante do C++
- Move semantics e perfect forwarding — evitar cópias desnecessárias
- Templates básicos e dedução de tipos com `auto`
- STL containers: vector, list, map, unordered_map, deque — quando usar qual

##  Recursos

| Tipo    | Recurso                                                |
| ------- | ------------------------------------------------------ |
| Livro   | _A Tour of C++_ (3ª edição, 2023) — Bjarne Stroustrup  |
| Site    | learncpp.com — o melhor tutorial gratuito de C++       |
| Prática | Exercism C++ track                                     |
| Video   | CppCon talks no YouTube ("CppCon 2023 back to basics") |
| Ref     | cppreference.com — referência definitiva               |

## Projeto

### Custom STL Containers — Vector + HashMap

**Tech Stack:**
	C++20 puro

**Overview**
	Reimplementar `std::vector` e `std::unordered_map` do zero em C++20,  com standards modernos. 
	Essa é a forma mais eficaz de entender o que acontece por baixo de todo o código C++ que escreves.
	O teu `ft_vector<T>` tem de implementar todos os métodos do equivalente standard: **push_back, emplace_back, insert, erase, resize, reserve, iterators bidirecionais, exception safety com strong guarantee em todos os métodos mutadores, e compatibilidade com C++20 Ranges**. 
	O teu `ft_hashmap<K,V>` usa **open addressing com Robin Hood hashing** (mais cache-friendly que chaining), **tombstones** para deletes eficientes, e load factor configurável.
	Para ambos: zero memory leaks confirmado via Valgrind e AddressSanitizer, benchmarks que ficam a menos de 10% do std em operações core, e documentação Doxygen completa.

**Arquitetura**
```cpp
template<typename T, typename Allocator = std::allocator<T>>
class ft_vector {
    // Growth factor configurável (default: 2x)
    // Iterator: random access, bidirectional, C++20 ranges compatible
    // Exception safety: strong guarantee em push_back, insert, emplace
    // Move semantics: move constructor e move assignment
};

template<typename K, typename V, typename Hash = std::hash<K>>
class ft_hashmap {
    // Robin Hood hashing — reduz variance do probe length
    // Tombstone deletion — O(1) delete sem rehash
    // Load factor max: 0.7 (configurável)
    // Resize automático quando load factor excedido
};
```

**Requisitos Técnicos**
- Todos os métodos do std equivalente implementados
- Benchmarks: deve estar a <10% do std em operações core
- Exception safe (strong guarantee)
- Valgrind + AddressSanitizer: zero leaks, zero UB
- Google Test suite completo com edge cases
- Documentação Doxygen gerada automaticamente
- Valgrind + AddressSanitizer zero errors
- Google Test suite com edge cases, benchmarks vs std com tabela comparativa
- Documentação Doxygen gerada por CI;

**Entregáveis**
- [ ] Biblioteca header-only compilável com CMake
- [ ] Big O de cada operação em tabela markdown
- [ ] Memory layout diagrams (draws.io ou ASCII art)
- [ ] Comparação de performance vs `std::` em diferentes tamanhos
- [ ] Benchmark report com tabela e gráficos
- [ ] Blog: "Implementing std::vector and std::unordered_map from Scratch in C++20"
- [ ] YouTube: time-lapse de desenvolvimento + explicação técnica
---





