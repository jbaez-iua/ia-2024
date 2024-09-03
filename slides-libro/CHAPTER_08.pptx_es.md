
# Lógica de primer orden
## Capítulo 8

---

# Esquema

- ¿Por qué lógica de primer orden?
- Sintaxis y semántica de la lógica de primer orden
- Divirtiéndose con oraciones
- El mundo de Wumpus en lógica de primer orden
- Ingeniería del conocimiento en lógica de primer orden

---

# Ventajas y desventajas de la lógica proposicional

- Declarativa: las piezas de sintaxis corresponden a hechos
- Permite información parcial/disyuntiva/negada
- Composicional: el significado se deriva de los componentes
- Significado independiente del contexto
- Poder expresivo limitado
  - Por ejemplo, no se puede decir "los pozos causan brisas en los cuadrados adyacentes" excepto escribiendo una oración para cada cuadrado

---

# Lógica de primer orden

Asume que el mundo contiene:

- **Objetos**: personas, casas, números, teorías, colores, juegos, etc.
- **Relaciones**: rojo, redondo, primo, hermano de, más grande que, posee, etc.
- **Funciones**: padre de, mejor amigo, uno más que, fin de, etc.

---

# Lógicas en general

| Lenguaje | Compromiso Ontológico | Compromiso Epistemológico |
|----------|------------------------|----------------------------|
| Lógica proposicional | hechos | verdadero/falso/desconocido |
| Lógica de primer orden | hechos, objetos, relaciones | verdadero/falso/desconocido |
| Lógica temporal | hechos, objetos, relaciones, tiempos | verdadero/falso/desconocido |
| Teoría de la probabilidad | hechos | grado de creencia |
| Lógica difusa | hechos + grado de verdad | valor de intervalo conocido |

---

# Sintaxis de la lógica de primer orden: Elementos básicos

- Constantes: ReyJuan, 2, UCB, ...
- Predicados: Hermano, >, ...
- Funciones: RaizCuadrada, PiernaIzquierdaDe, ...
- Variables: x, y, a, b, ...
- Conectores: ∧ ∨ ¬ ⇒ ⇔
- Igualdad: =
- Cuantificadores: ∀ ∃

---

# Oraciones atómicas

- Oración atómica = predicado(término1, ..., términon) o término1 = término2
- Término = función(término1, ..., términon) o constante o variable

Ejemplos:
- Hermano(ReyJuan, RicardoCorazónDeLeón)
- >(Longitud(PiernaIzquierdaDe(Ricardo)), Longitud(PiernaIzquierdaDe(ReyJuan)))

---

# Oraciones complejas

Formadas a partir de oraciones atómicas usando conectores:
¬S, S1 ∧ S2, S1 ∨ S2, S1 ⇒ S2, S1 ⇔ S2

Ejemplos:
- Hermano(ReyJuan, Ricardo) ⇒ Hermano(Ricardo, ReyJuan)
- >(1, 2) ∨ ≤(1, 2)
- >(1, 2) ∧ ¬>(1, 2)

---

# Verdad en lógica de primer orden

- Las oraciones son verdaderas con respecto a un modelo y una interpretación
- El modelo contiene ≥ 1 objetos (elementos del dominio) y relaciones entre ellos
- La interpretación especifica referentes para:
  - símbolos constantes → objetos
  - símbolos de predicados → relaciones
  - símbolos de funciones → relaciones funcionales

---

# Modelos para lógica de primer orden: Ejemplo

