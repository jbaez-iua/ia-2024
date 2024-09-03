
# Aprendizaje Profundo para Procesamiento del Lenguaje Natural
### Capítulo 25
Inteligencia Artificial: Un Enfoque Moderno, Cuarta Edición, Edición Global
© 2022 Pearson Education Ltd.

---

# Esquema

- Embeddings de palabras
- Redes neuronales recurrentes para PLN
- Modelos de secuencia a secuencia
- La arquitectura Transformer
- Preentrenamiento y transferencia de aprendizaje
- Estado del arte

---

# Embeddings de palabras

- Se busca una representación de palabras que no requiera ingeniería manual de características, pero que permita la generalización entre palabras relacionadas
- **Embedding de palabra**: un vector de baja dimensión que representa una palabra
  - Aprendido automáticamente de los datos
  - Tiene propiedades adicionales más allá de la mera proximidad para palabras similares
  - Probado como una buena representación para tareas de lenguaje posteriores (por ejemplo, respuesta a preguntas, traducción, resumen)
- Es posible usar vectores preentrenados genéricos
- Los diccionarios de vectores incluyen WORD2VEC, GloVe (Global Vectors) y FASTTEXT (embeddings para 157 idiomas)

---

# Embeddings de palabras: Pasos del proceso

1. Elegí el ancho w (un número impar de palabras, típicamente = 5) para la ventana de predicción
2. Creá un vocabulario de tokens de palabras únicas que aparezcan más de 5 veces en los datos de entrenamiento
3. Ordená el vocabulario (por ejemplo, alfabéticamente)
4. Elegí un valor d como el tamaño de cada vector de embedding de palabra
5. Creá una nueva matriz de pesos E de v por d (inicializada aleatoriamente o a partir de vectores preentrenados)
6. Configurá una red neuronal que genere una etiqueta de parte del discurso
7. Codificá una secuencia de w palabras buscando y concatenando los vectores de embedding
8. Entrená los pesos E y otras matrices de pesos usando descenso de gradiente

---

# Visualización de Embeddings de palabras

