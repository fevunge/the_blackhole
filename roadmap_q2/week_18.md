# Python Avançado + Data Engineering Moderno
#week 
 

## Objectivos

- Python avançado: decorators, generators, context managers, descriptors, `__slots__`
- Type system moderno: `mypy` strict, `TypeVar`, `Protocol`, `TypedDict`, `ParamSpec`
- `asyncio` com `TaskGroup` (Python 3.11+) e `asyncio.timeout`
- Polars — o substituto de Pandas para performance (10-100x mais rápido)
- DuckDB — SQL analítico em processo, substitui Spark para datasets médios

## Recursos

| Tipo    | Recurso                                             |
| ------- | --------------------------------------------------- |
| Livro   | _Fluent Python_ (2ª edição, 2022) — Luciano Ramalho |
| Docs    | Polars user guide — pola.rs                         |
| Docs    | DuckDB documentation — duckdb.org                   |
| Blog    | pythonspeed.com — performance em Python             |
| Prática | Python Morsels — morsels.com (free tier)            |

# Projeto
### Modern ETL Pipeline Framework com Polars + DuckDB

**Tech Stack** 
	Python 3.12 + Polars + DuckDB + Prefect + FastAPI + Pydantic v2

**Overview**
	Um **framework de ETL** moderno e de alta performance que torna o processamento de dados **10-100x** mais rápido que pipelines tradicionais baseados em Pandas.
	O framework tem três camadas: 
	- **Extract** suporta REST APIs com rate limiting inteligente e retry automático, ficheiros CSV/Excel/Parquet/JSON via Polars native, bases de dados via DuckDB JDBC, e web scraping assíncrono com `httpx` e `selectolax`; 
	- **Transform** usa Polars com lazy evaluation para processar milhões de linhas sem carregar tudo em memória, com data quality checks automáticos via Great Expectations e detecção de schema drift; 
	- **Load** suporta PostgreSQL com batch inserts optimizados, Parquet columnar, e DuckDB para análise local instantânea. 
	A orquestração usa Prefect com retry automático, DAG visualization, e alertas em caso de falha. O projecto inclui benchmarks obrigatórios de Polars vs Pandas em 1M, 10M e 100M rows, lineage tracking para rastrear a origem de cada dado transformado, e publicação como PyPI package. O diferencial prático é um exemplo real: pipeline que processa dados de uma API pública, transforma, e produz um relatório analítico — tudo em segundos onde pandas levaria minutos.

**Core Features**
- **Extract**
	-  REST APIs com rate limiting inteligente e retry
	- CSV/Excel/Parquet/JSON files (Polars nativo)
	- PostgreSQL e SQLite (via DuckDB JDBC)
	- Web scraping assíncrono (`httpx` + `selectolax`)
	- Google Sheets API (gratuita)

```python
# Exemplo: 1M rows em <1s com Polars lazy evaluation
df = (
    pl.scan_parquet("data/*.parquet")
    .filter(pl.col("date") >= pl.lit("2025-01-01"))
    .group_by("category")
    .agg([
        pl.col("revenue").sum().alias("total_revenue"),
        pl.col("user_id").n_unique().alias("unique_users"),
    ])
    .sort("total_revenue", descending=True)
    .collect()
)
```

- **Load:**
	- PostgreSQL batch inserts optimizados
	- Parquet (formato columnar eficiente)
	- DuckDB (análise local instantânea)
- **Orchestration:**
	- Prefect flows com retry automático
	- DAG visualization
	- Alertas em caso de falha (email + webhook)
- Data quality checks automáticos (Great Expectations)
- Schema evolution detection
- Lineage tracking (quais dados vieram de onde)

### Entregáveis

- [ ] PyPI package publicado
- [ ] Blog: "Polars + DuckDB — Why Pandas + Spark Is Overkill for Most Teams in 2026"
- [ ] Benchmark: Polars vs Pandas em 1M/10M/100M rows (gráfico)
- [ ] Video: pipeline completo do zero ao relatório analítico