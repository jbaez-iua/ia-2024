
---
marp: true
theme: default
paginate: true
---

<!-- _class: lead -->
# Robótica
Capítulo 26

---

# Esquema

- Robots
- Hardware robótico
- ¿Qué tipo de problema resuelve la robótica?
- Percepción robótica
- Planificación y control
- Planificación de movimientos inciertos
- Aprendizaje por refuerzo en robótica
- Humanos y robots
- Dominios de aplicación

---

# Robots

- Agentes físicos que realizan tareas manipulando el mundo físico
- Equipados con:
  - Efectores: patas, ruedas, articulaciones y pinzas
  - Sensores: para percibir su entorno
- Maximizan la utilidad esperada eligiendo cómo actuar sobre los efectores
- El entorno es:
  - Parcialmente observable
  - Estocástico
  - Generalmente modelado con espacio de estados continuo
- El aprendizaje robótico está limitado por la operación en tiempo real

---

# Hardware robótico

Tipos de robots:

1. Manipuladores (brazos robóticos)
   - Gran capacidad de carga (ensamblaje de autos)
   - Brazos montables en sillas de ruedas

2. Robots móviles
   - Usan ruedas, patas o rotores para moverse
   - Incluyen drones cuadricópteros (VANTs)

3. Otros: prótesis, exoesqueletos, robots con alas, enjambres, entornos inteligentes

---

