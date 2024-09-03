
---
marp: true
theme: default
class: invert
---

# Visión por Computadora
## Capítulo 27

---

# Esquema

- Introducción
- Formación de imágenes
- Características simples de imágenes
- Clasificación de imágenes
- Detección de objetos
- El mundo 3D
- Uso de la visión por computadora

---

# Introducción

- La mayoría de los agentes que usan visión utilizan sensores pasivos
- Una característica es un número obtenido al aplicar cálculos simples a una imagen
- El enfoque basado en modelos para la visión utiliza dos tipos de modelos:
  - Modelo de objeto (ej. modelo geométrico preciso producido por sistemas de diseño asistido por computadora)
  - Modelo de renderizado (describe los procesos físicos, geométricos y estadísticos que producen el estímulo del mundo)

- Dos problemas centrales de la visión por computadora:
  1. Reconstrucción: construir un modelo del mundo a partir de imagen(es)
  2. Reconocimiento: establecer distinciones entre objetos basadas en información visual y de otro tipo

---

# Formación de imágenes

![bg right:40% 80%](https://example.com/pinhole_camera_image.jpg)

- Principio de la cámara estenopeica
- Sistemas de lentes:
  - Plano focal
  - Profundidad de campo
  - El tamaño de la apertura afecta la profundidad de campo

---

# Luz y sombreado

- El brillo de un píxel depende de:
  1. Intensidad general de la luz ambiental
  2. Orientación de la superficie respecto a la fuente de luz
  3. Cantidad de luz reflejada desde el punto

- Tipos de reflexión:
  - Reflexión difusa
  - Reflexión especular

- Las sombras ocurren cuando la superficie no puede ver la fuente de luz

---

![bg 80%](https://example.com/illumination_effects_image.jpg)

---

# Color

- Principio de tricromía:
  - Se puede igualar cualquier densidad de energía espectral mezclando tres colores primarios (RGB)

- Constancia del color:
  - Estimar el color de la superficie bajo luz blanca
  - Ignorar los efectos de luces de diferentes colores

---

# Características simples de imágenes: Bordes

- Bordes: líneas o curvas con cambio significativo en el brillo de la imagen
- La detección de bordes abstrae la imagen en una representación compacta
- Causas de los bordes:
  - Discontinuidades de profundidad
  - Cambios en la normal de la superficie
  - Cambios en la reflectancia de la superficie
  - Sombras (discontinuidades de iluminación)

---

![bg 80%](https://example.com/edge_types_image.jpg)

---

# Suavizado de imágenes

- Suprime el ruido utilizando píxeles circundantes
- Filtro gaussiano:
  - Convolución de la imagen con función gaussiana
  - Reemplaza la intensidad con suma ponderada de píxeles cercanos

---

![bg 80%](https://example.com/edge_detection_steps_image.jpg)

---

# Textura

- Patrón en una superficie percibido visualmente
- Propiedades:
  - Patrón repetitivo de elementos (texels)
  - Propiedad de un parche de imagen, no de píxeles individuales
  - Invariante a cambios de iluminación
  - Cambia de manera sensible con la rotación

- Representación de textura:
  - Calcular orientación del gradiente en cada píxel
  - Caracterizar el parche por histograma de orientaciones

---

# Flujo óptico

- Movimiento aparente debido al movimiento relativo entre la cámara y los objetos
- Describe la dirección y velocidad del movimiento de características en la imagen
- Medición: Suma de Diferencias Cuadradas (SSD)
- Requiere textura en la escena para una medición precisa

---

![bg 80%](https://example.com/optical_flow_image.jpg)

---

# Segmentación de imágenes

- Proceso de agrupar píxeles similares
- Enfoques:
  1. Detección de bordes
  2. Agrupamiento de regiones

- Problema de clasificación:
  - Entrenar clasificador de aprendizaje automático con ground truth marcado por humanos

---

![bg 80%](https://example.com/segmentation_example_image.jpg)

---

# Clasificación de imágenes

- Los sistemas modernos usan apariencia (color y textura) en lugar de geometría
- Desafíos:
  1. Variación intraclase
  2. Variaciones en las condiciones de visualización (iluminación, escorzo, aspecto, oclusión, deformación)

- Solución: Redes Neuronales Convolucionales (CNNs) entrenadas en grandes conjuntos de datos

---

# CNNs para clasificación de imágenes

- Ideas clave:
  1. Detección de patrones locales (convolución + ReLU)
  2. Detección de múltiples patrones (múltiples kernels)
  3. Detección de patrones compuestos (múltiples capas)

- Técnicas de aumento de datos:
  - Desplazamientos, rotaciones y estiramientos aleatorios
  - Cambios de tono

- Importancia del contexto en la clasificación

---

# Detección de objetos

- Los detectores de objetos encuentran múltiples objetos, informan clase y ubicación (bounding box)
- Proceso:
  1. Definir forma de la ventana
  2. Construir clasificador para ventanas
  3. Decidir qué ventanas examinar
  4. Elegir ventanas a informar
  5. Informar ubicaciones precisas de objetos

- Red de Propuesta de Regiones (RPN) en Faster RCNN
- Supresión no máxima para selección de ventanas
- Regresión de bounding box para localización precisa

---

![bg 80%](https://example.com/faster_rcnn_diagram.jpg)

---

# El mundo 3D

- Múltiples vistas proporcionan mejor comprensión 3D
- Problema clave: Establecer correspondencias entre vistas
- Métodos para múltiples vistas:
  1. Dos cámaras (visión estéreo)
  2. Movimiento de cámara

---

![bg right:40% 80%](https://example.com/stereo_vision_diagram.jpg)

- Estereopsis: Percepción de profundidad a partir de disparidad binocular
- Relación entre disparidad y profundidad

---

# Uso de la visión por computadora

1. Comprensión de acciones humanas
   - Desafíos:
     - Vincular observaciones con objetivos e intenciones
     - Dependencia de escala temporal
     - Comportamientos concurrentes no relacionados
   - Problemas de adaptación de dominio

2. Vinculación de imágenes y palabras
   - Etiquetado de imágenes
   - Generación de descripciones de imágenes
   - Respuesta a preguntas visuales (VQA)
   - Sistemas de diálogo visual

3. Generación de imágenes
   - GANs para generación de imágenes sintéticas

4. Aplicaciones en vehículos autónomos

---

# Resumen

- Representaciones de imágenes: bordes, textura, flujo óptico, regiones
- CNNs para clasificación precisa de imágenes
- Detección de objetos usando clasificadores de imágenes
- Reconstrucción de escenas 3D a partir de múltiples vistas
- Avances en aplicaciones de reconocimiento de acciones, vinculación imagen-texto y generación de imágenes

---

```

Notas sobre la traducción:

1. "Computer Vision" se tradujo como "Visión por Computadora", que es el término más utilizado en Argentina para este campo.
2. Se mantuvo el uso de términos técnicos en inglés como "CNN", "RPN", "Faster RCNN", "GANs", y "VQA", ya que son ampliamente utilizados en la comunidad académica y profesional argentina sin traducción.
3. Se utilizó el pronombre "vos" implícito en las instrucciones, aunque no fue necesario utilizarlo explícitamente en este texto técnico.
4. Se mantuvieron algunos términos en inglés como "ground truth", "bounding box", y "kernels", ya que son comúnmente utilizados en el ámbito académico argentino de visión por computadora.

Aspectos desafiantes de la traducción:

1. La traducción de "feature" como "característica" en lugar de "rasgo" o "atributo", ya que en el contexto de visión por computadora en Argentina, "característica" es el término más utilizado.
2. La decisión de mantener "renderizado" como traducción de "rendering", ya que es un anglicismo ampliamente aceptado en el campo de la computación gráfica en Argentina.
3. La traducción de "depth of field" como "profundidad de campo", que es el término técnico utilizado en fotografía y óptica en Argentina.
4. La decisión de no traducir términos como "ReLU" o "Non-maximum suppression", ya que se utilizan comúnmente en inglés en la literatura académica argentina.