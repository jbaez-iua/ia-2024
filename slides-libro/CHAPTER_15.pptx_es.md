
---
marp: true
theme: default
paginate: true
---

# Tomando Decisiones Simples
## Capítulos 15 y 16

Inteligencia Artificial: Un Enfoque Moderno
Cuarta Edición, Edición Global © 2022 Pearson Education Ltd.

---

# Esquema

- Combinando creencias y deseos bajo incertidumbre
- Utilidades
- La base de la teoría de la utilidad
- Funciones de utilidad
- Funciones de utilidad multiatributo
- Redes de decisión
- Valor de la información
- Preferencias desconocidas

---

# La Base de la Teoría de la Utilidad

## Restricciones sobre preferencias racionales

Un agente elige entre:
- Premios (A, B, etc.)
- Loterías: situaciones con premios inciertos

![width:500px](https://mermaid.ink/img/pako:eNpNjrEOgjAURX-l6WwCgyQOJg4OxsHBmA5voBUetA-1BU1j_l1AHcztueeem9MBY8kEHfTGaoEf7aTnsO8-AoJzI1GUynZwQtOgkJYr1SgtZWe4_5uxqpRq3p2_U_h0Vjx6HXlg5qn7-ZkqpQXTb89xgzh6H4RxkAQsj1bBOkxZFsZRki5e9L5hAoUYwcItaB9KzpDBddY-kRE2SiozwjkrwcFkNjQCr6zsoYEzzc-pP8Yv8JNR1Q?type=png)

Notación: A ≺ B (A preferido a B), A ∼ B (indiferencia entre A y B)

---

# Preferencias racionales

Idea: las preferencias de un agente racional deben obedecer restricciones.

Preferencias racionales ⇒ comportamiento describible como maximización de la utilidad esperada

## Restricciones:

1. Ordenabilidad: (A ≺ B) ∨ (B ≺ A) ∨ (A ∼ B)
2. Transitividad: (A ≺ B) ∧ (B ≺ C) ⇒ (A ≺ C)
3. Continuidad: A ≺ B ≺ C ⇒ ∃p[p, A; 1 - p, C] ∼ B
4. Sustituibilidad: A ∼ B ⇒ [p, A; 1 - p, C] ∼ [p, B; 1 - p, C]
5. Monotonicidad: A ≺ B ⇒ (p ≥ q ⇔ [p, A; 1 - p, B] ≺ [q, A; 1 - q, B])

---

# Preferencias racionales (continuación)

Violar las restricciones lleva a una irracionalidad evidente

Ejemplo: un agente con preferencias intransitivas puede ser inducido a regalar todo su dinero

![width:600px](https://mermaid.ink/img/pako:eNpNkDFuwzAMRa9CaHIBO0OWokOHDkWHohcgZTGxUFkyRDpFYPjupaK0BbeP7_H_Ujs0ziU0aNFbZ-CjX4wXcBg-EkJwM1NcaddDQDujtFYY3aKNVr0V8V9jUr0x7Xvwd8qQzorHYJMMkr10Pz9TrY1k_u15bhBH75MkTbOUl9EqWIdDXiRpmuWLF71vmEEjJlgEBf1DLTmRoOtiQ6YTbIzWdoJzUUOAWW0YFV1F3UMLwbA8p_4Yv5Rwca4?type=png)

---

# Maximizando la utilidad esperada

**Teorema** (Ramsey, 1931; von Neumann y Morgenstern, 1944):

Dadas las preferencias que satisfacen las restricciones, existe una función real U tal que:

1. U(A) ≥ U(B) ⇔ A ≺ B
2. U([p₁, S₁; ... ; pₙ, Sₙ]) = Σᵢ pᵢU(Sᵢ)

**Principio MEU**: Elegir la acción que maximiza la utilidad esperada

Nota: un agente puede ser completamente racional (consistente con MEU) sin representar ni manipular utilidades y probabilidades
Ej., una tabla de búsqueda para ta-te-ti perfecto

---

# Funciones de Utilidad

Las utilidades mapean estados a números reales. ¿Qué números?

Enfoque estándar para evaluar utilidades humanas:
- Comparar un estado dado A con una lotería estándar Lp que tiene:
  - "mejor premio posible" u⊤ con probabilidad p
  - "peor catástrofe posible" u⊥ con probabilidad (1 - p)
- Ajustar la probabilidad de la lotería p hasta que A ∼ Lp

![width:700px](https://mermaid.ink/img/pako:eNpNkDFuwzAMRa9CaHIBO0OWokOHDkWHohcgZTGxUFkyRDpFYPjupaK0BbeP7_H_Ujs0ziU0aNFbZ-CjX4wXcBg-EkJwM1NcaddDQDujtFYY3aKNVr0V8V9jUr0x7Xvwd8qQzorHYJMMkr10Pz9TrY1k_u15bhBH75MkTbOUl9EqWIdDXiRpmuWLF71vmEEjJlgEBf1DLTmRoOtiQ6YTbIzWdoJzUUOAWW0YFV1F3UMLwbA8p_4Yv5Rwca4?type=png)

---

# Escalas de utilidad

- Utilidades normalizadas: u⊤ = 1.0, u⊥ = 0.0
- Micromorts: una probabilidad de un millón de morir
  - Útil para la ruleta rusa, pagar para reducir riesgos de productos, etc.
- AVAC: años de vida ajustados por calidad
  - Útil para decisiones médicas que implican riesgos sustanciales

Nota: el comportamiento es invariante respecto a una transformación lineal positiva
U'(x) = k₁U(x) + k₂ donde k₁ > 0

Con premios determinísticos solamente (sin elecciones de lotería), solo se puede determinar la utilidad ordinal, es decir, el orden total de los premios

---

# Dinero

El dinero no se comporta como una función de utilidad

Dada una lotería L con valor monetario esperado VME(L), usualmente U(L) < U(VME(L)), es decir, las personas son aversas al riesgo

Curva de utilidad: ¿para qué probabilidad p soy indiferente entre un premio x y una lotería [p, $M; (1 - p), $0] para un M grande?

Datos empíricos típicos, extrapolados con comportamiento propenso al riesgo:

![width:600px](https://via.placeholder.com/600x300.png?text=Gráfico+de+Curva+de+Utilidad)

---

# Funciones de Utilidad Multiatributo

¿Cómo podemos manejar funciones de utilidad de muchas variables X₁ ... Xₙ?
Ej., ¿cuál es U(Muertes, Ruido, Costo)?

¿Cómo se pueden evaluar funciones de utilidad complejas a partir del comportamiento de preferencia?

**Idea 1**: Identificar condiciones bajo las cuales se pueden tomar decisiones sin identificar completamente U(x₁, ..., xₙ)

**Idea 2**: Identificar varios tipos de independencia en las preferencias y derivar formas canónicas consecuentes para U(x₁, ..., xₙ)

---

# Dominancia estricta

Típicamente se definen atributos tales que U es monótona en cada uno

Dominancia estricta: la elección B domina estrictamente a la elección A si y solo si
∀i Xᵢ(B) ≥ Xᵢ(A) (y por lo tanto U(B) ≥ U(A))

![width:800px](https://via.placeholder.com/800x400.png?text=Gráficos+de+Dominancia+Estricta)

La dominancia estricta rara vez se da en la práctica

---

# Dominancia estocástica

La distribución p₁ domina estocásticamente a la distribución p₂ si y solo si
∀t ∫ᵗ₋∞ p₁(x)dx ≤ ∫ᵗ₋∞ p₂(x)dx

Si U es monótona en x, entonces A₁ con distribución de resultados p₁ domina estocásticamente a A₂ con distribución de resultados p₂:
∫₋∞∞ p₁(x)U(x)dx ≥ ∫₋∞∞ p₂(x)U(x)dx

Caso multiatributo: dominancia estocástica en todos los atributos ⇒ óptimo

---

# Dominancia estocástica (continuación)

La dominancia estocástica a menudo puede determinarse sin distribuciones exactas usando razonamiento cualitativo

Ejemplos:
1. El costo de construcción aumenta con la distancia desde la ciudad
   S₁ está más cerca de la ciudad que S₂
   ⇒ S₁ domina estocásticamente a S₂ en costo
2. Las lesiones aumentan con la velocidad de colisión

Se pueden anotar redes de creencias con información de dominancia estocástica:
X →⁺ Y (X influye positivamente en Y) significa
Para cada valor z de los otros padres Z de Y
∀x₁, x₂ x₁ ≥ x₂ ⇒ P(Y|x₁, z) domina estocásticamente a P(Y|x₂, z)

---

# Estructura de preferencia: Determinística

X₁ y X₂ son preferencialmente independientes de X₃ si y solo si la preferencia entre (x₁, x₂, x₃) y (x'₁, x'₂, x₃) no depende de x₃

Ejemplo (Ruido, Costo, Seguridad):
(20.000 afectados, $4.600 millones, 0,06 muertes/mpm) vs.
(70.000 afectados, $4.200 millones, 0,06 muertes/mpm)

**Teorema** (Leontief, 1947): Si cada par de atributos es P.I. de su complemento, entonces cada subconjunto de atributos es P.I de su complemento: P.I. mutua

**Teorema** (Debreu, 1960): P.I. mutua ⇒ ∃ función de valor aditiva:
V(S) = ΣᵢVᵢ(Xᵢ(S))

Por lo tanto, evaluar n funciones de atributo único; a menudo es una buena aproximación

---

# Estructura de preferencia: Estocástica

Es necesario considerar preferencias sobre loterías:
X es utilidad-independiente de Y si y solo si las preferencias sobre loterías en X no dependen de y

U.I. mutua: cada subconjunto es U.I de su complemento
⇒ ∃ función de utilidad multiplicativa:
U = k₁U₁ + k₂U₂ + k₃U₃
  + k₁k₂U₁U₂ + k₂k₃U₂U₃ + k₃k₁U₃U₁
  + k₁k₂k₃U₁U₂U₃

Existen procedimientos rutinarios y paquetes de software para generar pruebas de preferencia para identificar varias familias canónicas de funciones de utilidad

---

# Redes de decisión

La red de decisión representa información sobre el estado actual del agente, sus posibles acciones, el estado que resultará de la acción del agente y la utilidad de ese estado.

Se utilizan tres tipos de nodos:
- Nodos de azar (óvalos): variables aleatorias, al igual que en las redes bayesianas
- Nodos de decisión (rectángulos): puntos donde el tomador de decisiones tiene una elección de acciones
- Nodos de utilidad (diamantes): función de utilidad del agente

---

# Redes de decisión

![width:800px](https://via.placeholder.com/800x400.png?text=Red+de+Decisión+para+el+Problema+de+Ubicación+del+Aeropuerto)

Una red de decisión para el problema de ubicación del aeropuerto.

![width:800px](https://via.placeholder.com/800x400.png?text=Red+de+Decisión+Simplificada)

Una representación simplificada del problema de ubicación del aeropuerto. Se han factorizado los nodos de azar correspondientes a los estados de resultado.

---

# Redes de decisión: Algoritmo de Evaluación

1. Establecer las variables de evidencia para el estado actual.
2. Para cada valor posible del nodo de decisión:
   a. Establecer el nodo de decisión a ese valor.
   b. Calcular las probabilidades posteriores para los nodos padres del nodo de utilidad, usando un algoritmo estándar de inferencia probabilística.
   c. Calcular la utilidad resultante para la acción.
3. Devolver la acción con la utilidad más alta.

---

# El Valor de la información

Idea: calcular el valor de adquirir cada posible pieza de evidencia
Se puede hacer directamente desde la red de decisión

Ejemplo: comprar derechos de perforación de petróleo
- Dos bloques A y B, exactamente uno tiene petróleo, vale k
- Probabilidades previas 0.5 cada uno, mutuamente excluyentes
- Precio actual de cada bloque es k/2
- Un "consultor" ofrece un estudio preciso de A. ¿Precio justo?

Solución: calcular el valor esperado de la información
= valor esperado de la mejor acción dada la información
menos el valor esperado de la mejor acción sin información

El estudio puede decir "petróleo en A" o "no hay petróleo en A", prob. 0.5 cada uno (¡dado!)
= [0.5 × valor de "comprar A" dado "petróleo en A"
   + 0.5 × valor de "comprar B" dado "no hay petróleo en A"]
   – 0
= (0.5 × k/2) + (0.5 × k/2) - 0 = k/2

---

# Fórmula general

Evidencia actual E, mejor acción actual α
Posibles resultados de acción Sᵢ, potencial nueva evidencia Eⱼ

EU(α|E) = max_a Σᵢ U(Sᵢ) P(Sᵢ|E, a)

Supongamos que supiéramos Eⱼ = eⱼₖ, entonces elegiríamos αeⱼₖ tal que
EU(αeⱼₖ|E, Eⱼ = eⱼₖ) = max_a Σᵢ U(Sᵢ) P(Sᵢ|E, a, Eⱼ = eⱼₖ)

Eⱼ es una variable aleatoria cuyo valor es actualmente desconocido
⇒ debemos calcular la ganancia esperada sobre todos los valores posibles:

VPI_E(Eⱼ) = Σₖ P(Eⱼ = eⱼₖ|E)EU(αeⱼₖ|E, Eⱼ = eⱼₖ) - EU(α|E)

(VPI = valor de la información perfecta)

---

# Propiedades del VPI

1. No negativo —en expectativa, no post hoc
   ∀j, E VPI_E(Eⱼ) ≥ 0

2. No aditivo —considerar, por ejemplo, obtener Eⱼ dos veces
   VPI_E(Eⱼ, Eₖ) ≠ VPI_E(Eⱼ) + VPI_E(Eₖ)

3. Independiente del orden
   VPI_E(Eⱼ, Eₖ) = VPI_E(Eⱼ) + VPI_E,Eⱼ(Eₖ) = VPI_E(Eₖ) + VPI_E,Eₖ(Eⱼ)

Nota: cuando se puede reunir más de una pieza de evidencia, maximizar el VPI para cada una para seleccionar una no siempre es óptimo
⇒ la recolección de evidencia se convierte en un problema de decisión secuencial

---

# Comportamientos cualitativos

![width:800px](https://via.placeholder.com/800x400.png?text=Gráfico+de+Comportamientos+Cualitativos)

a) La elección es obvia, la información vale poco
b) La elección no es obvia, la información vale mucho
c) La elección no es obvia, la información vale poco

---

# Preferencias desconocidas

Imaginá que estás en una heladería en Tailandia y solo quedan dos sabores: vainilla y durián. Ambos cuestan $2. Sabés que te gusta moderadamente la vainilla y estarías dispuesto a pagar hasta $3 por un helado de vainilla en un día tan caluroso, por lo que hay una ganancia neta de $1 por elegir vainilla. Por otro lado, no tenés idea si te gusta el durián o no, pero leíste en Wikipedia que el durián provoca diferentes respuestas en diferentes personas: algunos encuentran que "supera en sabor a todas las otras frutas del mundo" mientras que otros lo comparan con "aguas residuales, vómito rancio, espray de zorrino y gasas quirúrgicas usadas."

---

# Preferencias desconocidas (continuación)

Digamos que hay un 50% de probabilidad de que lo encuentres sublime (+$100) y un 50% de probabilidad de que lo odies (-$80 si el sabor persiste toda la tarde). Podemos simplemente reemplazar el valor incierto del durián con su ganancia neta esperada a continuación, sin embargo, la decisión seguirá sin cambiar.

(0.5 × $100) - (0.5 × $80) - $2 = $8

En lugar de decir que hay incertidumbre sobre la función de utilidad, movemos esa incertidumbre "al mundo", por así decirlo. Es decir, creamos una nueva variable aleatoria GustaElDurian con probabilidades previas de 0.5 para verdadero y falso en (c)

---

# Preferencias desconocidas: Redes de decisión

![width:800px](https://via.placeholder.com/800x400.png?text=Redes+de+Decisión+para+la+Elección+de+Helado)

(a) Una red de decisión para la elección del helado con una función de utilidad incierta.
(b) La red con la utilidad esperada de cada acción.
(c) Moviendo la incertidumbre de la función de utilidad a una nueva variable aleatoria

---

# Resumen

- La teoría de la probabilidad describe lo que un agente debería creer sobre la base de evidencia, la teoría de la utilidad describe lo que un agente quiere, y la teoría de la decisión combina las dos para describir lo que un agente debería hacer.

- La teoría de la utilidad muestra que un agente cuyas preferencias entre loterías son consistentes con un conjunto de axiomas simples puede ser descrito como poseedor de una función de utilidad

- La teoría de la utilidad multiatributo trata con utilidades que dependen de varios atributos distintos de los estados.

- La dominancia estocástica es una técnica particularmente útil para tomar decisiones inequívocas, incluso sin valores de utilidad precisos para los atributos.

- Las redes de decisión proporcionan un formalismo simple para expresar y resolver problemas de decisión.

- El valor de la información se define como la mejora esperada en la utilidad en comparación con tomar una decisión sin la información

```

Notas sobre la traducción:

1. "Marp": Se mantuvo el término en inglés ya que es un nombre propio para el formato de presentación.
2. "Outline": Se tradujo como "Esquema", que es más común en español para este contexto.
3. "Unknown Preferences": Se tradujo como "Preferencias desconocidas".
4. "Decision networks": Se tradujo como "Redes de decisión".
5. "Utility": Se tradujo como "Utilidad", manteniendo el término técnico en economía y teoría de decisiones.
6. "Multiattribute utility functions": Se tradujo como "Funciones de utilidad multiatributo".
7. "Value of information": Se tradujo como "Valor de la información".
8. "Micromorts" y "QALYs": Se mantuvieron en inglés por ser términos técnicos, pero se proporcionaron traducciones descriptivas (una probabilidad de un millón de morir y años de vida ajustados por calidad, respectivamente).
9. "Stochastic dominance": Se tradujo como "Dominancia estocástica", manteniendo el término técnico en español.
10. "Vos": Se utilizó el pronombre "vos" y sus conjugaciones verbales correspondientes en el ejemplo de la heladería, adaptando el texto al español argentino.

La traducción mantuvo el tono formal y técnico del original, adaptando algunos ejemplos y expresiones al contexto argentino cuando fue posible. Se conservaron los términos técnicos específicos del campo de la inteligencia artificial y la teoría de decisiones.

Aspectos desafiantes de la traducción:

1. La terminología técnica específica de la teoría de decisiones y la inteligencia artificial requirió investigación para asegurar el uso de los términos correctos en español.
2. La adaptación de ejemplos, como el de la heladería, para que suene natural en español argentino mientras se mantiene el significado original.
3. La traducción de fórmulas matemáticas y notación simbólica, asegurando que se mantengan correctas y comprensibles en español.
4. La adaptación de los gráficos y diagramas mencionados en el texto, considerando que los títulos y etiquetas deberían estar en español en una versión final de la presentación.

```