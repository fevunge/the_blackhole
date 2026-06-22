# Ray Tracing — Path Tracer Fisicamente Baseado
#week 

## Objectivos

- Ray-object intersection: raios vs esferas, planos, triângulos, AABBs
- BVH (Bounding Volume Hierarchy): construção com SAH e traversal eficiente
- Path tracing: Monte Carlo integration, importance sampling, Russian Roulette
- Materials físicos: diffuse Lambertian, specular GGX, dielectric (vidro), emissive
- Multi-threading com work-stealing para paralelismo eficiente
## Recursos

| Tipo  | Recurso                                                                         |
| ----- | ------------------------------------------------------------------------------- |
| Livro | _Ray Tracing in One Weekend_ — Peter Shirley (gratuito em raytracing.github.io) |
| Livro | _Ray Tracing: The Next Week_ + _The Rest of Your Life_ — mesma série, gratuita  |
| Paper | "Physically Based Rendering: From Theory to Implementation" — Pharr, Jakob      |
| Site  | scratchapixel.com — teoria de CG mais aprofundada                               |
| Video | "Writing a Ray Tracer" — The Cherno (YouTube)                                   |

## Projeto
### Path Tracer em C++20 com BVH e Multi-threading

**Tech Stack**
	C++20 + `std::thread` + `std::atomic` + `stb_image_write`

**Overview**
	Um path tracer fisicamente baseado capaz de produzir renders com global illumination, caustics, subsurface scattering, e materiais PBR realistas, usando apenas a CPU com multi-threading eficiente. O motor de rendering usa um BVH construído com SAH (Surface Area Heuristic) para minimizar o custo de traversal, intersection tests com primitivas como esferas, planos e triangle meshes carregadas de ficheiros OBJ, e um path tracer com Monte Carlo integration onde cada raio bounce amostra materiais via BRDF importance sampling — Lambertian para diffuse, GGX microfacet para specular, Fresnel-Schlick para reflexão/refracção no vidro. O Russian Roulette termina paths com probabilidade proporcional à sua contribuição esperada, evitando bias. O sistema de multi-threading divide a imagem em tiles e usa um `std::atomic` counter como work queue — cada thread pega o próximo tile disponível, sem lock contention. O progressive rendering mostra a imagem a melhorar em tempo real enquanto acumulas amostras. O projecto termina com o Cornell Box clássico (validação matemática), uma cena com vidro e metais, e benchmarks de speedup linear de 1 a N threads.

**Core Features**
- Primitivas: sphere, plane, triangle mesh (OBJ loader)
- BVH acceleration: SAH (Surface Area Heuristic) para construção óptima
- Materials: Lambertian diffuse, Metallic (GGX microfacet), Dielectric, Emissive
- Light sources: area lights, environment map (HDRI)
- Path tracing com Russian Roulette para terminação
- Importance sampling de lights e BRDF
- Anti-aliasing por supersampling (N amostras por pixel)
- Progressive rendering: mostra imagem a melhorar em tempo real
- Multi-threading: tile-based com work queue (`std::atomic` counter)
- Scene format: JSON legível

**Requisitos**
- Cornell Box clássico (validação do algoritmo)
- Cena com vidro, metais e luzes coloridas
- Comparação: 1 thread vs N threads (speedup linear?)

## Entregáveis

- [ ] Renders de alta qualidade no README
- [ ] Blog: "Implementing a Path Tracer — Monte Carlo Integration Explained Visually"
- [ ] Video: Time-lapse de uma render de alta qualidade a convergir
- [ ] Benchmark: speedup de 1 a 8 threads (gráfico)
- [ ] Gallery de renders no GitHub Pages
