# PROJECTO SHOWCASE #2 — MLOps Platform
#week 

## End-to-End MLOps Platform (Open-source)

**Tech Stack**
	Python + Go + Ray + MLflow + FastAPI + Prometheus + Grafana

**Overview**
	Vais construir uma plataforma MLOps completa que cobre todo o ciclo de vida de modelos de machine learning — da ingestão de dados ao deployment em produção com monitoring de data drift. O Data Pipeline em Python com Prefect gere ingestão de múltiplas fontes com data quality checks automáticos usando Great Expectations. O Feature Store em Redis e PostgreSQL persiste features computadas que podem ser reutilizadas por múltiplos modelos sem recomputação. A Training Platform usa Ray para distributed training em CPU (sem GPU necessária) e gere o ciclo completo: treina, avalia, regista no MLflow, e promove automaticamente se superar o modelo em produção no metric target. O Model Serving com Ray Serve e FastAPI expõe endpoints de inferência com batching automático para throughput máximo, versionamento por modelo, e canary deployments. O Monitoring detecta data drift comparando distribuições de features em produção vs distribuição de treino, e dispara alertas quando o drift excede thresholds configuráveis — o que aciona um auto-retrain com os dados recentes. Os modelos de exemplo usam os modelos que fine-tunaste na [[week_20]].

**Core Features**

1. **Data Pipeline** (Python + Prefect): ingestão, transformação, validação
2. **Feature Store** (Python + Redis + PostgreSQL): features reutilizáveis
3. **Training Platform** (Python + Ray): distributed training em CPU (sem GPU necessária)
4. **Experiment Tracking** (MLflow self-hosted): runs, metrics, artefacts
5. **Model Registry** (MLflow + MinIO): versionamento e staging
6. **Model Serving** (Python + FastAPI + Ray Serve): inference API escalável
7. **Monitoring** (Python + Prometheus + Grafana): data drift, prediction quality

- Classificação de sentimento (BERT fine-tuned via Projecto 20)
- Document extraction (LayoutLM via Projecto 20)
- Recommendation system (collaborative filtering)
- Time series forecasting (N-BEATS)

**Pipeline completo:**

```
Raw Data → Feature Store → Model Training → Registry
                                               ↓
                                     Model Serving (API)
                                               ↓
                                     Monitoring (drift alert)
                                               ↓
                                     Auto-retrain trigger
```

## Entregáveis
- [ ] Platform completa e funcional
- [ ] Blog series (4 posts)
- [ ] Video: workflow completo do dado ao model serving
- [ ] Comparison: self-hosted MLOps vs Vertex AI vs SageMaker (custo e features)

