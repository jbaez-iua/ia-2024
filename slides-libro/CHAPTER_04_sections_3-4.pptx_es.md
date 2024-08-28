---
marp: true
theme: default
paginate: true
---

<!-- Diapositiva de título -->
# Búsqueda en Entornos Complejos
## Capítulo 4, Secciones 3–4

---

<!-- Diapositiva de esquema -->
# Esquema

- Búsqueda local y problemas de optimización
- Ascenso de colinas
- Recocido simulado
- Algoritmos genéticos
- Búsqueda local en espacios continuos
- Búsqueda con acciones no deterministas
- Búsqueda en entornos parcialmente observables

---

<!-- Diapositiva de búsqueda local y problemas de optimización -->
# Búsqueda Local y Problemas de Optimización

- El camino es irrelevante; el estado objetivo en sí es la solución
- Espacio de estados = conjunto de configuraciones "completas"
- Buscar la configuración óptima (ej., TSP) o configuración que satisfaga restricciones (ej., horarios)
- Algoritmos de mejora iterativa: mantienen un único estado "actual", intentan mejorarlo
- Algoritmos de búsqueda local:
  - Buscan desde el estado inicial hacia estados vecinos
  - No llevan registro de caminos o estados explorados
  - No son sistemáticos - podrían omitir porciones del espacio de búsqueda

---

<!-- Diapositiva de ejemplo: Problema del Viajante de Comercio -->
# Ejemplo: Problema del Viajante de Comercio

- Comenzar con cualquier tour completo, realizar intercambios por pares
- Las variantes llegan al 1% del óptimo muy rápidamente con miles de ciudades

![width:600px](https://example.com/tsp-image.jpg)

---

<!-- Diapositiva de ejemplo: Problema de las n reinas -->
# Ejemplo: Problema de las n Reinas

- Colocar n reinas en un tablero de n × n sin que dos reinas estén en la misma fila, columna o diagonal
- Mover una reina para reducir el número de conflictos

![bg right:40% 80%](https://example.com/nqueens-image.jpg)

- Casi siempre resuelve problemas de n reinas casi instantáneamente para n muy grande (ej., n = 1 millón)

---

<!-- Diapositiva de ascenso de colinas -->
# Ascenso de Colinas (o ascenso/descenso de gradiente)

"Como escalar el Everest en una niebla espesa con amnesia"

```python
función Ascenso-De-Colinas(problema) devuelve un estado que es un máximo local
    actual ← Crear-Nodo(Estado-Inicial[problema])
    bucle hacer
        vecino ← un sucesor de actual con el valor más alto
        si Valor[vecino] ≤ Valor[actual] entonces devolver Estado[actual]
        actual ← vecino
```

---

<!-- Diapositiva de ascenso de colinas continuación -->
# Ascenso de Colinas (continuación)

![bg right:50% 80%](https://example.com/hill-climbing-landscape.jpg)

- Considerar el paisaje del espacio de estados
- El ascenso de colinas con reinicio aleatorio supera los máximos locales—trivialmente completo
- Los movimientos laterales aleatorios escapan de los hombros y bucles en máximos planos

---

<!-- Diapositiva de recocido simulado -->
# Recocido Simulado

Idea: escapar de máximos locales permitiendo algunos movimientos "malos" pero disminuyendo gradualmente su tamaño y frecuencia

```python
función Recocido-Simulado(problema, programa) devuelve un estado solución
    actual ← Crear-Nodo(Estado-Inicial[problema])
    para t ← 1 hasta ∞ hacer
        T ← programa[t]
        si T = 0 entonces devolver actual
        siguiente ← un sucesor seleccionado aleatoriamente de actual
        ΔE ← Valor[siguiente] – Valor[actual]
        si ΔE > 0 entonces actual ← siguiente
        sino actual ← siguiente solo con probabilidad e^(ΔE/T)
```

---

<!-- Diapositiva de propiedades del recocido simulado -->
# Propiedades del Recocido Simulado

- A "temperatura" T fija, la probabilidad de ocupación del estado alcanza la distribución de Boltzmann
  $p(x) = αe^{-E(x)/kT}$
- Si T disminuye lo suficientemente lento ⇒ siempre se alcanza el mejor estado x*
- Ideado por Metropolis et al., 1953, para modelado de procesos físicos
- Ampliamente utilizado en diseño de VLSI, programación de aerolíneas, etc.

---

<!-- Diapositiva de búsqueda local por haces -->
# Búsqueda Local por Haces

- Mantener k estados en lugar de 1; elegir los k mejores de todos sus sucesores
- ¡No es lo mismo que k búsquedas ejecutadas en paralelo!
- Las búsquedas que encuentran buenos estados reclutan a otras búsquedas para unirse a ellas
- Problema: a menudo, los k estados terminan en la misma colina local
- Solución: elegir k sucesores aleatoriamente, sesgados hacia los buenos
- ¡Observar la estrecha analogía con la selección natural!

---

<!-- Diapositiva de algoritmos genéticos -->
# Algoritmos Genéticos

![bg right:50% 80%](https://example.com/genetic-algorithm.jpg)

- Búsqueda local por haces estocástica + generar sucesores a partir de pares de estados
- Requieren estados codificados como cadenas (los GP usan programas)
- El cruce ayuda si y solo si las subcadenas son componentes significativos
- AG ≠ evolución: ej., ¡los genes reales codifican maquinaria de replicación!

---

<!-- Diapositiva de espacios de estados continuos -->
# Espacios de Estados Continuos

Ejemplo: Ubicación de tres aeropuertos en Rumania
- Espacio de estados de 6-D definido por (x1, y1), (x2, y2), (x3, y3)
- Función objetivo: suma de distancias al cuadrado desde cada ciudad al aeropuerto más cercano

Métodos:
1. Discretización: Convertir espacio continuo en espacio discreto
2. Métodos de gradiente: Calcular ∇f para aumentar/reducir f
3. Método de Newton–Raphson: Itera para resolver ∇f(x) = 0

---

<!-- Diapositiva de búsqueda con acciones no deterministas -->
# Búsqueda con Acciones No Deterministas

- El agente no conoce el estado exacto después de una acción
- Usa "estado de creencia" - conjunto de estados posibles
- Ejemplos:
  - Mundo de la aspiradora errática
  - Árboles de búsqueda AND-OR
  - Enfoque de intentar, intentar de nuevo

---

<!-- Diapositiva de búsqueda en entornos parcialmente observables -->
# Búsqueda en Entornos Parcialmente Observables

- Observabilidad parcial: Las percepciones del agente no son suficientes para determinar el estado exacto
- Búsqueda sin observación (problema sin sensores/conformante):
  - Solución: secuencia de acciones, no un plan condicional
- Requiere una función para monitorear/estimar el entorno y mantener el estado de creencia

---

<!-- Diapositiva de resumen -->
# Resumen

- Los métodos de búsqueda local mantienen solo un pequeño número de estados en memoria
- La búsqueda AND-OR genera planes de contingencia para entornos no deterministas
- El estado de creencia es el conjunto de estados posibles en entornos parcialmente observables
- Los algoritmos de búsqueda estándar se pueden aplicar al espacio de estados de creencia para problemas sin sensores

---
