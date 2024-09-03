
# Toma de Decisiones Multiagente
## Capítulo 17

Inteligencia Artificial: Un Enfoque Moderno
Cuarta Edición, Edición Global © 2022 Pearson Education Ltd.

---

# Esquema

- Propiedades de los Entornos Multiagente
- Teoría de Juegos No Cooperativos
- Teoría de Juegos Cooperativos
- Toma de Decisiones Colectivas

---

# Propiedades de los Entornos Multiagente: Un Tomador de Decisiones

- Múltiples actores, pero un solo tomador de decisiones
- Suposición de agente benevolente: los agentes simplemente hacen lo que se les indica
- Caso especial: un solo tomador de decisiones con múltiples efectores operando concurrentemente
  - Planificación multiefector: gestiona cada efector, manejando interacciones
  - Planificación multicuerpo: los efectores están físicamente desacoplados en unidades separadas

---

# Propiedades de los Entornos Multiagente: Múltiples Tomadores de Decisiones

- Múltiples actores y múltiples tomadores de decisiones
- Cada uno tiene preferencias y elige/ejecuta su propio plan
- Dos posibilidades:
  1. Objetivo común (problema de coordinación)
  2. Preferencias personales (potencialmente opuestas)

- Teoría de juegos: teoría de la toma de decisiones estratégicas
  - Los jugadores tienen en cuenta cómo pueden actuar los demás
  - Se usa en diseño de agentes y diseño de mecanismos
  - Puede ser cooperativa o no cooperativa

---

# Planificación Multiagente: Problemas de Concurrencia

- Los planes de cada agente pueden ejecutarse simultáneamente
- Los agentes deben considerar las interacciones entre sus acciones y las de los demás

## Enfoque de Ejecución Entrelazada
- Preserva el orden de las acciones en los planes respectivos
- Asume que las acciones son atómicas
- Debe ser correcto para todas las posibles intercalaciones
- No modela acciones verdaderamente simultáneas
- El número de secuencias entrelazadas crece exponencialmente

---

# Planificación Multiagente: Enfoques de Concurrencia

## Enfoque de Concurrencia Verdadera
- No crea un ordenamiento serializado completo de las acciones
- Las acciones están parcialmente ordenadas

## Enfoque de Sincronización Perfecta
- Reloj global
- Las acciones son simultáneas, con la misma duración
- Semántica simple
- Restricción de acción concurrente: las acciones deben o no deben ejecutarse concurrentemente

---

# Planificación con Múltiples Agentes: Cooperación y Coordinación

- Adoptar convenciones antes de participar en una actividad conjunta
  - Convención: restricción en la selección de planes conjuntos
  - Las convenciones generalizadas se llaman leyes sociales

- Usar comunicación para lograr conocimiento común del plan conjunto factible

- Reconocimiento de planes: una sola acción (o secuencia corta) de un agente permite a otros determinar el plan conjunto sin ambigüedades

---

# Teoría de Juegos No Cooperativos: Juegos en Forma Normal

- Todos los jugadores actúan simultáneamente
- Ningún jugador tiene conocimiento de las elecciones de los demás
- Definido por 3 componentes:
  1. Jugadores
  2. Acciones
  3. Función de pagos (matriz de pagos)

Ejemplo: Juego Morra de dos dedos

