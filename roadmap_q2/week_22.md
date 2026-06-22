# Computação Gráfica — OpenGL + Shaders Modernos
#week 

## Objectivos
- OpenGL pipeline: VAO, VBO, EBO, shaders, framebuffers
- GLSL: vertex shader, fragment shader, uniforms, varyings
- Transformações: Model, View, Projection matrices (MVP)
- Lighting: Phong shading, normal mapping, shadow mapping
- MVP matrices: Model, View, Projection — a matemática que move objectos 3D
- Physically Based Rendering: Cook-Torrance BRDF, metallic/roughness workflow
- IBL (Image-Based Lighting): environment maps para reflexos realistas

## Recursos

| Tipo  | Recurso                                                               |
| ----- | --------------------------------------------------------------------- |
| Site  | learnopengl.com — o melhor tutorial de OpenGL, completamente gratuito |
| Livro | _Real-Time Rendering_ (4ª edição) — Akenine-Möller et al.             |
| Tool  | RenderDoc — frame debugger gratuito                                   |
| Site  | shadertoy.com — experimentos com GLSL                                 |
| Video | The Cherno — OpenGL series (YouTube)                                  |

## Projeto
### PBR 3D Model Viewer

**Tech Stack**
	C++20 + OpenGL 4.6 + GLFW + GLM + Dear ImGui + stb_image

**Overview** 
	Um visualizador de modelos 3D com Physically Based Rendering — o pipeline de rendering que todos os jogos modernos e ferramentas de visualização 3D usam. O viewer importa modelos no formato glTF 2.0 (o formato standard moderno que substituiu OBJ) incluindo os seus materiais PBR (albedo, metallic, roughness, occlusion, normal maps, emissive), e renderiza-os com um fragment shader Cook-Torrance completo com Fresnel, GGX distribution e Smith geometry masking. O Image-Based Lighting usa HDR environment maps para iluminação indirecta realista — specular via cubemap pré-filtrado e difuse via irradiance map pré-calculado — o que dá aos materiais metálicos aquele reflexo environment característico dos renders de qualidade. Shadow mapping com PCF elimina o aliasing das sombras duras. O Dear ImGui panel permite ajustar os parâmetros de material em tempo real (metallic, roughness, albedo), fazer switch de environment maps, e visualizar os diferentes channels dos materiais (normal, metallic, roughness separados). O projecto termina com uma galeria de renders antes/depois de activar PBR para mostrar a diferença.

**Core Features**
- Import de modelos glTF 2.0 (formato padrão moderno — substitui OBJ)
- PBR materials: albedo, metallic, roughness, AO, normal maps
- IBL (Image-Based Lighting): HDR environment maps para reflexos realistas
- Multiple light types: directional, point, spot
- Shadow mapping com PCF (Percentage Closer Filtering)
- Camera: orbit, pan, zoom com damping suave
- Wireframe, normals, tangent space visualization
- Dear ImGui panel para ajustar materiais em tempo real
- Export de screenshots

**Requisitos**

```glsl
// PBR fragment shader core
vec3 Lo = vec3(0.0);
for(int i = 0; i < NUM_LIGHTS; ++i) {
    // Cook-Torrance BRDF
    vec3 F = fresnelSchlick(max(dot(H, V), 0.0), F0);
    float NDF = DistributionGGX(N, H, roughness);
    float G = GeometrySmith(N, V, L, roughness);
    // ...
}
```

## Entregáveis

- [ ] Desktop app compilada (CMake) com modelos de exemplo
- [ ] Blog: "Implementing PBR Shading from Scratch — The Math Behind Modern Game Graphics"
- [ ] Video: Antes/depois com PBR activo
- [ ] Shader collection no GitHub (comentados e educativos)
