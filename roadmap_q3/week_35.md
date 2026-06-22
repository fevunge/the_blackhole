# Distributed Database — Storage Engine do Zero
#week 

## Objectivos
- B-tree e LSM-tree: os dois storage engines dominantes
- Write-Ahead Log (WAL): durabilidade sem flush por operação
- MVCC (Multi-Version Concurrency Control): transactions sem locks em reads
- Compaction: como o LevelDB e o RocksDB limpam dados antigos
- Recovery: como a DB recupera após crash

## Recursos

| Tipo   | Recurso                                                             |
| ------ | ------------------------------------------------------------------- |
| Livro  | _Database Internals_ — Alex Petrov (o melhor livro sobre este tema) |
| Paper  | "The Log-Structured Merge-Tree" — O'Neil et al.                     |
| Código | LevelDB source code — github.com/google/leveldb                     |
| Video  | CMU 15-445 Database Internals — lectures no YouTube                 |
| Blog   | "How SQLite Works" — phiresky.github.io                             |

## Projeto
### Storage Engine — LSM-Tree em Go

**Tech Stack** 
	Go + mmap

**Overview**
	Um storage engine baseado em LSM-Tree (Log-Structured Merge-Tree) — a estrutura de dados que está no coração do RocksDB, Cassandra, LevelDB, e muitos outros sistemas de base de dados modernos. O LSM-Tree é optimizado para writes de alta velocidade: em vez de escrever directamente no disco em posição aleatória (que é lento), escreve sequencialmente no WAL para durabilidade e na MemTable em memória para velocidade, e periodicamente faz flush para SSTables imutáveis e ordenadas no disco. O Write-Ahead Log garante que nenhum dado se perde num crash — ao reiniciar, fazes replay do WAL para reconstruir a MemTable. As SSTables têm um Bloom Filter (que implementas do zero) para evitar disk reads desnecessários em GETs de keys que não existem, e um índice esparso para binary search eficiente. O processo de compaction funde SSTables de L0 em L1, L2, L3 com sorted runs sem overlaps para reduzir write amplification. O MVCC usa timestamps em cada entry para que reads vejam um snapshot consistente sem bloquear writes. Benchmarks obrigatórios contra BadgerDB (LSM em Go, open-source) mostram onde estás em relação a uma implementação madura.

**Componentes do LSM-Tree:**

```
Writes → MemTable (skip list in-memory)
              ↓ (quando cheio)
         WAL flush + SSTable flush
              ↓
         L0 SSTables (ordenadas por key)
              ↓ (compaction)
         L1, L2, L3 (sorted, no overlaps)
              ↓
Reads: MemTable → Bloom Filter → Binary Search em SSTable
```

**Implementação detalhada:**

- **MemTable**: skip list com O(log n) reads e writes
- **WAL**: append-only log para durabilidade, recovery após crash
- **SSTable**: ficheiro imutável ordenado por key, com índice esparso e Bloom filter
- **Bloom Filter**: implementado do zero, zero false negatives, configurable false positive rate
- **Compaction**: size-tiered compaction (como Cassandra)
- **MVCC**: cada write tem um timestamp, reads vêem snapshot consistente

**Benchmarks vs RocksDB:**

- Sequential write throughput
- Random read throughput
- Space amplification
- Write amplification

## Entregáveis

- [ ] Storage engine funcional com testes de correctness
- [ ] Blog: "Building an LSM-Tree Storage Engine — How RocksDB Works Under the Hood"
- [ ] Whitepaper: design doc com decisões e trade-offs
- [ ] Benchmark: comparação com BadgerDB (LSM em Go, open-source)
