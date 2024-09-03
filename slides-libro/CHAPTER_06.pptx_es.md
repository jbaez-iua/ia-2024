
# Búsqueda Adversarial y Juegos
## Capítulo 6

---

# Esquema

- Teoría de juegos
- Decisiones óptimas en juegos
  - decisiones minimax
  - poda α–β
  - Búsqueda de árbol Monte Carlo (MCTS)
- Límites de recursos y evaluación aproximada
- Juegos de azar
- Juegos de información imperfecta
- Limitaciones de los algoritmos de búsqueda en juegos

---

# Teoría de Juegos

- Dos jugadores
  - Max-min
  - Por turnos, totalmente observable
- Movimientos: Acción
- Posición: estado
- Suma cero:
  - lo que es bueno para un jugador, es malo para el otro
  - No hay resultado donde ambos ganen

---

# Componentes de la Teoría de Juegos

- S0: El estado inicial del juego
- TO-MOVE(s): jugador que se mueve en el estado s
- ACTIONS(s): El conjunto de movimientos legales en el estado s
- RESULT(s, a): El modelo de transición, estado resultante
- IS-TERMINAL(s): Una prueba terminal para detectar cuando el juego ha terminado
- UTILITY(s; p): Una función de utilidad (objetivo/recompensa)

---

# Juegos vs. Problemas de Búsqueda

- Oponente "impredecible" ⇒ la solución es una estrategia que especifica un movimiento para cada posible respuesta del oponente
- Límites de tiempo ⇒ es poco probable encontrar el objetivo, se debe aproximar

Plan de ataque:
1. La computadora considera posibles líneas de juego (Babbage, 1846)
2. Algoritmo para juego perfecto (Zermelo, 1912; Von Neumann, 1944)
3. Horizonte finito, evaluación aproximada (Zuse, 1945; Wiener, 1948; Shannon, 1950)
4. Primer programa de ajedrez (Turing, 1951)
5. Aprendizaje automático para mejorar la precisión de la evaluación (Samuel, 1952–57)
6. Poda para permitir una búsqueda más profunda (McCarthy, 1956)

---

# Tipos de Juegos

|                     | Información Perfecta | Información Imperfecta |
|---------------------|---------------------|------------------------|
| **Determinístico**   | ajedrez, damas, go, othello | batalla naval, ta-te-ti ciego |
| **Azar**          | backgammon, monopoly | bridge, póker, scrabble, guerra nuclear |

---

# Árbol de Juego (2 jugadores, determinístico, por turnos)

