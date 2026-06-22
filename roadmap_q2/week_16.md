# Sistemas Embarcados Simulados — RTOS & IoT
#week 

## Objectivos
- RTOS concepts: tasks, scheduler preemptivo, priorities, context switching
- FreeRTOS: tasks, queues, semaphores, mutexes, software timers
- MQTT protocol: publish/subscribe, QoS levels, retained messages, LWT
- Power management: sleep modes, wake-up triggers
- Watchdog timers e fault handling em sistemas críticos

## Recursos

| Tipo   | Recurso                                             |
| ------ | --------------------------------------------------- |
| Docs   | FreeRTOS documentation — freertos.org               |
| Sim    | Wokwi ESP32 Simulator — wokwi.com (gratuito)        |
| Livro  | _Real-Time Concepts for Embedded Systems_ — Qing Li |
| Video  | "FreeRTOS from Scratch" — Jacob Beningo (YouTube)   |
| Artigo | "MQTT Essentials" — HiveMQ blog                     |
## Projeto
### IoT Data Pipeline Completo — RTOS + Backend + Dashboard

**Tech Stack** 
	C++ com FreeRTOS (Wokwi) + Node.js + MQTT + TimescaleDB + React 
	**Hardware simulado no Wokwi:** DHT22, PIR, LDR, OLED SSD1306, LED RGB

**Overview**
	Um sistema IoT completo e funcionalmente realista, simulado no Wokwi: firmware para ESP32 com FreeRTOS a gerir múltiplas tasks concorrentes.
	Um backend Node.js como MQTT broker gateway, armazenamento de séries temporais em TimescaleDB, e um dashboard React com gráficos em tempo real.
	O firmware usa cinco tasks FreeRTOS com prioridades distintas
		**SensorTask** lê temperatura, humidade, luminosidade e movimento a cada 500ms e publica numa fila interna; **ProcessingTask** valida e normaliza as leituras descartando outliers; 
		**MQTTTask** consome a fila interna e publica os dados via MQTT com QoS 1 (acknowledged delivery); 
		**DisplayTask** actualiza o OLED SSD1306 com as leituras mais recentes;
		**WatchdogTask** reseta o sistema se qualquer task ficar bloqueada por mais de 5 segundos.
	O backend processa os eventos MQTT, armazena em TimescaleDB com particionamento automático por tempo, e expõe uma API WebSocket para o dashboard.
	O sistema de alertas detecta leituras fora de threshold e envia notificações. O projecto inclui OTA update simulation — como um sistema embarcado actualiza o firmware remotamente sem intervenção física.

**Core Features**
- Leituras em tempo real
- Alertas configuráveis
- Data logging (TimescaleDB)
- Gráficos históricos
- Automações (rules engine)
- Over-the-air (OTA) updates

**Requisitos**
- **Hardware simulado no Wokwi:**
	- DHT22 (temperatura + humidade)
	- PIR (movimento)
	- LDR (luminosidade)
	- OLED SSD1306 (display de status)
	- LED RGB (indicador de alertas)
- **Backend Node.js:**
	- MQTT broker (Mosquitto em Docker)
	- WebSocket gateway (tempo real para o frontend)
	- TimescaleDB (PostgreSQL com extensão time-series)
	- Alerting engine com regras configuráveis
- **Dashboard React:**
	- Gráficos em tempo real (Recharts)
	- Histórico com zoom
	- Gestão de alertas
	- OTA update simulation

**Entregáveis**

- [ ] Firmware + backend + dashboard no GitHub
- [ ] Link da simulação Wokwi partilhável (funciona no browser)
- [ ] Blog: "Building an IoT Data Pipeline with FreeRTOS and MQTT — No Hardware Needed"
- [ ] Video: demo da simulação completa a correr em tempo real