# DevOps Platform — GitOps com ArgoCD
#week 

### GitOps CI/CD Platform Completa

**Tech Stack** 
	Kubernetes + Terraform + ArgoCD + Tekton (CI) + Vault

**Overview**
	Vais construir uma pipeline GitOps completa onde o Git é a única fonte de verdade para o estado da infraestrutura e das aplicações — qualquer mudança aprovada num PR é automaticamente aplicada ao cluster sem intervenção manual. O Terraform provisiona o cluster k3d local e configura os recursos necessários. O ArgoCD monitoriza o repositório de manifests e sincroniza automaticamente quando detecta divergência entre o estado desejado no Git e o estado actual do cluster — com rollback automático via health checks se um deployment quebra. O Tekton define pipelines como CRDs Kubernetes: um pipeline de CI corre testes, builda a imagem Docker, faz push para o registry, e actualiza o manifest de deployment no repo de infra (disparando o ArgoCD). O Vault em modo dev gere todos os secrets: zero secrets em YAML ou Git, os pods recebem secrets via Vault Agent Injector como ficheiros em memória. O Cert-Manager gere certificados TLS automaticamente.
	

**Core Features**
- **Terraform**: provisiona o cluster K8s local (k3d) e os recursos cloud necessários
- **ArgoCD**: GitOps — qualquer commit no repo de infra é aplicado automaticamente
- **Tekton**: CI/CD nativo em Kubernetes (pipelines como CRDs)
- **Vault**: secrets management (zero secrets em YAML/Git)
- **Cert-Manager**: TLS automático
- **External-DNS**: DNS automático para Ingresses

**Fluxo GitOps**

```
Dev → git push → GitHub Actions (CI: test + build + push image)
                      ↓
                 ArgoCD detecta nova imagem
                      ↓
                 Sync automático para K8s
                      ↓
                 Rollback automático se health checks falham
```

**Serviços deployados (projectos anteriores):**

- Auth Platform ([[week_7]])
- SaaS Platform ([[week_13]])
- AI Knowledge Base ([[week_38]])

## Entregáveis

- [ ] IaC repo completo (um `terraform apply` + ArgoCD sync → tudo a funcionar)
- [ ] Blog: "GitOps in 2026 — The Definitive Setup with ArgoCD and Tekton"
- [ ] Video: from `git push` to production em tempo real
- [ ] Runbooks completos para operações comuns
