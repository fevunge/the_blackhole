# Microserviços & Event-Driven Architecture

**Objectivo** 
	Dominar os padrões modernos de decomposição de sistemas.

### Recursos Obrigatórios

| Tipo   | Recurso                                                                                                                                 |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| Livro  | _Building Microservices_ — Sam Newman (2ª edição) (caps. 1–8)                                                                           |
| Livro  | _Designing Event-Driven Systems_ — Ben Stopford (gratuito no Confluent website)                                                         |
| Vídeo  | ["GOTO 2019 — "The Many Meanings of Event-Driven Architecture"" — Martin Fowler (YouTube)](https://www.youtube.com/watch?v=STKCRSUsyP0) |
| Artigo | "Saga Pattern" — Chris Richardson (microservices.io)                                                                                    |
| Site   | [microservices.io](https://microservices.io/) — catálogo completo de padrões, por Chris Richardson                                      |

### PROJECTO: _"Decomposição de Monólito em Microserviços"_

**Overview** 
	Parte de um projeto web open-source monólito do github. Faz um fork aplicando a técnica Strangler Fig Pattern para decompor gradualmente em micro serviços. Documenta:

- Identificação de bounded contexts
- Estratégia de decomposição (por domínio, capacidade, etc.)
- Gestão de dados distribuídos (cada serviço tem a sua DB)
- Comunicação: sync (REST/gRPC) vs async (eventos)
- Padrão Saga para transacções distribuídas

**Entrega** 
	Documento LaTeX + diagramas C4 antes/depois + diagrama de eventos

