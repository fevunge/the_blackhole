# Portfolio Website & Personal Brand
#week 

## Objectivo

Portfolio profissional que se destaca entre 1000 candidatos.

### Portfolio Website

**Tech Stack:** Next.js 15 + TypeScript + Tailwind CSS + MDX + Framer Motion

**Overview**
	Vais construir o portfolio que te representa como engineer e que convence um hiring manager em 2 minutos que és alguém que constrói coisas reais. A diferença entre um portfolio mediano e um excelente não é o design — é os case studies: cada projecto não tem apenas screenshots e um link GitHub, mas um documento estruturado que explica o problema que resolveste, as decisões técnicas que tomaste e porquê, os desafios que encontraste e como os superaste, e os resultados mensuráveis. O site é construído com Next.js 15 com full SSG para performance máxima, blog integrado via MDX local ou DEV.to API, e um mapa visual interactivo das skills em vez de uma lista estática. O Lighthouse tem de ser 100/100 em todas as categorias — é um sinal de qualidade e atenção ao detalhe. O dark/light mode com transição suave, command palette (⌘K) para navegação, e reading time estimado em cada post são os detalhes que mostram que te preocupas com a experiência do utilizador.

**Sections:**
- **Hero:** headline forte + CTA claro + animação subtil
- **About:** a tua história em 3 parágrafos — o porquê, o percurso, o agora
- **Projects:** 10-15 melhores com case studies individuais
- **Blog:** integrado via DEV.to API ou MDX local
- **Skills:** mapa visual interactivo (não uma lista chata)
- **Timeline:** o teu percurso de aprendizagem
- **Contact:** formulário + links

**Performance targets:**
- Lighthouse: 100/100/100/100 (Performance/Accessibility/Best Practices/SEO)
- LCP < 1.2s
- CLS = 0
- Funciona sem JavaScript (SSG + SSR)

**Case Studies (top 5 projectos):**

```markdown
## [Nome do Projecto]
Problema → Solução → Decisões Técnicas → Desafios → Métricas → Learnings
```

- Dark/Light mode com transição suave
- Command palette (⌘K) para navegação rápida
- Blog com table of contents + tempo de leitura
- Analytics: Plausible (privacy-first, gratuito self-hosted)

### Personal Branding Completo

**LinkedIn:**
- Headline: `[Role] | [Specialization] | Building [X]`
- About: hook forte + percurso + expertise + CTA
- Featured: top 3 projectos com screenshots
- Skills: 50+ endorsements nos skills core
- Recomendações: pede a 3-5 pessoas da comunidade

**GitHub Profile README:**
- Stats dinâmicos (GitHub Actions atualiza automaticamente)
- "Currently building" — actualiza semanalmente
- Lista dos 5 melhores projectos com 1 linha cada
- Contribution graph activo há 365 dias

## Entregáveis

- [ ] Portfolio live com domínio próprio (Cloudflare Pages — gratuito)
- [ ] 5+ case studies completos e detalhados
- [ ] LinkedIn totalmente optimizado
- [ ] GitHub profile polished
- [ ] Blog: "How to Build a Developer Portfolio That Gets Interviews"
