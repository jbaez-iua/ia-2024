
# Aprendizaje de Modelos Probabilísticos
## Capítulo 21

Inteligencia Artificial: Un Enfoque Moderno
Cuarta Edición, Edición Global

© 2022 Pearson Education Ltd.

---

# Esquema

- Aprendizaje Estadístico
- Aprendizaje con Datos Completos
- Aprendizaje con Variables Ocultas: El Algoritmo EM

---

# Aprendizaje Bayesiano Completo

- Ve el aprendizaje como una actualización bayesiana de una distribución de probabilidad sobre el espacio de hipótesis
- H es la variable de hipótesis, valores h1, h2, ..., probabilidad a priori P(H)
- La j-ésima observación dj da el resultado de la variable aleatoria Dj
- Datos de entrenamiento d = d1, ..., dN

---

# Aprendizaje Bayesiano Completo (cont.)

Dados los datos hasta ahora, cada hipótesis tiene una probabilidad posterior:

$$P(h_i|d) = \alpha P(d|h_i)P(h_i)$$

donde P(d|hi) se llama la verosimilitud

Las predicciones usan un promedio ponderado por verosimilitud sobre las hipótesis:

$$P(X|d) = \sum_i P(X|d, h_i)P(h_i|d) = \sum_i P(X|h_i)P(h_i|d)$$

¡No es necesario elegir una hipótesis de mejor estimación!

---

# Ejemplo: Bolsas de Caramelos

Supongamos que hay cinco tipos de bolsas de caramelos:
- 10% son h1: 100% caramelos de cereza
- 20% son h2: 75% caramelos de cereza + 25% caramelos de lima
- 40% son h3: 50% caramelos de cereza + 50% caramelos de lima
- 20% son h4: 25% caramelos de cereza + 75% caramelos de lima
- 10% son h5: 100% caramelos de lima

Luego observamos caramelos sacados de alguna bolsa:
- ¿Qué tipo de bolsa es?
- ¿De qué sabor será el próximo caramelo?

---

# Probabilidad Posterior de Hipótesis

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW051bWJlciBvZiBtdWVzdHJhcyBlbiBkXSAtLT4gQltQcm9iYWJpbGlkYWQgcG9zdGVyaW9yIGRlIGhpcMOzdGVzaXNdXG4gICAgQiAtLT4gQ1tQKGgxIHwgZCldXG4gICAgQiAtLT4gRFtQKGgyIHwgZCldXG4gICAgQiAtLT4gRVtQKGgzIHwgZCldXG4gICAgQiAtLT4gRltQKGg0IHwgZCldXG4gICAgQiAtLT4gR1tQKGg1IHwgZCldXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)

---

# Probabilidad de Predicción

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW051bWJlciBkZSBtdWVzdHJhcyBlbiBkXSAtLT4gQltQKGVsIHByb3hpbW8gY2FyYW1lbG8gZXMgZGUgbGltYSB8IGQpXVxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

---

# Aproximación MAP

- Sumar sobre el espacio de hipótesis a menudo es intratable
- Aprendizaje de máximo a posteriori (MAP): elegir hMAP maximizando P(hi|d)
- Maximizar P(d|hi)P(hi) o log P(d|hi) + log P(hi)
- Los términos de log pueden verse como (negativo de) bits para codificar datos dada la hipótesis + bits para codificar la hipótesis
- Esta es la idea básica del aprendizaje de longitud de descripción mínima (MDL)
- Para hipótesis deterministas, P(d|hi) es 1 si es consistente, 0 en caso contrario
  ⇒ MAP = hipótesis consistente más simple (cf. ciencia)

---

# Aproximación ML

- Para conjuntos de datos grandes, la probabilidad a priori se vuelve irrelevante
- Aprendizaje de máxima verosimilitud (ML): elegir hML maximizando P(d|hi)
- Simplemente obtener el mejor ajuste a los datos; idéntico a MAP para probabilidad a priori uniforme
- ML es el método de aprendizaje estadístico "estándar" (no bayesiano)

---

# Modelo de Red Bayesiana

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgICBBW01vZGVsbyBkZSByZWQgYmF5ZXNpYW5hXVxuICAgIEEgLS0-IEJbQ2FyYW1lbG9zIGNvbiBwcm9wb3JjacOzbiBkZXNjb25vY2lkYSBkZSBjZXJlemFzIHkgbGltYXNdXG4gICAgQSAtLT4gQ1tFbCBjb2xvciBkZWwgZW52b2x0b3JpbyBkZXBlbmRlIGRlbCBzYWJvciBkZWwgY2FyYW1lbG9dXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)

