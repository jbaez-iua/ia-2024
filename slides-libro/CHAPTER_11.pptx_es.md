
# Planificación Automatizada
## Capítulo 11

---

# Esquema

- Definición de Planificación Clásica
- Algoritmos para Planificación Clásica
- Heurísticas para Planificación
- Planificación Jerárquica
- Planificación y Actuación en Dominios No Deterministas
- Tiempo, Cronogramas y Recursos
- Análisis de Enfoques de Planificación

---

# Definición de Planificación Clásica

- Planificación clásica: Encontrar una secuencia de acciones para lograr un objetivo en un entorno discreto, determinista, estático y completamente observable.
- Lenguaje de Definición de Dominios de Planificación (PDDL): Una representación factorizada para dominios de planificación.
- El PDDL básico maneja dominios de planificación clásica; las extensiones cubren dominios no clásicos.

---

# Definición de Planificación Clásica (cont.)

- Estado: Representado como una conjunción de fluentes atómicos fundamentados
- Usa semántica de base de datos: suposición de mundo cerrado
- Esquema de acción: Representa una familia de acciones fundamentadas
  - Consiste en nombre de acción, variables, precondición y efecto

Ejemplo:
```
Acción(Volar(p, desde, hasta),
  PRECOND: En(p, desde) ∧ Avión(p) ∧ Aeropuerto(desde) ∧ Aeropuerto(hasta)
  EFECTO: ¬En(p, desde) ∧ En(p, hasta))
```

---

# Algoritmos para Planificación Clásica

1. Búsqueda hacia adelante en el espacio de estados
   - Comienza en el estado inicial
   - Determina las acciones aplicables unificando el estado actual contra las precondiciones

2. Búsqueda hacia atrás
   - Comienza en el objetivo y aplica acciones hacia atrás
   - Considera acciones relevantes en cada paso
   - Reduce el factor de ramificación

---

# Algoritmos para Planificación Clásica (cont.)

Otros enfoques:
- Graphplan: Usa una estructura de datos especializada llamada grafo de planificación
- Cálculo situacional: Describe problemas de planificación en lógica de primer orden
- Planificación de orden parcial: Representa un plan como un grafo en lugar de una secuencia lineal

---

# Heurísticas para Planificación

- Heurística de ignorar precondiciones: Elimina todas las precondiciones de las acciones
- Heurística de ignorar listas de eliminación: Quita todos los literales negativos de los efectos
- Poda independiente del dominio:
  - Reducción de simetría
  - Poda hacia adelante
- Plan relajado y acciones preferidas

---

# Heurísticas para Planificación (cont.)

Abstracción de estados en planificación:
- Mapeo de muchos a uno desde la representación fundamental a la representación abstracta
- Relajaciones que disminuyen el número de estados
- Descomposición: Dividir un problema en partes
- Suposición de independencia de submetas

---

# Planificación Jerárquica

- Usa niveles más altos de abstracción con descomposición jerárquica
- Reduce la tarea computacional a un pequeño número de actividades en el siguiente nivel inferior
- Acciones de alto nivel (HLAs) y Redes de tareas jerárquicas (HTN)
- Plan de alto nivel (HLP): Concatenación de implementaciones de cada HLA en la secuencia

---

# Planificación y Actuación en Dominios No Deterministas

Planificación sin sensores:
- Suposición de mundo abierto
- Estados de creencia y aplicaciones de acciones
- Efectos condicionales

---

# Planificación y Actuación en Dominios No Deterministas (cont.)

Planificación contingente:
- Generación de planes con ramificación condicional basada en percepciones
- Apropiada para entornos con observabilidad parcial o no determinismo

Planificación en línea:
- Monitoreo de ejecución
- Replanificación cuando es necesario
- Tres enfoques: Monitoreo de acción, Monitoreo de plan, Monitoreo de objetivo

---

# Tiempo, Cronogramas y Recursos

- La planificación clásica no aborda restricciones de tiempo y recursos
- Representación de restricciones temporales y de recursos:
  - Acciones con duración y restricciones
  - Tipos y números de recursos
  - Recursos consumibles vs. reutilizables
  - Agregación: Representación de recursos como cantidades numéricas

---

# Tiempo, Cronogramas y Recursos (cont.)

Resolución de problemas de programación:
- Método de la Ruta Crítica (CPM)
- Holgura y ventanas de programación
- Enfoques: ramificación y acotación, recocido simulado, búsqueda tabú, satisfacción de restricciones
- Heurística de holgura mínima

---

# Análisis de Enfoques de Planificación

- La planificación combina búsqueda y lógica
- Escala desde problemas de juguete hasta aplicaciones industriales del mundo real
- Controla la explosión combinatoria mediante la identificación de subproblemas independientes
- Investigación en curso para mejores técnicas y representaciones
- Sistemas de planificación de portafolio: Colección de algoritmos disponibles para cualquier problema dado

---

# Resumen

- PDDL describe estados iniciales y finales, y acciones
- La planificación de red de tareas jerárquicas (HTN) usa acciones de alto nivel (HLAs)
- Los planes contingentes permiten detectar durante la ejecución
- La planificación en línea usa monitoreo de ejecución y reparaciones
- Muchas acciones consumen recursos
- Investigación en curso en técnicas y representaciones de planificación

```

## Notas sobre la traducción

1. "vos" form: En esta traducción, no se utilizó explícitamente la forma "vos" ya que el texto es de naturaleza técnica y no incluye diálogos o instrucciones directas al lector.

2. Términos técnicos: Se mantuvieron en su forma original algunos términos técnicos ampliamente reconocidos en el campo de la Inteligencia Artificial y la Planificación, como "PDDL", "Graphplan", "branch-and-bound", "tabu search", etc.

3. Adaptaciones académicas:
   - "Classical Planning" se tradujo como "Planificación Clásica", que es el término comúnmente usado en las universidades argentinas.
   - "Critical Path Method (CPM)" se tradujo como "Método de la Ruta Crítica (CPM)", manteniendo la sigla en inglés que es reconocida internacionalmente.

4. Términos específicos:
   - "Planificación sin sensores" se usó para "Sensorless planning", que es una traducción común en el contexto académico argentino.
   - "Recocido simulado" se utilizó para "simulated annealing", que es el término aceptado en la comunidad científica argentina.

## Aspectos desafiantes de la traducción

1. Equilibrio entre términos técnicos en inglés y español: Fue necesario decidir cuándo mantener términos en inglés (como "branch-and-bound") y cuándo traducirlos (como "búsqueda tabú" para "tabu search").

2. Adaptación de conceptos sin equivalente directo: Algunos conceptos, como "slack" en el contexto de planificación, se tradujeron como "holgura", que es el término más cercano utilizado en Argentina.

3. Mantenimiento de la precisión técnica: Fue crucial asegurar que la traducción de términos técnicos y descripciones de algoritmos mantuviera la precisión del original, especialmente en secciones como la descripción de PDDL y los diferentes enfoques de planificación.

4. Formato Marp: Se mantuvo la estructura y formato del documento original para asegurar su compatibilidad con Marp, incluyendo los delimitadores de diapositivas y la formatación de código.

```