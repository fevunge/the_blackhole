# Sistemas Distribuídos — Fundamentos

**Objectivo** 
	Entender os problemas reais de sistemas distribuídos: consistência, disponibilidade, particionamento.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                        |
| ------ | ------------------------------------------------------------------------------------------------------------------------------ |
| Livro  | _Designing Data-Intensive Applications_ — Martin Kleppmann (caps. 1–6) — **o livro mais importante de sistemas distribuídos**  |
| Vídeo  | [MIT 6.824 Distributed Systems — Lectures (YouTube)](https://www.youtube.com/playlist?list=PLrw6a1wE39_tb2fErI4-WkMbsvGQk9_UB) |
| Artigo | "CAP Theorem" — Eric Brewer (original paper, disponível online)                                                                |
| Artigo | "The Log: What every software engineer should know about real-time data" — Jay Kreps (LinkedIn Engineering)                    |
| Site   | [ByteByteGo Newsletter](https://blog.bytebytego.com/) — análises semanais de sistemas reais                                    |

### PROJECTO: _"Análise CAP — 3 Sistemas Reais"_

**Overview** Analisa 3 bases de dados/sistemas distribuídos reais:
- Cassandra
- PostgreSQL
- Kafka 

**E Mais importante o banco de dados do projeto [[week_9]]

Para cada um:

- Onde se posicionam no triângulo CAP?
- Que casos de uso servem melhor?
- Que trade-offs o arquitecto deve conhecer?

**Entrega** 
	Documento _LaTeX_ comparativo com tabela de trade-offs e recomendações por cenário de uso