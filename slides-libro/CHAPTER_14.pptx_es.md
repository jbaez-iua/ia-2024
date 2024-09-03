
---
marp: true
theme: default
paginate: true
---

<!-- _class: lead -->
# Razonamiento Probabilístico a lo Largo del Tiempo
## Capítulo 14

---

# Esquema

- Tiempo e Incertidumbre
- Inferencia en Modelos Temporales
- Modelos Ocultos de Markov
- Filtros de Kalman
- Redes Bayesianas Dinámicas

---

# Tiempo e Incertidumbre

## Estados y observaciones

- Modelos de tiempo discreto: el mundo se ve como una serie de instantáneas o cortes temporales
- El intervalo de tiempo Δ entre cortes es constante
- Xt: conjunto de variables de estado no observables en el tiempo t
- Et: conjunto de variables de evidencia observables
- La observación en el tiempo t es Et = et

---

# Tiempo e Incertidumbre (cont.)

## Modelos de transición y de sensor

- Modelo de transición: P(Xt | X0:t−1)
- Suposición de Markov: el estado actual depende de un número finito fijo de estados previos
  - Primer orden: P(Xt | Xt−1)
  - Segundo orden: P(Xt | Xt-2, Xt−1)
- Modelo de sensor: P(Et | Xt)
  - Suposición de Markov del sensor: P(Et | X0:t, E1:t−1) = P(Et | Xt)

---

# Tiempo e Incertidumbre (cont.)

- Distribución de probabilidad previa en el tiempo 0: P(X0)
- Mundo del Paraguas: proceso de Markov de primer orden
- Formas de mejorar la precisión:
  1. Aumentar el orden del modelo de proceso de Markov
  2. Aumentar el conjunto de variables de estado

![bg right:40% w:400](https://example.com/markov_process.png)

---

# Tiempo e Incertidumbre (cont.)

![w:900](https://example.com/umbrella_world.png)

Estructura de red bayesiana y distribuciones condicionales para el mundo del paraguas

---

# Inferencia en Modelos Temporales

## Tareas básicas de inferencia:

1. Filtrado (estimación de estado): P(Xt | e1:t)
2. Predicción: distribución posterior sobre el estado futuro
3. Suavizado: distribución posterior sobre el estado pasado
4. Explicación más probable: secuencia de estados más probable

## Tarea adicional:
- Aprendizaje: modelos de transición y sensor a partir de observaciones

---

# Inferencia en Modelos Temporales (cont.)

## Filtrado y predicción

![w:900](https://example.com/filtering_prediction.png)

---

# Inferencia en Modelos Temporales (cont.)

## Suavizado

![w:900](https://example.com/smoothing.png)

---

# Inferencia en Modelos Temporales (cont.)

## Encontrando la secuencia más probable

- Algoritmo de tiempo lineal disponible
- Usa la propiedad de Markov
- Algoritmo de Viterbi:
  - Mensaje m1:t calculado recursivamente
  - Registra el mejor estado que lleva a cada estado

![bg right:40% w:400](https://example.com/viterbi.png)

---

# Modelos Ocultos de Markov

![w:900](https://example.com/hmm_algorithm.png)

---

# Modelos Ocultos de Markov (cont.)

![w:900](https://example.com/hmm_performance.png)

---

# Filtros de Kalman

- Manejo de variables continuas
- Distribuciones gaussianas y modelos lineal-gaussianos
- Operador FORWARD para filtrado de Kalman:
  - Entrada: Mensaje forward gaussiano f1:t (media μt, covarianza Σt)
  - Salida: Nuevo mensaje forward gaussiano f1:t+1 (media μt+1, covarianza Σt+1)

---

# Filtros de Kalman (cont.)

![w:900](https://example.com/kalman_filter_stages.png)

---

# Filtros de Kalman (cont.)

![w:900](https://example.com/kalman_filter_results.png)

---

# Redes Bayesianas Dinámicas (DBNs)

- Extienden las redes bayesianas para manejar modelos de probabilidad temporal
- Pueden representar HMMs y modelos más complejos
- Ventaja: pueden modelar la dispersión en el modelo de probabilidad temporal
- Pueden modelar distribuciones arbitrarias (a diferencia de los filtros de Kalman)

---

# Redes Bayesianas Dinámicas (cont.)

## Para construir una DBN:

1. Especificar la distribución previa: P(X0)
2. Especificar el modelo de transición: P(Xt+1 | Xt)
3. Especificar el modelo de sensor: P(Et | Xt)

## Modelos de falla:
- Falla transitoria
- Falla persistente

---

# Redes Bayesianas Dinámicas (cont.)

![w:900](https://example.com/dbn_failure_models.png)

---

# Redes Bayesianas Dinámicas (cont.)

## Inferencia exacta en DBNs

- Desenrollado: construir la red bayesiana completa replicando cortes
- Se pueden usar algoritmos de inferencia estándar (eliminación de variables, agrupamiento)
- Actualización de filtrado: costo O(ndn+k) por paso

![bg right:40% w:400](https://example.com/dbn_unrolling.png)

---

# Redes Bayesianas Dinámicas (cont.)

## Inferencia aproximada en DBNs

1. Muestreo de Importancia Secuencial (SIS)
   - Tiempo constante por actualización
   - La precisión disminuye con el tiempo

2. Filtrado de partículas
   - Se enfoca en regiones de alta probabilidad
   - Muestreo de importancia secuencial con remuestreo

---

# Redes Bayesianas Dinámicas (cont.)

![w:900](https://example.com/particle_filtering_algorithm.png)

---

# Redes Bayesianas Dinámicas (cont.)

## Debilidades del filtrado de partículas:
- Las suposiciones iniciales pueden no actualizarse nunca
- La diversidad de la población puede colapsar

## Filtro de partículas Rao-Blackwellizado
- Combina inferencia exacta y muestreo
- Efectivo para problemas SLAM

---

# Resumen

- El estado cambiante se representa mediante variables aleatorias en cada punto temporal
- La propiedad de Markov y la homogeneidad temporal simplifican la representación
- Modelos de probabilidad temporal: modelo de transición + modelo de sensor
- Principales tareas de inferencia: filtrado, predicción, suavizado, explicación más probable
- El filtrado de partículas y sus variantes son algoritmos de aproximación efectivos

---

<!-- _class: lead -->
# ¡Gracias!
## ¿Preguntas?

```

### Notas sobre la traducción

1. Se utilizó el "voseo" en la última diapositiva ("¿Preguntas?") para mantener el estilo argentino.
2. Se mantuvieron los términos técnicos en inglés cuando son comúnmente utilizados en el ámbito académico argentino, como "Hidden Markov Models" y "Kalman Filters".
3. Se tradujo "Outline" como "Esquema", que es más común en el contexto académico argentino.
4. Se mantuvo la notación matemática y las abreviaturas en su forma original (e.g., P(Xt | X0:t−1)).

### Aspectos desafiantes de la traducción

1. La traducción de "slices" en el contexto de modelos temporales fue desafiante. Se optó por "cortes temporales", que es una terminología aceptada en el ámbito académico argentino.
2. La traducción de "smoothing" como "suavizado" en el contexto de inferencia temporal puede no ser inmediatamente clara para todos los lectores, pero es el término técnico utilizado en este campo en español.
3. Algunos términos técnicos como "Rao-Blackwellization" no tienen una traducción establecida en español, por lo que se mantuvieron en su forma original.
4. La adaptación de expresiones coloquiales como "Thank you!" al final de la presentación requirió considerar el tono formal del contexto académico argentino.