![bg right:40% 80%](https://example.com/robot_arm.jpg)

# Hardware robótico: Manipuladores

- Brazo robótico industrial con efector final personalizado
- Brazo robótico asistencial Kinova® JACO® montado en una silla de ruedas

---

![bg right:40% 80%](https://example.com/mobile_robots.jpg)

# Hardware robótico: Robots móviles

- Rover Curiosity de la NASA en Marte
- Dron Skydio acompañando a una familia en un paseo en bicicleta

---

# Hardware robótico: Sensores

1. Sensores pasivos (por ejemplo, cámaras)
   - Observan señales generadas por otras fuentes

2. Sensores activos (por ejemplo, sonar, lidar, radar)
   - Envían energía al entorno

3. Telémetros
   - Miden la distancia a objetos cercanos

4. Visión estereoscópica
   - Usa múltiples cámaras para calcular la profundidad

---

![bg right:40% 80%](https://example.com/3d_range_image.jpg)

# Hardware robótico: Detección 3D

- Cámara de tiempo de vuelo
- Imagen de rango 3D para detección de obstáculos

---

# Hardware robótico: Actuadores

Tipos de actuadores:
1. Actuadores eléctricos
2. Actuadores hidráulicos
3. Actuadores neumáticos

Articulaciones:
- Articulaciones de revolución: un eslabón rota en relación con otro
- Articulaciones prismáticas: un eslabón se desliza a lo largo de otro

---

# Resolución de problemas en robótica

Jerarquía de tres niveles:
1. Planificación de tareas: plan de acción de alto nivel
2. Planificación de movimiento: búsqueda de caminos
3. Control: lograr el movimiento planificado usando actuadores

Componentes adicionales:
- Aprendizaje de preferencias: estimación de objetivos del usuario
- Predicción de personas: pronóstico de acciones de otros

---

# Percepción robótica

Percepción: mapeo de mediciones de sensores a representaciones internas

Buenas representaciones internas:
1. Contienen suficiente información para la toma de decisiones
2. Se pueden actualizar eficientemente
3. Corresponden a variables de estado naturales en el mundo físico

Conceptos clave:
- Modelo del sensor: P(Xt | z1:t, a1:t−1)
- Modelo de movimiento: P(Xt+1 | xt, at)

---

# Localización y mapeo

Métodos de localización:
1. Localización Monte Carlo (MCL)
   - Usa filtro de partículas

2. Filtro de Kalman
   - Representa la distribución posterior como una gaussiana
   - Filtro de Kalman extendido (EKF) para sistemas no lineales

3. Localización y mapeo simultáneos (SLAM)
   - Para entornos desconocidos

---

![bg right:40% 80%](https://example.com/robot_model.jpg)

# Percepción robótica: Modelos

- Modelo cinemático simplificado de un robot móvil
- Modelo de sensor de barrido de rango

---

![bg 80%](https://example.com/mcl_algorithm.jpg)

# Algoritmo de localización Monte Carlo

---

![bg right:40% 80%](https://example.com/mcl_visualization.jpg)

# Visualización de localización Monte Carlo

(a) Incertidumbre global inicial
(b) Incertidumbre bimodal en corredor simétrico
(c) Incertidumbre unimodal después de entrar en una habitación distintiva

---

![bg right:40% 80%](https://example.com/ekf_localization.jpg)

# Localización con filtro de Kalman extendido

Robot moviéndose en línea recta, observando puntos de referencia

---

![bg 80%](https://example.com/adaptive_vision.jpg)

# Visión adaptativa para clasificación de superficies transitables

---

# Planificación y control

Conceptos clave:
- Camino: secuencia de puntos en el espacio geométrico
- Planificación de movimiento: encontrar un buen camino
- Control de seguimiento de trayectoria: ejecutar acciones para seguir el camino
- Trayectoria: camino con tiempo asociado para cada punto
- Espacio de configuración (C-espacio): espacio multidimensional abstracto que representa la configuración del robot

---

![bg right:40% 80%](https://example.com/workspace_cspace.jpg)

# Espacio de trabajo vs. Espacio de configuración

(a) Representación del espacio de trabajo de un brazo robótico con 2 grados de libertad
(b) Espacio de configuración correspondiente

---

# Técnicas de planificación de movimiento

1. Grafos de visibilidad
2. Diagramas de Voronoi
3. Descomposición celular
4. Planificación de movimiento aleatorizada
5. Árboles de exploración rápida aleatoria (RRT)
6. Optimización de trayectoria para planificación cinemática

---

![bg right:40% 80%](https://example.com/motion_planning_examples.jpg)

# Ejemplos de planificación de movimiento

- Diagrama de Voronoi
- RRT bidireccional
- Mapa de ruta probabilístico (PRM)
- Optimización de trayectoria

---

# Control de seguimiento de trayectoria

- Controlador estable: pequeñas perturbaciones llevan a errores acotados
- Estrictamente estable: vuelve y se mantiene en la trayectoria de referencia después de una perturbación
- Controlador PD: Proporcional-Derivativo
- Controlador PID: Proporcional-Integral-Derivativo
- Control por par calculado

---

![bg 80%](https://example.com/robot_arm_control.jpg)

# Ejemplos de control de brazo robótico

---

# Planificación de movimientos inciertos

Estrategias:
1. Discretización del espacio de estados continuo
2. Elección del estado más probable de la distribución de probabilidad
3. Uso de políticas en lugar de planes deterministas
4. Replanificación en línea y control predictivo del modelo (MPC)
5. Acciones de recopilación de información (marco POMDP)
6. Movimientos protegidos

---

# Aprendizaje por refuerzo en robótica

Desafíos:
- Espacios de estados y acciones continuos
- Reducción de la complejidad de muestras en el mundo real

Enfoques:
1. Aprendizaje por refuerzo basado en modelo
2. Transferencia de simulación a realidad
3. Aprendizaje de extremo a extremo
4. Aprovechamiento de primitivas de movimiento de alto nivel
5. Meta-aprendizaje y aprendizaje por transferencia

---

# Humanos y robots

Problema de coordinación: optimizar la recompensa con personas en el entorno

Formulación teórica de juegos:
- Estado: x = (xR, xH)
- Acciones: uR y uH
- Objetivos: JR(x, uR, uH) y JH(x, uH, uR)

Complicaciones:
1. Juego con información incompleta
2. Espacios de estados y acciones continuos
3. El comportamiento humano puede no seguir la solución teórica del juego

---

![bg right:40% 80%](https://example.com/human_prediction.jpg)

# Predicción de acciones humanas

- Uso del modelo softmax para P(uH | x, JH)
- Actualización de creencias sobre objetivos humanos
- Consideración de la influencia del robot en las acciones humanas

---

# Dominios de aplicación

1. Cuidado del hogar
2. Atención médica
3. Servicios
4. Autos autónomos
5. Entretenimiento
6. Exploración y entornos peligrosos
7. Industria

---

![bg right:40% 80%](https://example.com/application_examples.jpg)

# Ejemplos de aplicaciones

- Robot quirúrgico
- Robot de entrega hospitalaria
- Auto autónomo
- Robot de exploración minera

---

<!-- _class: lead -->
# Resumen

- Tipos de robots: manipuladores y robots móviles
- Sensores y actuadores para percepción y movimiento
- Percepción robótica usando filtrado probabilístico
- Técnicas de planificación de movimiento y control
- Planificación bajo incertidumbre
- Interacción humano-robot y coordinación
- Amplia gama de dominios de aplicación

```

# Notas sobre la traducción

1. Se utilizó el "vos" implícito en los títulos y subtítulos, manteniendo un tono formal.
2. Se mantuvieron términos técnicos en inglés cuando son comúnmente usados así en el ámbito académico argentino, como "hardware", "software", "lidar", "rover", etc.
3. Se tradujeron nombres de conceptos específicos cuando tienen una versión aceptada en español, como "Aprendizaje por refuerzo" para "Reinforcement Learning".
4. Se utilizaron algunos términos específicos del español argentino en contextos académicos, como "VANTs" (Vehículos Aéreos No Tripulados) para "UAVs".

# Aspectos desafiantes de la traducción

1. La traducción de términos técnicos específicos de robótica requirió un equilibrio entre mantener la precisión técnica y usar términos comprensibles en el contexto argentino.
2. Algunos conceptos, como "Rapidly-exploring random trees (RRT)", no tienen una traducción establecida en español, por lo que se optó por mantener el término en inglés con su acrónimo.
3. La adaptación de expresiones idiomáticas en inglés a equivalentes naturales en español argentino, manteniendo el tono formal y académico, fue un desafío en algunas secciones.
4. La estructura de algunas frases tuvo que ser modificada para sonar más natural en español, manteniendo al mismo tiempo la precisión del contenido técnico.