# Technical Writing & Documentation Master
#s_week  

## Objectivo

Elevar todos os 40+ repositórios ao nível de documentação de projectos open-source profissionais que as pessoas realmente queiram usar.
## Documentation Overhaul

**Para cada projecto no GitHub:**

- README: reescreve com estrutura clara (o que é, como instalar, como usar, arquitectura, contribuir)
- ADRs (Architecture Decision Records): mínimo 3 por projecto complexo
- OpenAPI/Swagger: todos os endpoints documentados com exemplos
- Changelog: `CHANGELOG.md` com semantic versioning
- Contributing guide: `CONTRIBUTING.md`
- Runbooks: para projectos com infra

**Templates criados (publicar no GitHub como template repo):**

- Project README template
- ADR template (MADR format)
- Pull Request template
- Issue template (bug report + feature request)
- Runbook template

### Content Creation desta semana

- 4-5 blog posts técnicos (retrospectiva dos projectos mais interessantes)
- Tutorial series para o projecto mais popular
- Comparação técnica (ex: "Go vs Rust for HTTP servers — Benchmarks and Trade-offs")

## Entregáveis

- [ ] Todos os 40+ repositórios com documentação de qualidade
- [ ] Template repo público
- [ ] Blog: "Documentation as a Competitive Advantage in Open Source"
- [ ] Video: walkthrough do processo de documentação

---
# **_Bônus_ [13]**

## Arquitectura Emergente & Casos de Estudo Avançados

**Objectivo**
	Aprender com os melhores casos reais da indústria.

### Recursos Obrigatórios

| Tipo        | Recurso                                                                                                   |
| ----------- | --------------------------------------------------------------------------------------------------------- |
| Livro       | _Software Architecture: The Hard Parts_ — Neal Ford, Mark Richards et al. (livro mais recente e avançado) |
| Conferência | [GOTO Conferences — YouTube](https://www.youtube.com/@GOTOConferences) — selecciona talks de arquitectura |
| Conferência | [QCon (InfoQ) — Architecture Tracks (infoq.com)](https://www.infoq.com/presentations/)                    |
| Papers      | Papers do Google: MapReduce, Bigtable, Spanner (todos disponíveis em research.google.com)                 |
| Site        | [The Morning Paper — adriancolyer.org](https://blog.acolyer.org/) — reviews de papers académicos          |

### PROJECTO: _"Architectural Kata"_

**Overview** 
	Resolve um "Architectural Kata" — exercício de arquitectura criado por Ted Neward (kata.softwarearchitect.it ou GitHub). Escolhe um dos katas disponíveis publicamente e entrega solução completa. O kata deve ser resolvido como se fosses apresentar a um cliente real.

**Entrega** 
	Documento LaTeX completo + todos os diagramas C4 + ADRs