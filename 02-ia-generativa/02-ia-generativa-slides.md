---
marp: true
theme: gaia
paginate: true
---

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true });
</script>

# Unidad 1 - Clase 02 - IA generativa

---

## 1. Introducción a herramientas de IA generativa

- IA generativa: técnicas y modelos capaces de crear contenido nuevo y original
- Democratiza la IA: uso mediante indicaciones en lenguaje natural
- Aplicaciones: escribir informes, crear aplicaciones, etc.
- En desarrollo desde los años 60
- Ejemplos: OpenAI ChatGPT, Anthropic Claude, Google Gemini

---

![bg contain](./img/ai-diagram.png)

---

## 1.1 Fundamentos de la IA generativa

- Basada en aprendizaje no supervisado
- Utiliza redes neuronales complejas
- Grandes modelos de lenguaje generan texto autocompletando

---

![bg contain](./img/cerebro-red-neuronal.png)

---

## Proceso de inferencia en modelos de lenguaje natural

![image](./img/llm-inference.png)

---

## Evolución del tamaño de los modelos

![image](./img/llm-parameter-numbers.png)

---

## Costos de entrenamiento de modelos

![image](./img/training-costs.png)

---

## 1.2 Tipos de modelos generativos

Los modelos generativos se pueden dividir entre los siguientes tipos:

<div class="mermaid">
graph TD
    A[-Modelos Generativos-----] --> B[GANs]
    A --> C[Modelos Autoregresivos]
    A --> D[-VAEs--]
    A --> E[Modelos de Difusión]
    B --> F[Generador]
    B --> G[Discriminador]
    C --> H[GPT]
    D --> I[Encoder]
    D --> J[Decoder]
<div>

---

## 1.3 Aplicaciones de la IA generativa

<div class="mermaid">
mindmap
  root((IA Generativa))
    Texto
      Artículos
      Poesía
      Guiones
      Código
    Imágenes
      Ilustraciones
      Fotografías
      Arte conceptual
    Audio
      Voces artificiales
      Composición musical
    Diseño
      Logos
      Productos
      Arquitectura
    Ciencia
      Diseño de moléculas
      Simulaciones
<div>

---

## Tipos de LLMs por tarea

<div class="mermaid">
graph LR
    A[Tipos de LLMs---] --> B[Audio y Voz---]
    A --> C[Imágenes--]
    A --> D[Texto-]
    A --> E[Multi-modal--]
    B --> F[Whisper]
    C --> G[DALL-E]
    C --> H[Midjourney]
    D --> I[GPT-3.5]
    D --> J[GPT-4]
    E --> K[GPT-4 Turbo con visión]
<div>


---

## Modelos de base vs LLMs

![image](./img/FoundationModel.png)

---

## Modelos multi-modales

![image](./img/Multimodal.png)

---

## Código abierto vs Propietarios

<div class="mermaid">
classDiagram
    class LLMs {
        +Código Abierto
        +Propietarios
    }
    class CódigoAbierto {
        +Disponibles públicamente
        +Personalizables
        +Ejemplos: Alpaca, Bloom, LLaMA
    }
    class Propietarios {
        +Propiedad de empresas
        +Optimizados para producción
        +Ejemplos: OpenAI, Google Bard, Claude 2
    }
    LLMs --> CódigoAbierto
    LLMs --> Propietarios
<div>

---

## Embeddings

![image](./img/Embedding.png)

---

## Generación de imágenes

![image](./img/Image.png)

---

## Generación de texto y código

![image](./img/Text.png)

---

## Arquitecturas de LLMs

<div class="mermaid">
graph TD
    A[Arquitecturas de LLMs] --> B[Solo Decoder]
    A --> C[Solo Encoder]
    A --> D[Encoder-Decoder]
    B --> E[GPT]
    C --> F[BERT]
    D --> G[BART]
    D --> H[T5]
    B --> I[Bueno generando contenido]
    C --> J[Bueno entendiendo contexto]
    D --> K[Combina generación y comprensión]
<div>

---

## Servicio vs Modelo

<div class="mermaid">
graph TD
    A[LLMs] --> B[Servicio]
    A --> C[Modelo]
    B --> D[Proveedor de 
    Servicios en la Nube-----]
    B --> E[Optimizado para producción]
    B --> F[Ejemplo: Azure OpenAI Service]
    C --> G[Componente central Red Neuronal]
    C --> H[Puede requerir infraestructura propia]
    C --> I[Ejemplo: LLaMA]
<div>

---

# Ingeniería de prompts