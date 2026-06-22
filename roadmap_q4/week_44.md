# Advanced Ray Tracer + GPU Path Tracing (WebGPU)
#week 

### Real-time Path Tracer com WebGPU

**Tech Stack**
	Rust + `wgpu` (WebGPU) + WGSL shaders + React (UI)

**Overview**
	Vais evoluir o path tracer da [[week_23]] para correr na GPU via WebGPU — o que permite renders interactivos em tempo real em vez de esperar minutos por uma imagem. WebGPU é a escolha correcta em 2026 porque corre em qualquer GPU (NVIDIA, AMD, Intel, Apple Silicon) via browser, sem CUDA, sem drivers especiais, e o `wgpu` de Rust dá acesso type-safe cross-platform. O compute shader em WGSL executa o path tracing com cada thread a calcular um pixel independentemente: para cada frame, acumulas uma nova amostra por pixel e fazes blend com o acumulado anterior — progressive rendering que converge para uma imagem de alta qualidade enquanto a câmera não se move. O BVH é serializado para WebGPU storage buffers para acesso eficiente na GPU. Os materiais usam o Disney BSDF completo. O denoising temporal usa motion vectors para reutilizar amostras de frames anteriores quando a câmera se move, reduzindo o noise percebido. O scene editor React permite modificar objectos, materiais e luzes em tempo real e ver o resultado imediatamente. O projecto é publicado como web app — qualquer pessoa com Chrome ou Firefox moderno pode correr o teu path tracer.

**Features:**

- Path tracing completo na GPU (global illumination)
- Denoising temporal (acumula amostras ao longo de frames)
- PBR materials: Disney BSDF
- BVH na GPU (WebGPU storage buffers)
- Real-time preview (1 sample/pixel) + high quality mode (N samples)
- Scene editor React + export de renders

**Pipeline GPU:**

```wgsl
// Compute shader — cada thread é um pixel
@compute @workgroup_size(8, 8)
fn ray_trace(@builtin(global_invocation_id) id: vec3<u32>) {
    let ray = generate_ray(id.xy, camera);
    let color = path_trace(ray, scene, 8u);  // 8 bounces
    atomicAdd(&accumulated[id.xy], color);
}
```

## Entregáveis
- [ ] Ray tracer funcional no browser (testado em Chrome e Firefox)
- [ ] Gallery de renders de alta qualidade
- [ ] Blog: "Real-time Path Tracing in the Browser with WebGPU and Rust"
- [ ] Video: time-lapse de convergência de uma render
