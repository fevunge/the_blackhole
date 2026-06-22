# Kubernetes — Platform Engineering
#week 

## Objectivos

- Kubernetes architecture: control plane, data plane, etcd
- Resources: Pods, Deployments, StatefulSets, DaemonSets
- Networking: Services, Ingress, Network Policies
- Storage: PVs, PVCs, StorageClasses
- Helm: charts, values, templates, hooks
- Operators: CRDs + Controller pattern

## Recursos

| Tipo    | Recurso                                                     |
| ------- | ----------------------------------------------------------- |
| Docs    | kubernetes.io/docs — documentação oficial                   |
| Course  | TechWorld with Nana — Kubernetes Full Course (YouTube)      |
| Prática | killer.sh — labs gratuitos para CKAD                        |
| Tool    | k3d — clusters K8s locais em Docker                         |
| Artigo  | Kubernetes Patterns — O'Reilly (versão gratuita no Red Hat) |

## Projeto
### Internal Developer Platform (Backstage-inspired)

**Tech Stack** 
	Go + Kubernetes API + Helm + React

**Overview**
	Um portal interno para developers gerirem os seus serviços, fazerem deploys, consultarem métricas e acederem a documentação — o tipo de plataforma que empresas como Spotify (que criou o Backstage) constroem para aumentar a produtividade das equipas de engenharia.
	O sistema usa um Kubernetes Operator com CRDs customizados (`Application` e `Environment`) para descrever declarativamente os serviços, e um webhook GitHub que dispara o pipeline de build e deploy automaticamente a cada push.
	O service catalog lista todos os serviços com owner, tecnologia, dependências, link para docs e status de saúde em tempo real.
	O metrics viewer integrado mostra CPU, memória, requests/segundo e error rate sem sair do portal.
	O dependency graph visualiza as dependências entre serviços para entender o impacto de mudanças.
	O sistema de RBAC garante que developers só vêem e actuam sobre os seus próprios serviços.
	A CLI companion (`idp` command) permite fazer tudo o que o portal faz mas via terminal, para developers que preferem não sair do terminal.

**Core Features**
- Service catalog: lista de todos os serviços com owner, docs, status
- One-click deploy: Git push → build → deploy via Kubernetes
- Metrics per service: CPU, memory, requests/s, error rate
- Logs viewer integrado (sem sair do portal)
- Secrets management UI
- Runbook viewer (markdown docs integrados)
- Dependency graph entre serviços
- CLI companion (`idp` command)

**Requisitos**
- Kubernetes Operator com CRDs (`Application`, `Environment`)
- Webhook para Git: push → build → deploy automático
- RBAC: developers só vêem os seus serviços
- Multi-namespace isolation

## Entregáveis

- [ ] Platform funcional em cluster local (k3d)
- [ ] Blog: "Building an Internal Developer Platform on Kubernetes"
- [ ] Video: Deploy workflow do git push ao serviço em produção
- [ ] Helm chart publicado no Artifact Hub