---

# Aprendizaje de Parámetros ML en Redes Bayesianas

- Bolsa de un nuevo fabricante; fracción θ de caramelos de cereza
- Cualquier θ es posible: continuo de hipótesis hθ
- θ es un parámetro para esta familia simple (binomial) de modelos

$$P(F=cereza) = \theta$$

---

# Aprendizaje de Parámetros ML en Redes Bayesianas (cont.)

Supongamos que desenvolvemos N caramelos, c cerezas y ℓ = N − c limas

Estas son observaciones i.i.d. (independientes e idénticamente distribuidas), entonces

$$P(d|h_\theta) = \prod_{j=1}^N P(d_j|h_\theta) = \theta^c \cdot (1-\theta)^\ell$$

Maximizar esto con respecto a θ—que es más fácil para la log-verosimilitud:

$$L(d|h_\theta) = \log P(d|h_\theta) = \sum_{j=1}^N \log P(d_j|h_\theta) = c \log \theta + \ell \log(1-\theta)$$

$$\frac{\partial L(d|h_\theta)}{\partial \theta} = \frac{c}{\theta} - \frac{\ell}{1-\theta} = 0 \Rightarrow \theta = \frac{c}{c+\ell} = \frac{c}{N}$$

Parece sensato, ¡pero causa problemas con conteos de 0!

---

# Múltiples Parámetros

El envoltorio rojo/verde depende probabilísticamente del sabor:

$$P(F=cereza) = \theta$$
$$P(W=rojo|F=cereza) = \theta_1$$
$$P(W=rojo|F=lima) = \theta_2$$

---

# Múltiples Parámetros (cont.)

Verosimilitud para, por ejemplo, caramelo de cereza en envoltorio verde:

$$P(F=cereza, W=verde|h_{\theta,\theta_1,\theta_2}) = P(F=cereza|h_{\theta,\theta_1,\theta_2}) P(W=verde|F=cereza, h_{\theta,\theta_1,\theta_2}) = \theta \cdot (1-\theta_1)$$

N caramelos, rc caramelos de cereza con envoltorio rojo, etc.:

$$P(d|h_{\theta,\theta_1,\theta_2}) = \theta^c(1-\theta)^\ell \cdot \theta_1^{rc}(1-\theta_1)^{gc} \cdot \theta_2^{r\ell}(1-\theta_2)^{g\ell}$$

$$L = [c \log \theta + \ell \log(1-\theta)] + [rc \log \theta_1 + gc \log(1-\theta_1)] + [r\ell \log \theta_2 + g\ell \log(1-\theta_2)]$$

---

# Múltiples Parámetros (cont.)

Las derivadas de L contienen solo el parámetro relevante:

$$\frac{\partial L}{\partial \theta} = \frac{c}{\theta} - \frac{\ell}{1-\theta} = 0 \Rightarrow \theta = \frac{c}{c+\ell}$$

$$\frac{\partial L}{\partial \theta_1} = \frac{rc}{\theta_1} - \frac{gc}{1-\theta_1} = 0 \Rightarrow \theta_1 = \frac{rc}{rc+gc}$$

$$\frac{\partial L}{\partial \theta_2} = \frac{r\ell}{\theta_2} - \frac{g\ell}{1-\theta_2} = 0 \Rightarrow \theta_2 = \frac{r\ell}{r\ell+g\ell}$$

Con datos completos, los parámetros se pueden aprender por separado

---

# Modelos Naive Bayes

- Con valores de atributos observados x1, ..., xn, la probabilidad de cada clase viene dada por:

$$P(C|x_1,...,x_n) = \alpha P(C) \prod_{i=1}^n P(x_i|C)$$

- Se puede obtener una predicción determinista eligiendo la clase más probable
- El método aprende bastante bien pero no tan bien como el aprendizaje de árboles de decisión
- El aprendizaje Naive Bayes resulta sorprendentemente bien en una amplia gama de aplicaciones
- Escala bien a problemas grandes con n atributos booleanos: hay solo 2n + 1 parámetros

---

# Modelos Naive Bayes: Curva de Aprendizaje

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW051bWVybyBkZSBlamVtcGxvc10gLS0-IEJbUHJlY2lzacOzbiBkZSBwcmVkaWNjacOzbl1cbiAgICBCIC0tPiBDW05haXZlIEJheWVzXVxuICAgIEIgLS0-IERbw4FyYm9sIGRlIERlY2lzacOzbl1cbiIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In0sInVwZGF0ZUVkaXRvciI6ZmFsc2V9)

---

