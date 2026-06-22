# Advanced Algorithms + Competitive Programming
#s_week 

## Objectivos
- Advanced trees: B-trees, Red-Black trees, Segment trees, Fenwick trees
- Graph algorithms: Bellman-Ford, Floyd-Warshall, A*, max-flow (Ford-Fulkerson)
- String algorithms: KMP, Z-algorithm, Rabin-Karp, Suffix Arrays
- Advanced DP: bitmask DP, divide and conquer DP, knuth optimization
- Geometry: convex hull, line intersection, closest pair

## Recursos

| Tipo    | Recurso                                                    |
| ------- | ---------------------------------------------------------- |
| Livro   | _Introduction to Algorithms_ (CLRS) — caps. seleccionados  |
| Prática | Codeforces — contests regulares gratuitos                  |
| Prática | AtCoder — editorial muito educativo                        |
| Site    | cp-algorithms.com — algoritmos com provas e implementações |
| Viz     | VisuAlgo — visualgo.net                                    |

## Projeto
### Competitive Programming Platform — Interactive Learning


**Tech Stack** 
	React + TypeScript + Canvas API (visualizações) + Go (judge backend)

**Overview**
	Uma plataforma web para aprender algoritmos de forma interactiva — como o LeetCode mas com visualizações passo a passo sincronizadas com código e um juiz de código online, tudo construído por ti. A plataforma tem duas áreas principais: a área de aprendizagem visualiza algoritmos interactivamente no Canvas API com controlo de velocidade, visualização do estado interno (heap, stack, memória), e código-fonte em highlighting sincronizado com cada step; a área de desafios tem um editor de código online com execução num sandbox Go no backend com timeout e memory limits, e diff automático do output. Os algoritmos implementados cobrem sorting (8 algoritmos side-by-side), grafos (DFS, BFS, Dijkstra, A*, Kruskal, Prim), árvores (AVL rotations passo a passo, Red-Black insertions, Segment tree updates), strings (KMP failure function animada, Z-array, Suffix Array), e DP (tabelas de LCS, Knapsack preenchidas em tempo real). O quiz mode pergunta "qual o próximo estado?" para verificar se realmente entendes ou só estás a ver. Esta semana inclui também 50+ problemas LeetCode com foco em padrões avançados.

**Features:**

- Editor de código online com execução (Go sandbox no backend)
- Step-by-step com velocidade ajustável e código sincronizado
- Complexidade de tempo e espaço por step
- Quiz mode: "Qual o próximo passo?"
- Challenge mode: implementa o algoritmo e valida
- **Judge Backend (Go):**
	- Executa código em sandbox seguro
	- Timeout e memory limit
	- Diff de output

**Requisitos**
- Sorting: 8 algoritmos com comparação side-by-side
- Graph: DFS, BFS, Dijkstra, A*, Kruskal, Prim
- Trees: AVL rotations, Red-Black insertions, Segment tree updates
- Strings: KMP failure function, Z-array, Suffix Array construction
- DP: LCS, Knapsack, Matrix Chain — visualização da tabela


## Entregáveis
- [ ] Web app publicada e funcional
- [ ] Blog: "How I Built an Interactive Algorithm Visualizer"
- [ ] Video: walkthrough da plataforma
- [ ] 50+ LeetCode problems resolvidos nesta semana

---

# **_Bônus [11]_**
## Performance, Escalabilidade & Resiliência

**Objectivo** 
	Arquitectar sistemas que sobrevivem ao sucesso.

###  Recursos Obrigatórios

| Tipo   | Recurso                                                                                                      |
| ------ | ------------------------------------------------------------------------------------------------------------ |
| Livro  | _Designing Data-Intensive Applications_ — Kleppmann (caps. 7–12) — continuação do Bloco 5                    |
| Artigo | "The Architecture of Open Source Applications" — Vol 1 & 2 (aosabook.org — **gratuito online**)              |
| Vídeo  | ["Scalability Harvard Web Development" — David Malan (YouTube)](https://www.youtube.com/watch?v=-W9F__D3oY4) |
| Artigo | "Chaos Engineering" — Principles of Chaos (principlesofchaos.org)                                            |
| Site   | [High Scalability Blog](http://highscalability.com/) — casos reais de escalabilidade                         |

### PROJECTO: _"Capacity Planning & Scalability Design"_

**Overview** 
	Para um sistema de streaming de vídeo fictício que quer passar de 1.000 para 1.000.000 utilizadores simultâneos:

- Cálculos de capacity planning (bandwidth, storage, compute)
- Estratégia de caching (CDN, Redis, in-memory)
- Estratégia de sharding/particionamento de dados
- Padrões de resiliência: Circuit Breaker, Bulkhead, Timeout
- Plano de Chaos Engineering para validar resiliência

**Entrega** 
	Documento LaTeX com cálculos justificados + diagramas de escalabilidade