![width:600px](https://i.imgur.com/PlvFQKt.png)

---

# Teoría de Juegos No Cooperativos: Estrategias

- Los conceptos de solución intentan hacer preciso el razonamiento
- Estrategia pura: política determinista (acción única para juego de un solo movimiento)
- Estrategia mixta: política aleatorizada que selecciona acciones según una distribución de probabilidad
- Perfil de estrategia: asignación de una estrategia a cada jugador

---

# Teoría de Juegos No Cooperativos: Dominancia

- Estrategia dominante: estrategia que domina a todas las demás
- Dominancia fuerte: el resultado para s es mejor para p que s' para cada elección de los otros jugadores
- Dominancia débil: s es mejor que s' en al menos un perfil de estrategia y no peor en ningún otro
- Un jugador racional siempre elegirá una estrategia dominante y evitará una estrategia dominada
- Equilibrio de estrategia dominante: resultado cuando todos los jugadores eligen estrategias dominantes

---

# Bienestar Social y Equilibrios

## Conceptos de Bienestar Social
- Optimalidad de Pareto: ningún resultado mejora a un jugador sin empeorar a otro
- Bienestar social utilitario: medida de la bondad del resultado agregado
- Bienestar social igualitario: maximiza la utilidad esperada del miembro en peor situación
- Coeficiente de Gini: resume cuán uniformemente se distribuye la utilidad entre los jugadores

## Cálculo de Equilibrios
- Mejor respuesta miope / mejor respuesta iterada
- Equilibrio de Nash: perfil de estrategia donde cada jugador hace la elección óptima dados los demás
- Juegos de suma cero: los pagos siempre suman cero
- Técnica maximin y algoritmo minimax

---

# Árboles de Juego Minimax

![width:800px](https://i.imgur.com/j7EvGKm.png)

---

# Juegos Repetidos

- Juego de múltiples movimientos – juego iterado
- Los jugadores juegan repetidamente rondas de un juego de un solo movimiento (juego de etapa)
- Estrategias modeladas usando máquinas de estados finitos (FSMs)

Estrategias comunes:
- Tit-for-Tat (Ojo por Ojo)
- HAWK (HALCÓN) y DOVE (PALOMA)
- GRIM (IMPLACABLE)

![width:600px](https://i.imgur.com/QrI7kev.png)

---

# Ejemplo de Juegos de Asistencia: Juego del Clip

![width:700px](https://i.imgur.com/Gc5uxQR.png)

---

# Teoría de Juegos Cooperativos

- Juego cooperativo G = (N, ν)
  - N: conjunto de jugadores
  - ν: función característica

- Coalición: subconjunto de jugadores
- Gran coalición: conjunto de todos los jugadores
- Particiones y estructuras de coalición

## Conceptos
- Superaditividad
- Imputación
- Valor de Shapley: esquema de distribución justa

---

# Teoría de Juegos Cooperativos: Valor de Shapley

Contribución marginal del jugador i a C: mci(C)

Axiomas de equidad satisfechos por el valor de Shapley:
1. Eficiencia
2. Jugador ficticio
3. Simetría
4. Aditividad

---

# Toma de Decisiones Colectivas: Red de Contratos

Mecanismo: lenguaje, agente distinguido, regla de resultado

Asignación de tareas con red de contratos (cuatro fases):

![width:700px](https://i.imgur.com/gLHKhuy.png)

---

# Toma de Decisiones Colectivas: Subastas y Votación

## Subastas
- Subasta ascendente (inglesa)
- Subasta de sobre cerrado
- Subasta de segundo precio de sobre cerrado

## Votación
- Teoría de la elección social
- Función de bienestar social
- Cuatro propiedades de una buena función de bienestar social (Teorema de Arrow)

---

# Toma de Decisiones Colectivas: La Estrategia de Zeuthen

- Mide la disposición de un agente a arriesgarse al conflicto
- Un valor de riesgo más alto indica menos que perder en caso de conflicto

![width:600px](https://i.imgur.com/M2LtFIL.png)

---

# Resumen

- La planificación multiagente es necesaria para entornos con múltiples agentes
- La teoría de juegos describe el comportamiento racional en interacciones multiagente
- Los conceptos de solución caracterizan los resultados racionales de un juego
- La teoría de juegos no cooperativos asume toma de decisiones independiente
- La teoría de juegos cooperativos considera acuerdos vinculantes y coaliciones

---

# Notas sobre la traducción

- "Toma de Decisiones Multiagente" es la traducción preferida en Argentina para "Multiagent Decision Making".
- Se mantuvo el término "Teoría de Juegos" como traducción directa de "Game Theory", ya que es el término técnico utilizado en la academia argentina.
- "Planificación multiefector" y "Planificación multicuerpo" son traducciones literales que se usan en el ámbito académico argentino.
- Se mantuvo el término "Equilibrio de Nash" sin traducir, ya que es un concepto reconocido internacionalmente.
- "Ojo por Ojo" es la traducción común en Argentina para la estrategia "Tit-for-Tat".
- "HALCÓN" y "PALOMA" son las traducciones utilizadas para "HAWK" y "DOVE" en el contexto de teoría de juegos en Argentina.
- "Valor de Shapley" se mantiene como término técnico sin traducción adicional.

# Aspectos desafiantes de la traducción

1. Mantener la precisión técnica: Fue crucial preservar el significado exacto de los términos técnicos mientras se adaptaban al español argentino.

2. Adaptación de ejemplos: El juego "Morra de dos dedos" y el "Juego del Clip" son ejemplos que podrían no ser familiares en Argentina, pero se mantuvieron por su relevancia técnica.

3. Equilibrio entre términos locales e internacionales: Se buscó un balance entre usar términos reconocibles internacionalmente (como "Equilibrio de Nash") y adaptar otros al contexto local.

4. Estructura académica: Se mantuvo la estructura formal y el tono académico apropiado para material universitario en Argentina.

5. Traducción de gráficos: Los gráficos se mantuvieron en inglés, ya que la traducción de imágenes está fuera del alcance de este ejercicio. En una situación real, estos también deberían ser traducidos y adaptados.
```