# Performance Engineering — Profiling & Optimization
#week 

## Objectivos
- Profiling: flame graphs, CPU profiling, memory profiling
- CPU architecture: cache hierarchy, branch prediction, SIMD
- Micro-benchmarking correcto: evitar pitfalls do benchmarking
- Memory optimization: cache-friendly data structures, pool allocation
- Concurrency performance: amdahl's law, false sharing, lock contention

## Recursos

| Tipo  | Recurso                                                                           |
| ----- | --------------------------------------------------------------------------------- |
| Livro | _Systems Performance_ — Brendan Gregg (2ª edição)                                 |
| Site  | brendangregg.com — flame graphs e performance tools                               |
| Video | "Performance Matters" — Emery Berger (Strange Loop 2019 — YouTube)                |
| Tools | perf (Linux), pprof (Go), flamegraph.pl, valgrind --callgrind                     |
| Blog  | "What scientists must know about hardware to write fast code" — Jakob Nybo Nissen |

## Projeto
### Performance Optimization Case Studies

**Overview**
	Vais pegar em três projectos anteriores e optimizá-los sistematicamente usando uma metodologia rigorosa de profiling — não por intuição, mas por dados. Este é o projecto que separa engineers que "acham que o código é lento" de engineers que "sabem exactamente onde e porquê e em quanto" antes de escrever uma linha. Para cada projecto: estabeleces um baseline benchmark antes de qualquer mudança; profiles com as ferramentas correctas (pprof para Go, perf + flamegraph para C++, cProfile + py-spy para Python); formulas uma hipótese específica sobre o gargalo; fazes a menor mudança possível que testa essa hipótese; e medes novamente comparando com o baseline.

**Caso 1 — Web Crawler ([[week_4]]):**
- Profile com pprof
- Identifica gargalo (suspeita: JSON parsing, DB writes)
- Optimiza: batch writes, buffer pool, zero-copy parsing
- Meta: 2x throughput

**Caso 2 — Path Tracer ([[week_23]]):**
- Profile com perf + flamegraph
- Identifica: BVH traversal hot path
- Optimiza: SIMD para ray-AABB intersection, cache-friendly BVH layout
- Meta: 1.5x speedup

**Caso 3 — Storage Engine ([[week_35]]):**
- Profile: onde vai o tempo em writes sequenciais?
- Optimiza: batch WAL writes, mmap reads, Bloom filter SIMD
- Meta: 30% throughput improvement

**Metodologia obrigatória para cada caso**

```
1. Baseline measurement (benchmark antes)
2. Profile (não adivinhar)
3. Hypothesis (o que vai melhorar e porquê)
4. Change (mínimo possível)
5. Measure (comparar com baseline)
6. Document
```

## Entregáveis
- [ ] Repositório de cada optimização com before/after benchmarks
- [ ] Blog: "The Art of Performance Optimization — A Systematic Approach"
- [ ] Flame graphs gerados e anotados
- [ ] Video: ao vivo de uma sessão de profiling e optimização