# Ejemplo: Modelo Gaussiano Lineal

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW3hdIC0tPiBCW3ldXG4gICAgQiAtLT4gQ1tQKHl8eCldXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)

$$P(y|x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(y-(\theta_1x+\theta_2))^2}{2\sigma^2}}$$

Maximizar P(y|x) con respecto a θ1, θ2 es equivalente a minimizar:

$$E = \sum_{j=1}^N (y_j - (\theta_1x_j + \theta_2))^2$$

Es decir, minimizar la suma de errores cuadrados da la solución ML para un ajuste lineal asumiendo ruido gaussiano de varianza fija.

---

# Aprendizaje Bayesiano de Parámetros

- Distribución previa sobre parámetros
- Distribución posterior sobre parámetros dados los datos
- Predicción promediando sobre la distribución posterior de parámetros

---

# Estimación de Densidad con Modelos No Paramétricos

- k vecinos más cercanos: para estimar la densidad de probabilidad desconocida en un punto de consulta x, simplemente podemos medir la densidad de los puntos de datos en el vecindario de x.
- Usar funciones kernel

---

# Ejemplo de Estimación de Densidad

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgICBBW01lemNsYSBkZSBHYXVzc2lhbmFzXSAtLT4gQltHcsOhZmljbyAzRF1cbiAgICBBIC0tPiBDW011ZXN0cmEgZGUgMTI4IHB1bnRvc11cbiAgICBDIC0tPiBEW1B1bnRvcyBkZSBjb25zdWx0YV1cbiAgICBDIC0tPiBFWzEwIHZlY2luZGFyaW9zIG3DoXMgY2VyY2Fub3NdXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)

---

# Estimación de Densidad: k Vecinos Más Cercanos

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW2sgPSAzXSAtLT4gQltEZW1hc2lhZG8gaXJyZWd1bGFyXVxuICAgIENbayA9IDEwXSAtLT4gRFtDYXNpIGp1c3RvXVxuICAgIEVbayA9IDQwXSAtLT4gRltEZW1hc2lhZG8gc3VhdmVdXG4gICAgR1tNZWpvciB2YWxvciBwYXJhIGtdIC0tPiBIW0VsZWdpZG8gcG9yIHZhbGlkYWNpw7NuIGNydXphZGFdXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)

---

# Aprendizaje con Variables Ocultas: El Algoritmo EM

- Muchos problemas del mundo real tienen variables ocultas (a veces llamadas variables latentes)
- La maximización de expectativas ayuda con las variables ocultas:
  1. Inferir la probabilidad de que cada punto de datos pertenezca a cada componente
  2. Reajustar los componentes a los datos, donde cada componente se ajusta al conjunto de datos completo con cada punto ponderado por la probabilidad de que pertenezca a ese componente
  3. El proceso se itera hasta la convergencia

---

# Algoritmo EM: Mezcla de Gaussianas

Para la mezcla de Gaussianas, inicializar los parámetros del modelo de mezcla arbitrariamente e iterar el paso E y el paso M

Observaciones:
- La log-verosimilitud para el modelo final aprendido supera ligeramente la del modelo original
- EM aumenta la log-verosimilitud de los datos en cada iteración

---

# Aprendizaje de Redes Bayesianas con Variables Ocultas

Ejemplo: Dos bolsas de caramelos mezcladas
- Los caramelos se describen por tres características: Sabor, Envoltorio y Agujero
- La distribución de caramelos en cada bolsa se describe mediante un modelo Naive Bayes

---

# Aprendizaje de Redes Bayesianas con Variables Ocultas (cont.)

Usando la regla de Bayes y aplicando independencia condicional:

El conteo esperado de caramelos de cereza de la bolsa 1 viene dado por:

$$E[n_{1,cereza}] = \sum_{j:F_j=cereza} P(B_j=1|F_j,W_j,H_j)$$

La actualización se da por los conteos esperados normalizados de la siguiente manera:

$$\theta_{1,cereza} = \frac{E[n_{1,cereza}]}{E[n_{1,cereza}] + E[n_{1,lima}]}$$

---

# Modelos de Mezcla

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgICBBW01vZGVsbyBkZSBtZXpjbGEgcGFyYSBjYXJhbWVsb3NdIC0tPiBCW0JvbHNhIChubyBvYnNlcnZhZGEpXVxuICAgIEIgLS0-IENbU2Fib3JdXG4gICAgQiAtLT4gRFtFbnZvbHRvcmlvXVxuICAgIEIgLS0-IEVbQWd1amVyb11cbiAgICBGW01lemNsYSBHYXVzc2lhbmFdIC0tPiBHW0NvbXBvbmVudGUgQ11cbiAgICBHIC0tPiBIW01lZGlhIHkgY292YXJpYW56YSBkZSBYXVxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