![Ejemplo de Modelo](https://i.imgur.com/example.png)

---

# Ejemplo de verdad

Considerá la interpretación:
- Ricardo → Ricardo Corazón de León
- Juan → el malvado Rey Juan
- Hermano → la relación de hermandad

Bajo esta interpretación, Hermano(Ricardo, Juan) es verdadera si y solo si Ricardo Corazón de León y el malvado Rey Juan están en la relación de hermandad en el modelo.

---

# Modelos para lógica de primer orden: ¡Muchos!

Enumerando modelos de lógica de primer orden para un vocabulario de BC dado:
1. Para cada número de elementos de dominio n de 1 a ∞
2. Para cada predicado k-ario Pk en el vocabulario
3. Para cada posible relación k-aria en n objetos
4. Para cada símbolo constante C en el vocabulario
5. Para cada elección de referente para C de n objetos ...

¡Calcular la implicación lógica enumerando modelos de lógica de primer orden no es fácil!

---

# Cuantificación universal

∀ variables oración

Ejemplo: Todos en Berkeley son inteligentes:
∀x En(x, Berkeley) ⇒ Inteligente(x)

∀x P es verdadero en un modelo m si y solo si P es verdadero con x siendo cada objeto posible en el modelo

---

# Un error común a evitar

Típicamente, ⇒ es el conector principal con ∀

Error común: usar ∧ como el conector principal con ∀:
∀x En(x, Berkeley) ∧ Inteligente(x)

Esto significa "Todos están en Berkeley y todos son inteligentes"

---

# Cuantificación existencial

∃ variables oración

Ejemplo: Alguien en Stanford es inteligente:
∃x En(x, Stanford) ∧ Inteligente(x)

∃x P es verdadero en un modelo m si y solo si P es verdadero con x siendo algún objeto posible en el modelo

---

# Otro error común a evitar

Típicamente, ∧ es el conector principal con ∃

Error común: usar ⇒ como el conector principal con ∃:
∃x En(x, Stanford) ⇒ Inteligente(x)

¡Esto es verdadero si hay alguien que no está en Stanford!

---

# Propiedades de los cuantificadores

- ∀x ∀y es lo mismo que ∀y ∀x
- ∃x ∃y es lo mismo que ∃y ∃x
- ∃x ∀y no es lo mismo que ∀y ∃x

Dualidad de cuantificadores: cada uno puede ser expresado usando el otro
- ∀x LeGusta(x, Helado) ⇔ ¬∃x ¬LeGusta(x, Helado)
- ∃x LeGusta(x, Brócoli) ⇔ ¬∀x ¬LeGusta(x, Brócoli)

---

# Diversión con oraciones

1. Los hermanos son hermanos
   ∀x,y Hermano(x,y) ⇒ Hermano(x,y)

2. "Hermano" es simétrico
   ∀x,y Hermano(x,y) ⇔ Hermano(y,x)

3. La madre de uno es el progenitor femenino de uno
   ∀x,y Madre(x,y) ⇔ (Femenino(x) ∧ Progenitor(x,y))

4. Un primo hermano es un hijo del hermano de un progenitor
   ∀x,y PrimoHermano(x,y) ⇔ ∃p,ps Progenitor(p,x) ∧ Hermano(ps,p) ∧ Progenitor(ps,y)

---

# Igualdad

término1 = término2 es verdadero bajo una interpretación dada si y solo si término1 y término2 se refieren al mismo objeto

Ejemplo: Definición de Hermano (completo) en términos de Progenitor:
∀x,y Hermano(x,y) ⇔ [¬(x = y) ∧ ∃m,f ¬(m = f) ∧ Progenitor(m,x) ∧ Progenitor(f,x) ∧ Progenitor(m,y) ∧ Progenitor(f,y)]

---

# Interactuando con BCs de lógica de primer orden

Ejemplo: Agente del mundo de Wumpus usando una BC de lógica de primer orden

Decir(BC, Percepción([Olor, Brisa, Ninguno], 5))
Preguntar(BC, ∃a Acción(a, 5))

Dada una oración S y una sustitución σ, Sσ denota el resultado de enchufar σ en S

Preguntar(BC, S) devuelve alguna/todas las σ tales que BC |= Sσ

---

# Base de conocimientos para el mundo de Wumpus

"Percepción":
∀b,g,t Percepción([Olor, b, g], t) ⇒ Olió(t)
∀s,b,t Percepción([s, b, Brillo], t) ⇒ EnOro(t)

Reflejo:
∀t EnOro(t) ⇒ Acción(Agarrar, t)

Reflejo con estado interno:
∀t EnOro(t) ∧ ¬Sosteniendo(Oro, t) ⇒ Acción(Agarrar, t)

---

# Deduciendo propiedades ocultas

Propiedades de las ubicaciones:
∀x,t En(Agente, x, t) ∧ Olió(t) ⇒ Maloliente(x)
∀x,t En(Agente, x, t) ∧ Brisa(t) ⇒ Ventoso(x)

Los cuadrados son ventosos cerca de un pozo:
∀y Ventoso(y) ⇒ ∃x Pozo(x) ∧ Adyacente(x, y)
∀x,y Pozo(x) ∧ Adyacente(x, y) ⇒ Ventoso(y)

Definición para el predicado Ventoso:
∀y Ventoso(y) ⇔ [∃x Pozo(x) ∧ Adyacente(x, y)]

---

# Manteniendo un registro del cambio

- Los hechos se mantienen en situaciones, en lugar de eternamente
- El cálculo situacional es una forma de representar el cambio en lógica de primer orden
- Agrega un argumento de situación a cada predicado no eterno
- Las situaciones están conectadas por la función Resultado

---

# Describiendo acciones I

Axioma de "efecto":
∀s EnOro(s) ⇒ Sosteniendo(Oro, Resultado(Agarrar, s))

Axioma de "marco":
∀s TieneFlecha(s) ⇒ TieneFlecha(Resultado(Agarrar, s))

Desafíos:
- Problema del marco
- Problema de la calificación
- Problema de la ramificación

---

# Describiendo acciones II

Los axiomas de estado sucesor resuelven el problema del marco representacional:

∀a,s Sosteniendo(Oro, Resultado(a, s))
⇔
[(a = Agarrar ∧ EnOro(s))
∨ (Sosteniendo(Oro, s) ∧ a ≠ Soltar)]

---

# Haciendo planes

Condición inicial en BC:
En(Agente, [1, 1], S0)
En(Oro, [1, 2], S0)

Consulta:
Preguntar(BC, ∃s Sosteniendo(Oro, s))

Respuesta:
{s/Resultado(Agarrar, Resultado(Avanzar, S0))}

---

# Haciendo planes: Una mejor manera

Representar planes como secuencias de acciones [a1, a2, ..., an]

ResultadoPlan(p, s) es el resultado de ejecutar p en s

Consulta:
Preguntar(BC, ∃p Sosteniendo(Oro, ResultadoPlan(p, S0)))

Solución:
{p/[Avanzar, Agarrar]}

---

# Ingeniería del conocimiento en lógica de primer orden

Pasos en el proceso de ingeniería del conocimiento:
1. Identificar las preguntas
2. Reunir el conocimiento relevante
3. Decidir sobre un vocabulario de predicados, funciones y constantes
4. Codificar el conocimiento general sobre el dominio
5. Codificar una descripción de la instancia del problema
6. Plantear consultas al procedimiento de inferencia y obtener respuestas
7. Depurar y evaluar la base de conocimientos

---

# Resumen

- Lógica de primer orden:
  - Objetos y relaciones son primitivas semánticas
  - Sintaxis: constantes, funciones, predicados, igualdad, cuantificadores
- Mayor poder expresivo: suficiente para definir el mundo de Wumpus
- Cálculo situacional para describir acciones y cambios
- Desarrollar una BC en lógica de primer orden requiere un análisis y codificación cuidadosos

```

## Notas sobre la traducción

1. "Wumpus world" se mantuvo como "mundo de Wumpus", ya que es un nombre propio en el contexto de inteligencia artificial.
2. Se utilizó "vos" implícito en las instrucciones, como en "Considerá la interpretación".
3. Se tradujeron términos técnicos cuando existe una versión aceptada en español, como "lógica de primer orden" para "first-order logic".
4. Se mantuvieron algunos términos en inglés cuando son comúnmente usados así en el ámbito académico argentino, como "frame problem".
5. Se usaron expresiones más comunes en Argentina, como "BC" para "base de conocimientos" en lugar de "KB".

## Aspectos desafiantes de la traducción

1. La traducción de términos técnicos específicos de lógica e inteligencia artificial requirió un equilibrio entre la precisión técnica y la comprensión en el contexto argentino.
2. Mantener la consistencia en la traducción de términos a lo largo del documento, especialmente en ejemplos y definiciones formales, fue un desafío importante.
3. Adaptar ejemplos culturalmente específicos (como referencias a universidades estadounidenses) sin perder el sentido original del texto requirió cuidado y consideración.
4. La traducción de fórmulas lógicas y notaciones matemáticas necesitó atención especial para asegurar que mantuvieran su significado preciso en el contexto de la lógica de primer orden.