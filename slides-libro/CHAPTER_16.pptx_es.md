
---
marp: true
theme: default
paginate: true
---

<!-- _class: lead -->
# Toma de Decisiones Complejas
## Capítulo 16

---

# Esquema

- Problemas de Decisión Secuencial
- Notación Básica de Probabilidad
- Problemas de Bandidos
- POMDPs (Procesos de Decisión de Markov Parcialmente Observables)
- Algoritmos para Resolver POMDPs

---

# Problemas de Decisión Secuencial

- Proceso de decisión de Markov (MDP): problema de decisión secuencial para un entorno estocástico completamente observable
- Un MDP consiste en:
  - un conjunto de estados (con un estado inicial s0)
  - un conjunto ACCIONES(s) de acciones en cada estado
  - un modelo de transición P(s' | s, a)
  - una función de recompensa R(s, a, s')

- Las soluciones de MDP generalmente involucran programación dinámica
- Una solución se llama política π
- Política óptima: utilidad esperada más alta

---

# Problemas de Decisión Secuencial: Ejemplo

![bg right:60% 80%](https://i.imgur.com/xKYd9Dj.png)

a) Un entorno estocástico simple de 4×3
b) Ilustración del modelo de transición:
   - Resultado previsto: probabilidad de 0,8
   - Movimiento en ángulo recto: probabilidad de 0,2
   - Colisión con la pared: sin movimiento
   - Estados terminales: recompensa +1 y –1
   - Otras transiciones: recompensa –0,04

---

# Utilidades a lo Largo del Tiempo

![bg right:50% 80%](https://i.imgur.com/XYZ1234.png)

- Utilidades: Uh([s0, a0, s1, a1 . . . , sn])
- Políticas óptimas para diferentes rangos de r
- (a) r = 0,04 para transiciones entre estados no terminales
- (b) Políticas óptimas para cuatro rangos diferentes de r

---

# Horizontes Temporales

- Horizonte finito: tiempo fijo N después del cual nada importa
  - Uh([s₀, a₀, s₁, a₁, . . . , sN₊k]) = Uh([s₀, a₀, s₁, a₁, . . . , sN])
  - La acción óptima puede depender del tiempo restante
  - Política no estacionaria

- Horizonte infinito: sin límite de tiempo fijo
  - La acción óptima depende solo del estado actual
  - Política estacionaria

---

# Recompensas Aditivas con Descuento

Uh([s0, a0, s1, a1, s2, . . .]) = R(s0, a0, s1) + γR(s1, a1, s2) + γ²R(s2, a2, s3) + · · ·

- γ: factor de descuento (0 < γ < 1)
- γ cercano a 0: no dispuesto a esperar
- γ cercano a 1: dispuesto a esperar por recompensa a largo plazo

Beneficios:
1. Sentido empírico y económico
2. Tiene en cuenta la incertidumbre sobre las recompensas verdaderas
3. Expresa preferencias sobre historias
4. Reduce la complejidad de secuencias infinitas

---

# Ecuación de Bellman y Función Q

- Ecuación de Bellman:
  U(s) = max[R(s, a, s') + γU(s')]
        a

- Función Q (Función de utilidad de acción):
  Q(s, a) = utilidad esperada de tomar la acción a en el estado s

- Relación con las utilidades:
  U(s) = max Q(s, a)
        a

- La política óptima se puede extraer de la función Q

---

# Ejemplo: Utilidades del Mundo 4×3

![bg right:50% 80%](https://i.imgur.com/ABCD5678.png)

Utilidades de los estados en el mundo 4×3:
- γ = 1
- r = -0,04 para transiciones no terminales

Ejemplo de cálculo para U(1,1):
```
max { [0,8(-0,04 + γU(1,2)) + 0,1(-0,04 + γU(2,1)) + 0,1(-0,04 + γU(1,1))],
      [0,9(-0,04 + γU(1,1)) + 0,1(-0,04 + γU(1,2))],
      [0,9(-0,04 + γU(1,1)) + 0,1(-0,04 + γU(2,1))],
      [0,8(-0,04 + γU(2,1)) + 0,1(-0,04 + γU(1,2)) + 0,1(-0,04 + γU(1,1))] }
```

---

# Escalas de Recompensa y Funciones Potenciales

- Transformación de recompensas:
  R'(s, a, s') = mR(s, a, s') + b

- Función potencial Φ(s):
  R'(s, a, s') = R(s, a, s') + γΦ(s') - Φ(s)

- Un Φ(s) más alto en estados de mayor utilidad lleva al agente "cuesta arriba" en utilidad

---

# Representación de MDPs: Redes de Decisión Dinámicas

![bg right:60% 80%](https://i.imgur.com/EFGH9012.png)

Red de Decisión Dinámica (DDN) para un robot móvil:
- Variables de estado:
  - Nivel de batería
  - Estado de carga
  - Ubicación
  - Velocidad
- Variables de acción:
  - Motor de rueda izquierda
  - Motor de rueda derecha
  - Carga

---

# Representación de MDPs: Ejemplo de Tetris

![bg right:60% 80%](https://i.imgur.com/IJKL3456.png)

a) Juego de Tetris
b) DDN para MDP de Tetris

---

# Algoritmo de Iteración de Valor

```python
función ITERACION-DE-VALOR(mdp, ε) devuelve una función de utilidad
    entradas: mdp, un MDP con estados S, acciones A(s), modelo de transición P(s'|s,a),
                   recompensas R(s,a,s'), descuento γ
              ε, el error máximo permitido en la utilidad de cualquier estado
    variables locales: U, U', vectores de utilidades para estados en S, inicialmente cero
                       δ, el cambio máximo en la utilidad de cualquier estado en una iteración

    repetir
        U ← U'
        δ ← 0
        para cada estado s en S hacer
            U'[s] ← max R(s,a,s') + γ Σ P(s'|s,a) U[s']
                   a       s'
            si |U'[s] - U[s]| > δ entonces δ ← |U'[s] - U[s]|
    hasta que δ < ε(1-γ)/γ
    devolver U
```

---

# Iteración de Valor: Ejemplo del Mundo 4×3

![bg right:50% 80%](https://i.imgur.com/MNOP7890.png)

(a) Evolución de utilidades para estados seleccionados
(b) Número de iteraciones requeridas para error ≤ ε = cRmax

---

# Algoritmo de Iteración de Política

```python
función ITERACION-DE-POLITICA(mdp) devuelve una política
    entradas: mdp, un MDP con estados S, acciones A(s), modelo de transición P(s'|s,a)
    variables locales: U, un vector de utilidades para estados en S, inicialmente cero
                       π, un vector de política indexado por estado, inicialmente aleatorio

    repetir
        U ← EVALUACION-DE-POLITICA(π, U, mdp)
        sin_cambios? ← verdadero
        para cada estado s en S hacer
            si max R(s,a,s') + γ Σ P(s'|s,a) U[s'] > Σ P(s'|s,π[s]) U[s'] entonces
               a       s'                    s'
                π[s] ← argmax R(s,a,s') + γ Σ P(s'|s,a) U[s']
                        a       s'
                sin_cambios? ← falso
    hasta que sin_cambios?
    devolver π
```

---

# Programación Lineal para MDPs

- Minimizar U(s) para todo s
- Sujeto a restricciones:
  U(s) ≥ R(s,a,s') + γ Σ P(s'|s,a) U[s'] para todo s, a
                       s'

- Eficiente para espacios de estados pequeños
- A menudo menos eficiente que la programación dinámica para MDPs grandes

---

# Algoritmos en Línea: EXPECTIMAX

![bg right:60% 80%](https://i.imgur.com/QRST5678.png)

Árbol EXPECTIMAX para MDP 4×3:
- Nodos triangulares: nodos max
- Nodos circulares: nodos de azar
- Evalúa hojas no terminales
- Respalda valores de utilidad
- Extrae decisiones del árbol

---

# Problemas de Bandidos

- Bandido de n brazos: máquina tragamonedas con n palancas
- Cada palanca tiene una distribución de probabilidad desconocida de ganancias
- Compensación: explotación vs. exploración
- Aplicaciones:
  - Tratamientos médicos
  - Estrategias de inversión
  - Asignación de fondos de investigación

---

# Problemas de Bandidos: Modelo Formal

- Cada brazo Mi es un Proceso de Recompensa de Markov (MRP)
- El problema general del bandido es un MDP:
  - Espacio de estados: S = S1 × ... × Sn
  - Acciones: a1, ..., an
  - Modelo de transición: actualiza el estado del brazo seleccionado
  - Factor de descuento: γ

Propiedad clave: los brazos son independientes

---

# Problemas de Bandidos: Ejemplo

![bg right:60% 80%](https://i.imgur.com/UVWX9012.png)

(a) Bandido determinista simple con dos brazos
(b) Caso general: el primer brazo da una secuencia arbitraria, el segundo brazo da una recompensa fija λ

---

# Índice de Gittins

- Describe la máxima utilidad obtenible por unidad de tiempo descontado
- Estrategia óptima: ejecutar el brazo M hasta el tiempo T, luego cambiar a Mλ

---

# Bandido de Bernoulli

![bg right:50% 80%](https://i.imgur.com/YZAB3456.png)

- El problema de bandido más simple
- Cada brazo Mi produce 0 o 1 con probabilidad fija desconocida μi
- El estado del brazo Mi se define por si y fi (conteos de éxitos y fracasos)
- (a) Estados, recompensas y probabilidades de transición
- (b) Índices de Gittins para estados

---

# POMDPs (Procesos de Decisión de Markov Parcialmente Observables)

- Extensión de MDPs con modelo de sensor P(e|s)
- Representación compacta usando Redes de Decisión Dinámicas
- Ciclo de decisión de un agente POMDP:
  1. Ejecutar acción a = π*(b) dado el estado de creencia actual b
  2. Observar percepción e
  3. Actualizar estado de creencia: b' = AVANZAR(b, a, e)
  4. Repetir

---

# POMDPs como MDPs Observables

P(b'|b, a) y ρ(b, a) definen un MDP observable en el espacio de estados de creencia

---

# Algoritmo de Iteración de Valor para POMDPs

```python
función ITERACION-DE-VALOR(pomdp, ε) devuelve una función de utilidad
    entradas: pomdp, un POMDP con estados S, acciones A(s), modelo de transición P(s'|s,a),
                     modelo de sensor P(e|s), recompensas R(s,a,s'), descuento γ
              ε, el error máximo permitido en la utilidad de cualquier estado
    variables locales: U, U', conjuntos de planes p con vectores de utilidad asociados αp

    U' ← { un plan p con una sola acción para cada a, con
           αp(b) = ρ(b,a) para todo b }
    repetir
        U ← U'
        U' ← ACTUALIZACION-POMDP(U)
        U' ← ELIMINAR-PLANES-DOMINADOS(U')
    hasta que DIFERENCIA-MAXIMA(U, U') < ε(1-γ)/γ
    devolver U
```

---

# Iteración de Valor para POMDP: Ejemplo

![bg right:60% 80%](https://i.imgur.com/CDEF7890.png)

(a) Utilidad de dos planes de un paso
(b) Utilidades para 8 planes distintos de dos pasos
(c) Utilidades para cuatro planes no dominados de dos pasos
(d) Función de utilidad para planes óptimos de ocho pasos

---

# Algoritmos en Línea para POMDPs

1. Comenzar con el estado de creencia previo
2. Elegir acción basada en el estado de creencia actual
3. Recibir observación y actualizar estado de creencia
4. Repetir

Enfoques:
- Algoritmo EXPECTIMAX (usando estados de creencia)
- Planificación Monte Carlo Parcialmente Observable (POMCP)

![bg right:40% 80%](https://i.imgur.com/GHIJ1234.png)

---

<!-- _class: lead -->
# Resumen

- MDPs: problemas de decisión secuencial en entornos estocásticos
- Solución: política que asocia decisiones con estados
- Iteración de valor: resuelve iterativamente ecuaciones que relacionan utilidades de estados
- Iteración de política: alterna entre cálculo de utilidad y mejora de política
- POMDPs: más difíciles de resolver que los MDPs
- Varios algoritmos para resolver POMDPs, incluyendo enfoques en línea

```

## Notas sobre la traducción

1. "Vos" form: En esta traducción, se mantuvo un tono formal y profesional, por lo que no se utilizó la forma "vos" característica del español argentino. En un contexto académico o técnico, es común mantener un lenguaje más neutro.

2. Términos técnicos: Se mantuvieron en su forma original en inglés términos como "MDP", "POMDP", "EXPECTIMAX" y "Monte Carlo", ya que son ampliamente reconocidos en la comunidad académica y técnica argentina.

3. "Bandido de n brazos": Se tradujo literalmente "n-armed bandit" como "bandido de n brazos", que es el término utilizado en la literatura académica en español.

4. "Tragamonedas": Se utilizó este término para "slot machine", que es el más común en Argentina.

5. "Palanca": Se usó este término para "lever", que es más común en Argentina que "palanca" en este contexto.

6. "Compensación": Se utilizó este término para "tradeoff", que es una traducción aceptada en contextos técnicos y académicos en Argentina.

## Aspectos desafiantes de la traducción

1. Mantenimiento del balance entre precisión técnica y accesibilidad: Fue necesario mantener términos técnicos en inglés mientras se aseguraba que el texto fuera comprensible para un público académico argentino.

2. Adaptación de ejemplos numéricos: Los números decimales se escribieron con coma en lugar de punto (por ejemplo, 0,8 en lugar de 0.8), siguiendo la convención argentina.

3. Traducción de algoritmos: Se tradujeron los nombres de funciones y variables en los pseudocódigos para mayor claridad, manteniendo la estructura y la lógica originales.

4. Conservación del formato Marp: Se aseguró que la estructura de la presentación y las directivas Marp se mantuvieran intactas durante la traducción.

5. Adaptación de conceptos sin equivalente directo: Algunos conceptos, como "Gittins Index", no tienen una traducción establecida en español. En estos casos, se optó por una traducción literal ("Índice de Gittins") y se mantuvo el contexto para su comprensión.