![Árbol de Juego](https://mermaid.ink/img/pako:eNptkc1qwzAQhF9F7CmFvoDPgZCQQ3NoDm1CKZQ9yPLGFrEkI8mNQ8i7V7JCnNQVErszs_NjWbPUTLHkmZpqNAGGUL8ZLsAvwV1egArnsK5-kWIL72ggHiwah_UvfIBe5xZHsOTQANmReqOIvlGqGsVDQ2ONJ5IXMTSO9FTIxJKH3rh1AE9OKCIwyqLx4H6oVWz8sP1Mzpq7UiT7wQ15HCyedFhHdD_UKNtv6I0aRyUOx8Ql-92znmtecM3PhhqLs7LcF7-Tj_c8L9PBs9LWNxdLsSnzIi-KQk7fXu8zXjZ8wdMnGxXTK9QmPBGnnexOUJPbTJb-f-Pnda5fORvMQJr3LJunoJJfslTOd7JF9hW8ZmkwBHQ6TbZ4Xyx4Jh3aaa7DRJLOF5otL8nyjw?type=png)

---

# Minimax

Juego perfecto para juegos determinísticos de información perfecta

Idea: elegir el movimiento hacia la posición con el valor minimax más alto = mejor recompensa alcanzable contra el mejor juego

Ejemplo: juego de 2 niveles:

![Ejemplo de Minimax](https://mermaid.ink/img/pako:eNptkc1qwzAQhF9F7CmFvoDPgZCQQ3NoDm1CKZQ9yPLGFrEkI8mNQ8i7V7JCnNQVErszs_NjWbPUTLHkmZpqNAGGUL8ZLsAvwV1egArnsK5-kWIL72ggHiwah_UvfIBe5xZHsOTQANmReqOIvlGqGsVDQ2ONJ5IXMTSO9FTIxJKH3rh1AE9OKCIwyqLx4H6oVWz8sP1Mzpq7UiT7wQ15HCyedFhHdD_UKNtv6I0aRyUOx8Ql-92znmtecM3PhhqLs7LcF7-Tj_c8L9PBs9LWNxdLsSnzIi-KQk7fXu8zXjZ8wdMnGxXTK9QmPBGnnexOUJPbTJb-f-Pnda5fORvMQJr3LJunoJJfslTOd7JF9hW8ZmkwBHQ6TbZ4Xyx4Jh3aaa7DRJLOF5otL8nyjw?type=png)

---

# Algoritmo Minimax

```python
function Minimax-Decision(estado) devuelve una acción
    devolver la a en Actions(estado) que maximiza Min-Value(Result(a, estado))

function Max-Value(estado) devuelve un valor de utilidad
    si Terminal-Test(estado) entonces devolver Utility(estado)
    v ← -∞
    para a, s en Successors(estado) hacer
        v ← Max(v, Min-Value(s))
    devolver v

function Min-Value(estado) devuelve un valor de utilidad
    si Terminal-Test(estado) entonces devolver Utility(estado)
    v ← ∞
    para a, s en Successors(estado) hacer
        v ← Min(v, Max-Value(s))
    devolver v
```

---

# Propiedades de Minimax

- Completo: Sí, si el árbol es finito
- Óptimo: Sí, contra un oponente óptimo
- Complejidad temporal: O(b^m)
- Complejidad espacial: O(bm) (exploración en profundidad)

Para el ajedrez, b ≈ 35, m ≈ 100 para juegos "razonables"
⇒ la solución exacta es completamente inviable

Pero, ¿necesitamos explorar cada camino?

---

# Ejemplo de Poda α–β

![Poda α–β](https://mermaid.ink/img/pako:eNptkctqwzAQRX9F3FUKfYGXgZCQRbNoFm1CKZQuZHlii1iSkeTGIeTfK1khTuoKid07c-fBWLPUTLHkmZpqNAGGUL8ZLsAvwV1egArnsK5-kWIL72ggHiwah_UvfIBe5xZHsOTQANmReqOIvlGqGsVDQ2ONJ5IXMTSO9FTIxJKH3rh1AE9OKCIwyqLx4H6oVWz8sP1Mzpq7UiT7wQ15HCyedFhHdD_UKNtv6I0aRyUOx8Ql-92znmtecM3PhhqLs7LcF7-Tj_c8L9PBs9LWNxdLsSnzIi-KQk7fXu8zXjZ8wdMnGxXTK9QmPBGnnexOUJPbTJb-f-Pnda5fORvMQJr3LJunoJJfslTOd7JF9hW8ZmkwBHQ6TbZ4Xyx4Jh3aaa7DRJLOF5otL8nyjw?type=png)

---

# El Algoritmo α–β

```python
function Alpha-Beta-Decision(estado) devuelve una acción
    devolver la a en Actions(estado) que maximiza Min-Value(Result(a, estado))

function Max-Value(estado, α, β) devuelve un valor de utilidad
    si Terminal-Test(estado) entonces devolver Utility(estado)
    v ← -∞
    para a, s en Successors(estado) hacer
        v ← Max(v, Min-Value(s, α, β))
        si v ≥ β entonces devolver v
        α ← Max(α, v)
    devolver v

function Min-Value(estado, α, β) devuelve un valor de utilidad
    # Igual que Max-Value pero con los roles de α, β invertidos
```

---

# Propiedades de α–β

- La poda no afecta el resultado final
- Un buen ordenamiento de movimientos mejora la efectividad de la poda
- Con un "ordenamiento perfecto", la complejidad temporal = O(b^(m/2))
  ⇒ duplica la profundidad solucionable
- Un ejemplo simple del valor de razonar sobre qué cálculos son relevantes (una forma de metarrazonamiento)
- Desafortunadamente, 35^50 sigue siendo imposible!

---

# Búsqueda de Árbol Monte Carlo (MCTS)

La estrategia básica de MCTS no utiliza una función de evaluación heurística. El valor de un estado se estima como la utilidad promedio sobre un número de simulaciones.

Conceptos clave:
- Playout: simulación que elige movimientos hasta alcanzar una posición terminal
- Selección: Comienza en la raíz, elige un movimiento (política de selección) repetidamente bajando por el árbol
- Expansión: El árbol de búsqueda crece generando un nuevo hijo del nodo seleccionado
- Simulación: playout desde el nodo hijo generado
- Retropropagación: usa el resultado de la simulación para actualizar todos los nodos del árbol de búsqueda subiendo hasta la raíz

---

# Búsqueda de Árbol Monte Carlo: UCT

UCT: Política de selección efectiva llamada "límites de confianza superiores aplicados a árboles"

UCT clasifica cada movimiento posible basándose en una fórmula de límite de confianza superior llamada UCB1:

![Fórmula UCT](https://latex.codecogs.com/png.latex?UCT%28n%29%20%3D%20%5Cfrac%7BU%28n%29%7D%7BN%28n%29%7D%20&plus;%20C%20%5Csqrt%7B%5Cfrac%7B%5Clog%20N%28PARENT%28n%29%29%7D%7BN%28n%29%7D%7D)

donde U(n) es la utilidad total de todos los playouts que pasaron por el nodo n, N(n) es el número de playouts a través del nodo n, y PARENT(n) es el nodo padre de n en el árbol.

---

# Algoritmo de Búsqueda de Árbol Monte Carlo

```python
función MONTE-CARLO-TREE-SEARCH(estado) devuelve una acción
    árbol ← NODE(estado)
    mientras IS-TIME-REMAINING() hacer
        hoja ← SELECT(árbol)
        hijo ← EXPAND(hoja)
        resultado ← SIMULATE(hijo)
        BACK-PROPAGATE(resultado, hijo)
    devolver el movimiento en ACTIONS(estado) cuyo nodo tiene el mayor número de playouts
```

---

# Límites de Recursos

Enfoque estándar:
- Usar Cutoff-Test en lugar de Terminal-Test
  por ejemplo, límite de profundidad (tal vez agregar búsqueda de quiescencia)
- Usar Eval en lugar de Utility
  es decir, función de evaluación que estima la deseabilidad de la posición

Supongamos que tenemos 100 segundos, exploramos 10^4 nodos/segundo
⇒ 10^6 nodos por movimiento ≈ 35^8 / 2
⇒ α–β alcanza profundidad 8 ⇒ programa de ajedrez bastante bueno

---

# Funciones de Evaluación

![Posiciones de Ajedrez](https://example.com/chess_positions.png)

Para el ajedrez, típicamente suma lineal ponderada de características:
Eval(s) = w1f1(s) + w2f2(s) + ... + wnfn(s)

por ejemplo, w1 = 9 con
f1(s) = (número de reinas blancas) – (número de reinas negras), etc.

---

# Juegos Determinísticos en la Práctica

- Damas: Chinook terminó con el reinado de 40 años del campeón mundial humano Marion Tinsley en 1994.
- Ajedrez: Deep Blue derrotó al campeón mundial humano Gary Kasparov en un match de seis partidas en 1997.
- Othello: Los campeones humanos se niegan a competir contra computadoras, que son demasiado buenas.
- Go: AlphaGo y sus sucesores han superado a los campeones humanos.

---

# Juegos No Determinísticos: Backgammon

![Tablero de Backgammon](https://example.com/backgammon_board.png)

---

# Algoritmo para Juegos No Determinísticos

Expectiminimax da un juego perfecto:

```python
si el estado es un nodo Max entonces
    devolver el valor ExpectiMinimax más alto de Successors(estado)
si el estado es un nodo Min entonces
    devolver el valor ExpectiMinimax más bajo de Successors(estado)
si el estado es un nodo de azar entonces
    devolver el promedio del valor ExpectiMinimax de Successors(estado)
```

---

# Juegos No Determinísticos en la Práctica

- Las tiradas de dados aumentan b: 21 tiradas posibles con 2 dados
- Backgammon ≈ 20 movimientos legales (pueden ser 6.000 con una tirada de 1-1)
- A medida que aumenta la profundidad, la probabilidad de alcanzar un nodo dado disminuye
  ⇒ el valor de la anticipación se reduce
- La poda α–β es mucho menos efectiva
- TDGammon usa búsqueda de profundidad 2 + muy buena Eval ≈ nivel de campeón mundial

---

# Juegos de Información Imperfecta

- Por ejemplo, juegos de cartas, donde las cartas iniciales del oponente son desconocidas
- Típicamente podemos calcular una probabilidad para cada reparto posible
- Idea: calcular el valor minimax de cada acción en cada reparto, luego elegir la acción con el valor esperado más alto sobre todos los repartos
- Caso especial: si una acción es óptima para todos los repartos, es óptima
- GIB (programa de bridge) aproxima esta idea:
  1. Generando 100 repartos consistentes con la información de la subasta
  2. Eligiendo la acción que gana más bazas en promedio

---

# Análisis Adecuado de Juegos de Información Imperfecta

- La intuición de que el valor de una acción es el promedio de sus valores en todos los estados reales es INCORRECTA
- Con observabilidad parcial, el valor de una acción depende del estado de información o estado de creencia en el que se encuentra el agente
- Se puede generar y buscar un árbol de estados de información
- Conduce a comportamientos racionales como:
  - Actuar para obtener información
  - Señalar a tu compañero
  - Actuar aleatoriamente para minimizar la divulgación de información

---

# Limitaciones de los Algoritmos de Búsqueda en Juegos

- La búsqueda alfa-beta es vulnerable a errores en la función heurística
- Desperdicio de tiempo computacional para decidir el mejor movimiento cuando es obvio (meta-razonamiento)
- El razonamiento se hace sobre movimientos individuales. Los humanos razonan en niveles abstractos
- Posibilidad de incorporar Aprendizaje Automático en el proceso de búsqueda de juegos

---

# Resumen

- Algoritmo minimax: selecciona movimientos óptimos mediante una enumeración en profundidad del árbol de juego
- Algoritmo alfa-beta: mayor eficiencia al eliminar subárboles
- Función de evaluación: una heurística que estima la utilidad del estado
- Búsqueda de árbol Monte Carlo (MCTS): sin heurística, juega el juego hasta el final con reglas y repite múltiples veces para determinar movimientos óptimos durante el playout

# Notas sobre la traducción

- Se mantuvo el término "minimax" sin traducir, ya que es ampliamente utilizado en español en el contexto de teoría de juegos.
- "Poda α–β" es la traducción estándar para "α–β pruning" en español.
- "Búsqueda de árbol Monte Carlo" es la traducción común para "Monte Carlo Tree Search" en español.
- Se mantuvo el término "playout" sin traducir, ya que es utilizado frecuentemente en español en el contexto de MCTS.
- "Retropropagación" es la traducción estándar para "back-propagation" en este contexto.

La traducción de términos técnicos específicos de la teoría de juegos y la inteligencia artificial presentó algunos desafíos. Se buscó mantener un equilibrio entre la precisión técnica y la naturalidad en español argentino, utilizando términos reconocibles en el ámbito académico y profesional de Argentina.

```