
---
marp: true
theme: default
paginate: true
---

<!-- _class: invert -->
# Aprendizaje Profundo
## Capítulo 22

---

# Esquema

- Redes de Alimentación Directa Simples
- Grafos de Cómputo para Aprendizaje Profundo
- Redes Convolucionales
- Algoritmos de Aprendizaje
- Generalización
- Redes Neuronales Recurrentes
- Aprendizaje No Supervisado y Aprendizaje por Transferencia
- Aplicaciones

---

# Redes de Alimentación Directa Simples

![bg right:40% 80%](https://miro.medium.com/max/1400/1*3fA77_mLNiJTSgZFhYnU0Q.png)

- Red de alimentación directa
  - Conexiones solo en una dirección (entrada a salida)
  - Grafo acíclico dirigido con nodos de entrada y salida designados
  - Sin bucles

- Red recurrente
  - Salidas intermedias o finales vuelven a sus propias entradas
  - Los valores de señal forman un sistema dinámico con estado interno o memoria

---

# Redes como Funciones Complejas

- Cada nodo se llama unidad
- Calcula suma ponderada de entradas de nodos predecesores
- Aplica función no lineal para producir salida

$$a_j = g_j(\sum_i w_{i,j} a_i)$$

Donde:
- $g_j$ es una función de activación no lineal
- $a_j$ denota la salida de la unidad j
- $w_{i,j}$ es el peso de la unidad i a la unidad j

---

<!-- _class: invert -->
# Estructura de una Red Neuronal

![width:900px](https://www.researchgate.net/publication/337194658/figure/fig1/AS:824905820966912@1573673169646/A-simple-artificial-neural-network-a-and-an-example-of-a-deep-neural-network-b.png)

---

# Grafos de Cómputo para Aprendizaje Profundo

## Codificación de Entrada

- Los nodos de entrada y salida se conectan directamente a los datos de entrada x y datos de salida y
- Valores booleanos: Falso → 0, Verdadero → 1 (o -1 y +1)
- Atributos numéricos usados tal cual
- Atributos categóricos con codificación one-hot
  - Atributo con d valores representado por d bits de entrada separados
  - Bit de entrada correspondiente se establece en 1, los demás en 0

---

# Capas Ocultas

- Cálculos intermedios antes de producir la salida y
- Diferente representación para la entrada x
- Cada capa transforma la representación de la capa precedente
- Las redes profundas a menudo descubren representaciones intermedias significativas
- Las capas ocultas suelen ser menos diversas que las capas de salida

---

# Redes Convolucionales

![bg right:40% 80%](https://miro.medium.com/max/1400/1*vkQ0hXDaQv57sALXAJquxA.jpeg)

- La Red Neuronal Convolucional (CNN) contiene conexiones espacialmente locales
- Kernel: Patrón de pesos replicado en múltiples regiones locales
- Convolución: Proceso de aplicar el kernel a los píxeles de la imagen

---

# Operación de Convolución

- Vector de entrada x de tamaño n (n píxeles en imagen 1D)
- Kernel vectorial k de tamaño l
- Operación de convolución: z = x * k
- Paso s: Distancia entre centros de kernel
- Relleno: Píxeles extra agregados para aplicar el kernel [n/s] veces

---

# Estructura de CNN

![width:900px](https://miro.medium.com/max/1400/1*ZCjPUFrB6eHPRi4eyP6aaA.gif)

---

# Agrupación y Submuestreo

- La capa de agrupación resume unidades adyacentes de la capa precedente
- Formas comunes:
  1. Agrupación promedio: Calcula el valor promedio de l entradas
  2. Agrupación máxima: Calcula el valor máximo de l entradas

- Beneficios:
  - Reduce la resolución de la imagen
  - Facilita el reconocimiento multiescala
  - Disyunción lógica (agrupación máxima)

---

# Operaciones con Tensores en CNNs

- Tensores: Arreglos multidimensionales de cualquier dimensión
- Vectores y matrices son casos especiales (1D y 2D)
- Mantener el seguimiento de la "forma" de los datos a través de las capas de la red
- Eficiencia computacional:
  - Código compilado optimizado para el sustrato computacional subyacente
  - A menudo se ejecuta en GPUs o TPUs para alto paralelismo

---

# Redes Residuales

![bg right:40% 80%](https://miro.medium.com/max/1400/1*D0F3UitQ2l5Q0Ak-tjEdJg.png)

- Evita el problema de desvanecimiento de gradientes
- Idea clave: La capa perturba la representación de la capa anterior
- Fórmula: $z^{(i)} = g^{(i)}(z^{(i-1)} + f(z^{(i-1)}))$
  - $z^{(i)}$: valores de las unidades en la capa i
  - $g^{(i)}$: funciones de activación para la capa residual
  - $f$: residual, perturbando el comportamiento predeterminado

---

# Algoritmos de Aprendizaje

## Cálculo de Gradientes en Grafos de Cómputo

- El gradiente de la función de pérdida se calcula retropropagando el error
- La retropropagación pasa mensajes a lo largo de los enlaces de la red
- Los mensajes son derivadas parciales de la pérdida L
- El compartir pesos se maneja como un único nodo con múltiples arcos salientes
- El gradiente para un peso compartido es la suma de las contribuciones de cada uso

---

# Generalización

## Elección de una Arquitectura de Red

- Algunas arquitecturas están diseñadas para generalizar bien en tipos de datos específicos
- Las redes más profundas suelen dar mejor rendimiento de generalización
- El aprendizaje profundo sobresale en entradas de alta dimensión (imágenes, video, habla)
- Limitaciones:
  - Falta de poder expresivo composicional y cuantificacional
  - Puede producir errores poco intuitivos y mapeos discontinuos

---

# Búsqueda de Arquitectura Neuronal

- Explora el espacio de estado de posibles arquitecturas de red
- Métodos:
  1. Algoritmos evolutivos (recombinación, mutación)
  2. Ascenso de colinas con operaciones de mutación
- Desafíos:
  - Estimar el valor de la red candidata
  - Entrenar una red grande, buscar subgrafos con mejor rendimiento
  - Usar funciones de evaluación heurísticas

---

# Dropout

![bg right:40% 80%](https://miro.medium.com/max/1400/1*iWQzxhVlvadk6VAJjsgXgg.png)

- Reduce el error en el conjunto de prueba a costa de un ajuste más difícil en el conjunto de entrenamiento
- Introduce ruido en el tiempo de entrenamiento para robustez
- Aproxima la creación de un gran conjunto de redes adelgazadas
- Fuerza al modelo a aprender múltiples explicaciones robustas para cada entrada

---

# Redes Neuronales Recurrentes (RNNs)

- Permiten ciclos en el grafo de cómputo (con retraso)
- Las unidades pueden tomar entrada de su propia salida anterior
- La RNN tiene estado/memoria interna
- Agrega poder expresivo en comparación con redes de alimentación directa

---

# RNNs de Memoria a Corto y Largo Plazo (LSTM)

![bg right:40% 80%](https://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-chain.png)

- Tiene componente de memoria a largo plazo (celda de memoria)
- Unidades de compuerta controlan el flujo de información:
  1. Compuerta de olvido
  2. Compuerta de entrada
  3. Compuerta de salida
- Las compuertas tienen rango [0,1] y son salidas de una función sigmoide

---

# Aprendizaje No Supervisado y Aprendizaje por Transferencia

## Aprendizaje No Supervisado

- Toma ejemplos no etiquetados x para:
  1. Aprender nuevas representaciones
  2. Aprender un modelo generativo

## PCA Probabilístico (PPCA)

- Modelo generativo simple
- z elegido de una distribución gaussiana esférica de media cero
- x generado de z aplicando matriz de pesos W y agregando ruido gaussiano

---

# Redes Generativas Adversarias (GANs)

![bg right:40% 80%](https://miro.medium.com/max/1400/1*-gFsbymY9oJUQJ-A3GTfeg.png)

- Par de redes formando un sistema generativo:
  1. Generador: Mapea valores de z a x
  2. Discriminador: Clasifica entradas x como reales o falsas
- Modelo implícito: Muestras generadas, pero probabilidades no disponibles fácilmente
- Entrenadas simultáneamente
- Sobresale en tareas de generación de imágenes

---

# Aprendizaje por Transferencia y Aprendizaje Multitarea

- Aprendizaje por transferencia: La experiencia con una tarea ayuda a aprender otra
- Enfoque común:
  1. Congelar las primeras capas del modelo preentrenado
  2. Modificar solo los parámetros de los niveles superiores
- Ajuste fino:
  1. Ejemplos de vocabulario especializado
  2. Entrenamiento en tarea específica
- Aprendizaje multitarea: Entrenar simultáneamente el modelo en múltiples objetivos

---

# Aplicaciones

1. Visión
   - Éxito de AlexNet en la competición ImageNet 2012
   - Aprendizaje supervisado con 1.200.000 imágenes en 1.000 categorías
   - Tasa de error top-5 reducida a <2% (por debajo de la tasa de error humana)

2. Procesamiento del Lenguaje Natural
   - Traducción automática y reconocimiento de voz
   - Aprendizaje de extremo a extremo, generación automática de representaciones de palabras
   - Incrustaciones de palabras: Re-representación de palabras como vectores en espacio de alta dimensión

3. Aprendizaje por Refuerzo
   - El agente aprende de una secuencia de señales de recompensa
   - Optimiza la suma de recompensas futuras
   - Aprende función de valor, función Q, política, etc.

---

<!-- _class: invert -->
# Resumen

- Las redes neuronales representan funciones no lineales complejas con unidades de umbral lineal parametrizadas
- La retropropagación implementa el descenso de gradiente en el espacio de parámetros para minimizar la función de pérdida
- Las redes convolucionales son adecuadas para el procesamiento de imágenes y datos con topología de cuadrícula
- Las redes recurrentes son efectivas para tareas de procesamiento de secuencias (modelado de lenguaje, traducción automática)

```

## Notas sobre la traducción

1. "Deep Learning" se tradujo como "Aprendizaje Profundo", que es el término más comúnmente usado en Argentina y otros países hispanohablantes.
2. Se mantuvo el término "kernel" sin traducir, ya que es ampliamente utilizado en español en el contexto de redes neuronales.
3. "Dropout" se mantuvo en inglés, ya que es un término técnico específico que no suele traducirse.
4. "Long Short-Term Memory (LSTM)" se tradujo como "Memoria a Corto y Largo Plazo (LSTM)", manteniendo la sigla en inglés.
5. Se utilizó "vos" implícito en algunas explicaciones, aunque no fue necesario hacer uso explícito del pronombre debido al carácter formal y técnico del texto.

## Aspectos desafiantes de la traducción

1. La traducción de términos técnicos específicos del aprendizaje profundo requirió un equilibrio entre la precisión técnica y la comprensión en español. Por ejemplo, "feedforward" se tradujo como "alimentación directa", que es el término más común en español, aunque no es una traducción literal.

2. Mantener la coherencia en la terminología a lo largo de todo el texto fue crucial, especialmente con términos que tienen múltiples posibles traducciones.

3. La adaptación de las explicaciones matemáticas y fórmulas requirió atención para asegurar que la notación y la terminología fueran consistentes con las convenciones en español.

4. La traducción de los conceptos relacionados con las redes neuronales y sus componentes (como "gating units" traducido como "unidades de compuerta") requirió un conocimiento profundo del tema para asegurar la precisión técnica.

5. Mantener el formato y la estructura del documento original en Markdown, incluyendo las imágenes y los estilos de presentación, fue un aspecto importante para preservar la integridad del contenido y su presentación visual.

```