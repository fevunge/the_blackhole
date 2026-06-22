# Computer Vision — YOLOv11 & Real-time Object Detection, Tracking & Analytics 
#week 

## Objectivos
- Computer vision pipeline: captura → pre-processing → inference → post-processing
- Object detection: YOLO architecture (v8/v11 em 2026)
- Object tracking: SORT, ByteTrack
- Video processing: frame extraction, FPS management, ROI-based inference
- OpenCV: transformações, filtros, morphological operations

## Recursos

| Tipo    | Recurso                                              |
| ------- | ---------------------------------------------------- |
| Docs    | Ultralytics YOLOv11 docs — docs.ultralytics.com      |
| Course  | OpenCV University — opencv.org/university (gratuito) |
| Prática | Kaggle Computer Vision competitions                  |
| Video   | "YOLOv8/v11 Tutorial" — Nicholas Renotte (YouTube)   |
| Paper   | ByteTrack paper — arxiv.org                          |

## Projeto
### Real-time Video Analytics Platform

**Tech Stack**
	Python + YOLOv11 + ByteTrack + ONNX Runtime + FastAPI + React + WebRTC

**Overview**
	Um sistema de análise de vídeo em tempo real com casos de uso práticos e reais: contagem de pessoas numa área, detecção de objectos específicos, análise de fluxo de movimento, e geração de heatmaps de presença. O sistema usa YOLOv11 na variante nano (corre em tempo real em CPU moderno sem GPU), exportado para ONNX Runtime para máxima performance, com ByteTrack a manter IDs consistentes de cada objecto entre frames para que possas calcular trajectórias e tempo de permanência em zonas configuráveis. O backend FastAPI recebe vídeo via WebRTC ou ficheiro, processa frame a frame com a pipeline optimizada (frame skipping inteligente baseado em motion detection, processamento apenas na ROI relevante), e expõe resultados via WebSocket ao dashboard React. O dashboard mostra o vídeo annotated em tempo real, heatmaps de movimento, estatísticas de contagem, e triggers de eventos configuráveis (pessoa parada por mais de X segundos, entrada em zona proibida, contagem acima de threshold). O projecto inclui benchmarks de FPS em diferentes configurações de hardware e um modo de exportação de clips quando eventos são detectados.

**Core Features**
- Object detection com YOLOv11 (ONNX export para CPU — sem GPU necessária)
- Multi-object tracking com ByteTrack (IDs consistentes entre frames)
- People counting com zona de interesse configurável
- Heatmap de movimento (densidade de presença)
- Detecção de eventos: pessoa parada >30s, zona proibida, etc.
- Dashboard com estatísticas em tempo real
- Recording de clips quando evento detectado
- Export de relatórios

**Requisitos**
- **Optimizações para CPU:**
	- YOLOv11n (nano) — corre em tempo real em CPU moderno
	- Frame skipping inteligente baseado em movimento
	- ROI-based inference (só processa zona relevante)
	- TensorRT / ONNX Runtime optimizado
- **Pipeline:**	
	```
	Webcam/Video → Frame Queue → YOLO Inference
                                   ↓
                             ByteTrack → Events
                                   ↓
                          WebSocket → React Dashboard
	```

## Entregáveis

- [ ] Sistema funcional com webcam ou ficheiro de vídeo
- [ ] Blog: "Building a Real-time Video Analytics System in 2026"
- [ ] Video: Demo completo do sistema
- [ ] Benchmark: FPS em diferentes hardware configs
