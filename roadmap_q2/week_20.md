# Deep Learning + Fine-tuning de Modelos Modernos
#week 

## Objectivos
- Neural networks: forward pass, backpropagation, gradients — matemática visual
- PyTorch: tensors, autograd, `nn.Module`, optimizers, learning rate schedulers
- Transfer learning: porque funciona e como aplicar correctamente
- Fine-tuning vs feature extraction — quando usar cada abordagem
- LoRA/QLoRA: fine-tuning eficiente de LLMs sem GPU cara
- Fine-tuning de LLMs pequenos com LoRA/QLoRA (gratuito no Colab)

## Recursos

| Tipo       | Recurso                                                            |
| ---------- | ------------------------------------------------------------------ |
| Course     | fast.ai Deep Learning — gratuito                                   |
| Docs       | PyTorch tutorials — pytorch.org/tutorials                          |
| Plataforma | Kaggle Notebooks com GPU — gratuito (30h/semana)                   |
| Plataforma | Google Colab Pro substituto: Kaggle é melhor em 2026               |
| Blog       | Sebastian Raschka — "LLM Fine-tuning" series (newsletter gratuita) |

## Projeto
### Document Intelligence System com Fine-tuned Model

**Tech Stack**
	Python + PyTorch + Hugging Face Transformers + LoRA + FastAPI + React

**Overview** 
	Um sistema que extrai informação estruturada de documentos não-estruturados (PDFs de recibos, contratos, formulários, facturas) através de fine-tuning de um modelo de document understanding — o tipo de sistema que empresas de automação documental vendem por centenas de milhares. O pipeline começa com pré-processamento de documentos (PDF → imagem → normalização), passa por um modelo LayoutLMv3 ou Donut fine-tuned com LoRA em datasets públicos (CORD para recibos, FUNSD para formulários) no Kaggle gratuito com GPU, e produz JSON estruturado com os campos extraídos e as suas bounding boxes no documento original. O fine-tuning usa QLoRA para caber na GPU gratuita do Kaggle (30h/semana), alcança >85% de accuracy em field extraction, e o modelo treinado é publicado no Hugging Face Hub. A interface web React permite upload de documentos, mostra as bounding boxes coloridas sobre o documento, e o JSON editável. O sistema está desenhado para ser extensível: podes adicionar novos tipos de documento treinando com mais exemplos sem alterar o código.

**Core Features**
- Train custom models
- Transfer learning (ResNet, EfficientNet)
- Data augmentation
- Model fine-tuning
- Web interface para upload
- Real-time prediction API
- Batch processing
- Confidence scores
- Grad-CAM visualization
- Model comparison
- **Pipeline**
	1. Documento (PDF/imagem) → pré-processamento
	2. Fine-tuned LayoutLM ou Donut model → extracção de campos
	3. Post-processamento → JSON estruturado
	4. API endpoint → integração com outros sistemas
- **Datasets**
	- CIFAR-10 (baseline)
	- Custom dataset (scraping + labeling)
	- Data augmentation pipeline
- **Fine-tuning (Colab gratuito)**
	- Dataset: CORD (receipts), FUNSD (formulários) — datasets públicos
	- Modelo base: microsoft/layoutlmv3-base ou naver-clova-ix/donut-base
	- LoRA para reduzir memória necessária (cabe no Colab gratuito)
	- Accuracy target: >85% em field extraction
- **Web Interface**
	- Upload de documento
	- Visualização das bounding boxes extraídas
	- JSON output editável
	- Export para Excel/CSV
- **Deployment**
	- ONNX export
	- TorchScript optimization
	- API com FastAPI
	- Docker container

## Entregáveis

- [ ] Modelo fine-tuned publicado no Hugging Face Hub (gratuito)
- [ ] API + Web interface deployada
- [ ] Blog: "Fine-tuning Document AI Models with LoRA — A Practical Guide"
- [ ] Video: Do PDF ao JSON estruturado em segundos
- [ ] Kaggle notebook público com o processo de fine-tuning
