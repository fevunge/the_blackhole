# AI Engineering — RAG, Agents & LLM Integration
#week 

## Objectivos
- RAG (Retrieval Augmented Generation): arquitectura e implementação
- Vector databases: embeddings, similarity search, HNSW index
- LLM APIs: OpenAI-compatible APIs (Ollama local — gratuito)
- AI Agents: function calling, tool use, chain-of-thought
- Evaluation de sistemas RAG: métricas e benchmarks

## Recursos

| Tipo   | Recurso                                                                      |
| ------ | ---------------------------------------------------------------------------- |
| Docs   | Ollama — ollama.ai (LLMs locais, gratuito)                                   |
| Paper  | "Retrieval-Augmented Generation" — Lewis et al. (paper original)             |
| Course | deeplearning.ai — "Building Systems with ChatGPT API" (gratuito com registo) |
| Video  | "RAG from Scratch" — LangChain YouTube channel                               |
| Tool   | Qdrant — vector DB open-source com Docker                                    |

## Projeto
### AI Knowledge Base — RAG System Completo

**Tech Stack** 
	Python + Ollama (LLM local) + Qdrant (vector DB) + FastAPI + React

**Overview**
	Construir um sistema RAG (Retrieval Augmented Generation) production-ready que responde perguntas sobre documentação técnica com citações de fontes — tudo local, sem pagar nenhuma API. O pipeline ingere documentos em PDF, Markdown, TXT e URLs via scraping, faz chunking recursivo com overlap configurável para preservar contexto entre chunks, gera embeddings com o modelo `nomic-embed-text` via Ollama (gratuito, local), e indexa num Qdrant (vector database open-source em Docker) com HNSW index para similarity search O(log n). Quando um utilizador faz uma pergunta, o sistema faz hybrid search: busca semântica com os embeddings mais um BM25 keyword search, combina os resultados com Reciprocal Rank Fusion, e passa os top-K chunks mais um cross-encoder re-ranker para ordenação final. O contexto retrived é enviado ao `llama3.1` ou `mistral` via Ollama para geração da resposta com streaming SSE. O sistema suporta AI Agents com tool use: a LLM pode chamar uma calculadora, fazer web search (via SearXNG self-hosted), e executar snippets de código para responder perguntas que requerem computação. O RAGAS evaluation dashboard mede automaticamente faithfulness, answer relevancy e context precision.

**Core Features**

- Ingestão de documentos: PDF, Markdown, TXT, URLs (web scraping)
- Chunking estratégico com overlap configurável
- Hybrid search: semântica + keyword (BM25)
- Re-ranking com cross-encoder (mais preciso)
- Streaming de respostas (SSE)
- Source citations com highlights
- **AI Agents:** o sistema pode usar tools (calculadora, web search, código)
- Evaluation dashboard: RAGAS metrics automáticas
- `ollama run llama3.1` — LLM gratuito e privado
- Qdrant em Docker — vector DB sem custo
- Zero chamadas a APIs pagas

**Pipeline RAG:**

```
Documents (PDF, MD, TXT)
    ↓
Chunking (recursive, semantic, sliding window)
    ↓
Embedding (nomic-embed-text via Ollama — gratuito)
    ↓
Qdrant (HNSW index, cosine similarity)
    ↓
Query → Embed → Search → Retrieve top-K chunks
    ↓
Context + Query → LLM (llama3.1 ou mistral via Ollama)
    ↓
Generated Answer + Source Citations
```

## Entregáveis

- [ ] Sistema RAG funcional e deployado localmente
- [ ] Blog: "Building a Production RAG System with Zero API Costs in 2026"
- [ ] Evaluation report: métricas de precisão e recall
- [ ] Video: demo completo — ingere documentação → faz perguntas → respostas com fontes