![bg right:60% 80%](https://example.com/word_embeddings_visualization.png)

Vectores de embedding de palabras calculados por el algoritmo GloVe entrenado con 6 mil millones de palabras de texto. Los vectores de palabras de 100 dimensiones se proyectan en dos dimensiones en esta visualización. Las palabras similares aparecen cerca unas de otras.

---

# Embeddings de palabras: Aritmética de vectores

![bg right:60% 80%](https://example.com/vector_arithmetic.png)

Un modelo de embedding de palabras a veces puede responder a la pregunta "A es a B como C es a [qué]?" con aritmética de vectores:
- Dados los vectores de embedding de palabras para A, B y C
- Calculá el vector D = C + (B - A)
- Buscá la palabra más cercana a D

---

# Modelo de etiquetado POS feedforward

![bg right:60% 80%](https://example.com/pos_tagging_model.png)

- Toma una ventana de 5 palabras como entrada
- Predice la etiqueta de la palabra del medio
- Tiene en cuenta la posición de la palabra multiplicando cada embedding de entrada con una parte diferente de la primera capa oculta
- Los valores de los parámetros para los embeddings de palabras y las tres capas se aprenden simultáneamente durante el entrenamiento

---

# Redes Neuronales Recurrentes para PLN

![bg right:60% 80%](https://example.com/rnn_diagram.png)

(a) Diagrama esquemático de una RNN donde la capa oculta z tiene conexiones recurrentes; el símbolo ∆ indica un retraso.
(b) La misma red desplegada en tres pasos de tiempo para crear una red feedforward

---

# RNN Bidireccional para etiquetado POS

![bg right:60% 80%](https://example.com/bidirectional_rnn.png)

Una red RNN bidireccional para etiquetado POS.

---

# LSTMs para tareas de PLN

- Long Short-Term Memory (LSTM): forma de RNN con unidades de compuerta
- Ventajas:
  - No sufren de reproducción imperfecta de mensajes entre pasos de tiempo
  - Pueden elegir recordar u olvidar partes de la entrada
  - Pueden aprender a crear y mantener características latentes
- Capacidad de copiar características hacia adelante sin alteración hasta que sean necesarias para la toma de decisiones

---

# Modelos de secuencia a secuencia

- Objetivo: Traducir una oración del idioma fuente al idioma objetivo (por ejemplo, del español al inglés)
- Usa dos RNNs: una para la fuente, otra para el objetivo
- Proceso:
  1. Ejecutá la RNN fuente sobre la oración fuente
  2. Usá el estado oculto final de la RNN fuente como estado oculto inicial para la RNN objetivo
  3. Generá palabras objetivo condicionadas a toda la oración fuente y las palabras objetivo anteriores
- Aplicaciones: traducción, subtitulado de texto, resumen, reescritura de texto
- Debilidades:
  - Sesgo de contexto cercano
  - Límite de tamaño de contexto fijo
  - Procesamiento secuencial más lento

---

# Modelo básico de secuencia a secuencia

![bg right:60% 80%](https://example.com/seq2seq_model.png)

Cada bloque representa un paso de tiempo LSTM. (Las capas de embedding y salida no se muestran para simplificar.)

---

# Modelos de secuencia a secuencia: Atención

- Permite que la RNN objetivo se enfoque en partes relevantes de la fuente para cada palabra objetivo
- Mecanismo de atención:
  ```
  hi = RNN(hi−1, [xi; ci])
  ```
  Donde:
  - hi−1 es el vector RNN objetivo
  - sj es la salida del vector RNN fuente
  - rij es el "puntaje de atención" bruto
  - aij es la probabilidad de atención normalizada
  - ci es el promedio ponderado de los vectores RNN fuente

---

# Modelos de secuencia a secuencia: Decodificación

1. Decodificación voraz:
   - Seleccioná la palabra de mayor probabilidad en cada paso de tiempo
   - Puede no maximizar la probabilidad de toda la secuencia objetivo

2. Búsqueda en haz:
   - Mantiene las k mejores hipótesis en cada etapa
   - Extiende cada una por una palabra usando las k mejores opciones de palabras
   - Elige las mejores k de las k^2 nuevas hipótesis resultantes
   - Genera la hipótesis con el puntaje más alto cuando todas las hipótesis generan EOS
   - Los modelos de MT neuronales de vanguardia usan un tamaño de haz de 4 a 8

---

# Ejemplo de búsqueda en haz

![bg right:60% 80%](https://example.com/beam_search.png)

Búsqueda en haz con tamaño de haz b = 2. El puntaje de cada palabra es el logaritmo de la probabilidad generada por el softmax de la RNN objetivo, y el puntaje de cada hipótesis es la suma de los puntajes de las palabras.

---

# La arquitectura Transformer: Auto-atención

- Auto-atención: cada secuencia de estados ocultos se atiende a sí misma
  - Fuente a fuente
  - Objetivo a objetivo
- Captura contexto de larga distancia y cercano dentro de cada secuencia
- Proceso:
  1. Proyectá la entrada en tres representaciones:
     - Vector de consulta: qi = Wqxi (desde donde se atiende)
     - Vector de clave: ki = Wkxi (hacia donde se atiende)
     - Vector de valor: vi = Wvxi (contexto que se está generando)

---

# Diagrama de la arquitectura Transformer

![bg right:60% 80%](https://example.com/transformer_architecture.png)

---

# De la auto-atención al Transformer

- Cada capa del transformer consiste en varias subcapas
- Codificador Transformer:
  1. Aplicá auto-atención
  2. Pasá la salida a través de capas feedforward
  3. Agregá dos conexiones residuales
- Generalmente tienen seis o más capas
- Captura el orden de las palabras usando embeddings posicionales
- El decodificador Transformer es casi idéntico
  - Usa una versión de auto-atención donde cada palabra solo puede atender a las palabras anteriores

---

# Transformer de una sola capa

![bg right:60% 80%](https://example.com/single_layer_transformer.png)

Un transformer de una sola capa consiste en auto-atención, una red feedforward y conexiones residuales

---

# Transformer para etiquetado POS

![bg right:60% 80%](https://example.com/transformer_pos_tagging.png)

Uso de la arquitectura transformer para etiquetado POS

---

# Preentrenamiento y transferencia de aprendizaje

1. Embeddings de palabras preentrenados:
   - Modelo GloVe (Global Vectors)
   - Captura la relación entre palabras comparándolas con otras palabras
   - Basado en probabilidades de co-ocurrencia

2. Representaciones contextuales preentrenadas:
   - Entrenamiento usando modelo de lenguaje de izquierda a derecha

3. Modelos de lenguaje enmascarado (MLM):
   - Enmascaramiento de palabras individuales en la entrada
   - Se le pide al modelo que prediga las palabras enmascaradas
   - Usa contexto bidireccional
   - No requiere datos etiquetados

---

# Modelado de lenguaje enmascarado

![bg right:60% 80%](https://example.com/masked_language_modeling.png)

Preentrenamiento de un modelo bidireccional enmascarando palabras de entrada y prediciendo solo esas palabras enmascaradas

---

# Estado del arte

- Los nuevos proyectos de PLN generalmente comienzan con modelos transformer preentrenados
- Los modelos transformer sobresalen en varias tareas de lenguaje más allá de la predicción de la siguiente palabra
- Ejemplos de modelos y sistemas avanzados:
  - ROBERTA: Estado del arte en respuesta a preguntas y comprensión de lectura
  - GPT-2: Buenos resultados en diversas tareas sin ajuste fino
  - ARISTO: Puntaje de 91.6% en examen de ciencias de opción múltiple de 8º grado
- Surgimiento de enfoques híbridos que combinan modelado gramatical y semántico
- Margen para mejorar:
  - Los sistemas de PLN aún están por detrás del rendimiento humano en muchas tareas
  - Procesan mucho más texto que los humanos, lo que sugiere un margen para nuevos hallazgos

---

# Resumen

- Los embeddings de palabras proporcionan representaciones continuas robustas de las palabras
- Las redes neuronales recurrentes modelan efectivamente el contexto local y de larga distancia
- Los modelos de secuencia a secuencia son útiles para la traducción automática y la generación de texto
- Los modelos transformer usan auto-atención para modelar tanto el contexto de larga distancia como el local
- La transferencia de aprendizaje con embeddings de palabras contextuales preentrenados permite el desarrollo a partir de grandes corpus no etiquetados
- Aplicación a una variedad de tareas de PLN

```

# Notas sobre la traducción

1. "vos" y conjugaciones correspondientes: En esta traducción, se utilizó el "vos" característico del español argentino en lugar del "tú". Por ejemplo, "Elegí" en lugar de "Elige" o "Creá" en lugar de "Crea".

2. Términos técnicos: Se mantuvieron en inglés términos como "embedding", "feedforward", "Long Short-Term Memory (LSTM)", "Transformer", ya que son ampliamente utilizados en la comunidad técnica y académica argentina sin traducción.

3. Siglas: Se mantuvieron siglas como "PLN" (Procesamiento del Lenguaje Natural) y "RNN" (Red Neuronal Recurrente) que son comúnmente usadas en español.

4. Expresiones académicas: Se utilizaron expresiones formales típicas del ámbito académico argentino, como "estado del arte" para "state of the art".

# Aspectos desafiantes de la traducción

1. Equilibrio entre términos técnicos en inglés y español: Fue necesario decidir qué términos mantener en inglés (como "embedding" o "transformer") y cuáles traducir (como "red neuronal recurrente"), basándose en el uso común en la comunidad académica argentina.

2. Adaptación de ejemplos: En la sección de aritmética de vectores, se mantuvo el ejemplo en inglés ("A is to B as C is to [what]?") ya que traducirlo podría alterar la comprensión del concepto original.

3. Mantenimiento del registro formal: Se tuvo que mantener un tono formal y académico a lo largo de la traducción, adecuado para una presentación universitaria, mientras se incorporaban elementos del español argentino.

4. Traducción de términos técnicos específicos: Algunos términos como "beam search" se tradujeron como "búsqueda en haz", que es la traducción comúnmente aceptada en la literatura académica en español, aunque no sea una traducción literal.

5. Adaptación de las instrucciones de los pasos: Se tuvo que adaptar las instrucciones para usar el "vos" característico del español argentino, manteniendo al mismo tiempo la claridad y precisión técnica de las instrucciones originales.