---

# Algoritmo EM: Log-verosimilitud

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW0l0ZXJhY2nDs24gRU1dIC0tPiBCW0xvZy12ZXJvc2ltaWxpdHVkIGRlIGxvcyBkYXRvc11cbiAgICBDIC0tPiBEW01vZGVsbyBkZSBtZXpjbGEgR2F1c3NpYW5hXVxuICAgIEMgLS0-IEVbUmVkIEJheWVzaWFuYV1cbiIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In0sInVwZGF0ZUVkaXRvciI6ZmFsc2V9)

---

# Aprendizaje de Modelos Ocultos de Markov

- Una aplicación de EM implica aprender las probabilidades de transición en modelos ocultos de Markov (HMM)
- Un HMM se puede representar mediante una red bayesiana dinámica con una única variable de estado discreta
- Cada punto de datos consiste en una secuencia de observaciones de longitud finita

---

# Aprendizaje de Modelos Ocultos de Markov (cont.)

Probabilidad de transición del estado i al estado j:

Calcular la proporción esperada de veces que el sistema experimenta una transición al estado j cuando está en el estado i:

$$a_{ij} = \frac{E[n_{i \rightarrow j}]}{\sum_k E[n_{i \rightarrow k}]}$$

---

# Modelo Oculto de Markov: Red Bayesiana Dinámica

![height:400px](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW0VzdGFkb10gLS0-IEJbRXN0YWRvXVxuICAgIEIgLS0-IENbRXN0YWRvXVxuICAgIEEgLS0-IERbT2JzZXJ2YWNpw7NuXVxuICAgIEIgLS0-IEVbT2JzZXJ2YWNpw7NuXVxuICAgIEMgLS0-IEZbT2JzZXJ2YWNpw7NuXVxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

---

# Resumen

- Los métodos de aprendizaje bayesiano formulan el aprendizaje como una forma de inferencia probabilística, usando las observaciones para actualizar una distribución previa sobre hipótesis.
- El aprendizaje de máximo a posteriori (MAP) selecciona una única hipótesis más probable dados los datos.
- El aprendizaje de máxima verosimilitud simplemente selecciona la hipótesis que maximiza la verosimilitud de los datos; es equivalente al aprendizaje MAP con una probabilidad previa uniforme.
- El aprendizaje Naive Bayes es una técnica particularmente efectiva que escala bien.
- Cuando algunas variables están ocultas, se pueden encontrar soluciones de máxima verosimilitud local usando el algoritmo EM.
- Los modelos no paramétricos representan una distribución usando la colección de puntos de datos.

```

## Notas sobre la traducción

1. "vos" form: En esta traducción no se utilizó la forma "vos" ya que el texto original está en un tono formal y profesional, por lo que se mantuvo el uso de "usted" implícito.

2. Términos técnicos: Se mantuvieron en su forma original en inglés términos como "Naive Bayes", "Maximum a posteriori (MAP)", "Maximum-likelihood (ML)", y "Expectation-maximization (EM)", ya que son ampliamente utilizados en la literatura técnica en español.

3. "Wrapper": Se tradujo como "envoltorio" en lugar de "envoltorio" o "envase", que es más común en Argentina para referirse al empaque de caramelos.

4. "Candy": Se tradujo como "caramelo" en lugar de "golosina" o "dulce", que son términos más utilizados en Argentina.

5. "Log likelihood": Se tradujo como "log-verosimilitud", que es el término técnico utilizado en estadística en español.

## Aspectos desafiantes de la traducción

1. Terminología técnica: Mantener el equilibrio entre la precisión técnica y la comprensibilidad fue un desafío, especialmente con términos como "Naive Bayes", "Maximum a posteriori", etc.

2. Fórmulas matemáticas: Asegurar que las fórmulas matemáticas se mantuvieran intactas y correctamente formateadas en Markdown fue crucial.

3. Diagramas: Los diagramas se mantuvieron en inglés ya que están representados como enlaces a imágenes generadas externamente. En una traducción completa, estos diagramas deberían ser regenerados con texto en español.

4. Contexto académico: Adaptar el contenido al contexto académico argentino sin perder la esencia del original requirió cuidado, especialmente en términos de vocabulario técnico y estructuras de oraciones formales.

5. Longitud de las oraciones: El español tiende a usar oraciones más largas que el inglés, lo que a veces requirió reestructurar las oraciones para mantener la claridad y fluidez.