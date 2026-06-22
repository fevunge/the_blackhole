# Machine Learning Fundamentals
#week 

## Objetivos
- ML pipeline completo: dados → features → treino → avaliação → deploy
- Supervised learning: regressão, classificação, árvores de decisão, ensemble methods
- Avaliação correcta: cross-validation, métricas por tipo de problema
- Feature engineering: encoding, scaling, imputation, feature selection
- MLflow: experiment tracking, model registry, model serving

## Recursos

| Tipo       | Recurso                                                          |
| ---------- | ---------------------------------------------------------------- |
| Course     | fast.ai — Practical Machine Learning (fastai.fast.ai — gratuito) |
| Livro      | _Hands-On Machine Learning_ (3ª edição) — Aurélien Géron         |
| Prática    | Kaggle Learn — micro-courses gratuitos                           |
| Plataforma | Google Colab — GPU gratuita                                      |
| Docs       | scikit-learn documentation — sklearn.org                         |

## Projeto
### AutoML Platform — Train, Compare, Deploy sem Código

**Tech Stack**
	Python + scikit-learn + LightGBM + MLflow + Optuna + FastAPI + Streamlit

**Overview**
	Uma plataforma web que permite a qualquer pessoa — mesmo sem saber Python — fazer upload de um dataset, treinar e comparar múltiplos modelos de machine learning, e obter um endpoint de API para fazer predictions, tudo via interface gráfica. O backend Python usa scikit-learn para os modelos clássicos, LightGBM para gradient boosting de alta performance, Optuna para hyperparameter tuning com bayesian optimization (mais eficiente que grid search para grandes espaços), e MLflow para tracking automático de cada experimento. A análise exploratória automática detecta o tipo de problema (classificação vs regressão), distribui as features, calcula correlações, identifica missing values e outliers, e sugere transformações adequadas. O AutoML treina 8+ algoritmos em paralelo, compara métricas numa tabela interactiva, e visualiza as curves de aprendizagem. O modelo vencedor é exportado automaticamente para ONNX (formato universal) e um endpoint FastAPI é gerado com o schema correcto de input/output. SHAP values explicam as previsões ao nível de feature individual, tornando o modelo interpretável mesmo para não-técnicos. Deploya na Hugging Face Spaces (gratuito) para que qualquer pessoa possa testar.

**Core Features**
- Upload de dataset (CSV, Excel, Parquet)
- Automated EDA: distribuições, correlações, missing values, outliers
- Feature engineering automático: encoding, scaling, imputation
- AutoML: treina 8+ algoritmos e compara
- Hyperparameter tuning: Optuna (bayesian optimization — mais eficiente que grid search)
- Cross-validation com N folds
- Model comparison dashboard interactivo
- Export: pickle, ONNX, joblib
- API endpoint gerado automaticamente para predictions
- MLflow tracking integrado: cada treino logado

**Requisitos (algoritmos)**
- Linear/Logistic Regression (baseline)
- Random Forest, Gradient Boosting (LightGBM, XGBoost, CatBoost)
- SVM, k-NN, Naive Bayes
- Simple Neural Network (MLPClassifier)
- Interpretability: SHAP values para explicar previsões.

## Entregáveis

- [ ] Web app funcional (Streamlit), deployada no Hugging Face Spaces (gratuito)
- [ ] Blog: "Building AutoML from Scratch — What AutoML Libraries Don't Tell You"
- [ ] Kaggle competition entry usando a plataforma
- [ ] Video: Treinar um modelo em 5 minutos sem código