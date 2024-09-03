
---
marp: true
theme: default
paginate: true
---

<!-- _class: lead -->
# Aprendizaje por Refuerzo
### Capítulo 23

---

<!-- _footer: "Inteligencia Artificial: Un Enfoque Moderno Cuarta Edición, Edición Global © 2022 Pearson Education Ltd." -->

## Esquema

- Aprendizaje a partir de Recompensas 
- Aprendizaje por Refuerzo Pasivo 
- Aprendizaje por Refuerzo Activo 
- Generalización en el Aprendizaje por Refuerzo 
- Búsqueda de Políticas 
- Aprendizaje por Imitación e Inversión del Aprendizaje por Refuerzo 
- Aplicaciones del Aprendizaje por Refuerzo

---

<!-- _header: "Aprendizaje a partir de Recompensas" -->

## Interacción del Agente

- El agente interactúa con el mundo y recibe recompensas (refuerzos) periódicamente

## Enfoques

1. **Aprendizaje por refuerzo basado en modelos**
   - Utiliza un modelo de transición
   - El modelo puede ser inicialmente desconocido
   - Aprende observando los efectos de las acciones
   - Útil para la estimación de estados
   - Aprende una función de utilidad U(s)

2. **Aprendizaje por refuerzo sin modelo**
   - No conoce ni aprende el modelo de transición
   - Aprendizaje de utilidad de acción: Q-learning, aprende la función Q(s, a)
   - Búsqueda de políticas: aprende una política π(s) que mapea estados a acciones

---

<!-- _header: "Aprendizaje por Refuerzo Pasivo" -->

![bg right:40% 80%](https://i.imgur.com/placeholder.png)

## Políticas Óptimas

- Entorno estocástico
- R(s, a, s') = 0.04 para transiciones entre estados no terminales
- Dos políticas óptimas en el estado (3,1): Izquierda y Arriba

## Utilidades

- Utilidades de los estados en el mundo 4 × 3, dada la política π

---

<!-- _header: "Aprendizaje por Refuerzo Pasivo" -->

## Agente de Aprendizaje Pasivo

- Aprende la función de utilidad U^π(s)
- Recompensa total descontada esperada si se ejecuta la política π desde el estado s
- Modelo de transición desconocido P(s'| s, a)
- Ejecuta pruebas usando la política π
- Comienza en el estado (1,1), experimenta transiciones de estado hasta llegar a los estados terminales (4,2) o (4,3)

### Utilidad Esperada

$U^\pi(s) = E\left[\sum_{t=0}^{\infty} \gamma^t R_t \mid S_0 = s, \pi\right]$

---

<!-- _header: "Aprendizaje a partir de Recompensas" -->

## Estimación Directa de Utilidad

- Utilidad de un estado: recompensa total esperada desde ese estado en adelante (recompensa-por-venir)
- Calcula la recompensa-por-venir observada para cada estado
- Actualiza la utilidad estimada
- Se reduce a un problema estándar de aprendizaje supervisado
  - Ejemplos: pares (estado, recompensa-por-venir)
- La utilidad está determinada por la recompensa y la utilidad esperada de los estados sucesores

---

<!-- _header: "Aprendizaje a partir de Recompensas" -->

## Programación Dinámica Adaptativa (ADP)

- El agente aprende el modelo de transición que conecta los estados
- Resuelve el proceso de decisión de Markov correspondiente usando programación dinámica

![bg right:40% 80%](https://i.imgur.com/placeholder2.png)

### Curvas de Aprendizaje para el Mundo 4 x 3

a) Estimaciones de utilidad para estados seleccionados
b) Error cuadrático medio en la estimación de U(1, 1)

---

<!-- _header: "Aprendizaje a partir de Recompensas" -->

## Aprendizaje por Diferencia Temporal

- Ajusta las utilidades de los estados observados para que concuerden con las ecuaciones de restricción
- Ecuación TD: $U(s) \leftarrow U(s) + \alpha [R(s,a,s') + \gamma U(s') - U(s)]$
  - α: parámetro de tasa de aprendizaje
- Usa la diferencia en utilidades entre estados sucesivos
- Ajusta las estimaciones de utilidad hacia el equilibrio ideal
- No se necesita modelo de transición para las actualizaciones

### Comparación con ADP

| TD | ADP |
|:---|:---|
| Ajusta el estado para que concuerde con el sucesor observado | Ajusta el estado para que concuerde con todos los sucesores posibles |
| Un solo ajuste por transición observada | Múltiples ajustes para restaurar la consistencia |

---

<!-- _header: "Aprendizaje por Refuerzo Activo" -->

## Agentes Activos vs. Pasivos

- Agente pasivo: política fija
- Agente activo: decide sobre las acciones

## Exploración

- ADP puede no aprender la ruta óptima debido a la política fija
- Agente codicioso: toma la acción que cree que es la mejor
- GLIE (Codicioso en el Límite de Exploración Infinita)
  - Probar cada acción en cada estado un número ilimitado de veces

---

<!-- _header: "Aprendizaje por Refuerzo Activo" -->

## Exploración Segura

- Muchas acciones son irreversibles
- Peor caso: estado absorbente
- Elegir una política que funcione bien para un rango de modelos posibles

### Enfoques Matemáticos:
1. Aprendizaje por refuerzo bayesiano
2. Exploración POMDP
3. Teoría de control robusto

---

<!-- _header: "Aprendizaje por Refuerzo Activo" -->

## Q-Learning por Diferencia Temporal

- Aprende la función de utilidad de acción Q(s, a) en lugar de U(s)
- Actualización TD sin modelo para los valores Q
- No se necesita modelo de transición
- Actualización SARSA (Estado, Acción, Recompensa, Estado, Acción):
  $Q(s,a) \leftarrow Q(s,a) + \alpha[R(s,a,s') + \gamma Q(s',a') - Q(s,a)]$

![bg right:40% 80%](https://i.imgur.com/placeholder3.png)

---

<!-- _header: "Generalización en el Aprendizaje por Refuerzo" -->

## Desafíos

- Olvido catastrófico
- Selección de características

## Aprendizaje por Refuerzo Profundo (Deep RL)

- Utiliza aproximadores de funciones no lineales
- Desafíos:
  - Difícil lograr un buen rendimiento
  - Comportamiento impredecible en entornos ligeramente diferentes

---

<!-- _header: "Generalización en el Aprendizaje por Refuerzo" -->

## Conformación de Recompensas

- Aborda el problema de asignación de crédito
- Proporciona pseudorecompensas adicionales

## Aprendizaje por Refuerzo Jerárquico (HRL)

- Similar a la planificación HTN
- Utiliza un programa parcial con estructura jerárquica
- Espacio de estados conjunto: (s, m) - estado físico s, estado de la máquina m
- Estado de elección σ = (s, m): contador de programa en punto de elección

---

<!-- _header: "Búsqueda de Políticas" -->

## Enfoque

- Ajusta continuamente la política para mejorar el rendimiento
- Utiliza representaciones parametrizadas de π

## Desafíos

- La política es una función discontinua de los parámetros para acciones discretas

## Solución

- Representación de política estocástica π(s, a)
- Ejemplo: Softmax
- Vector de gradiente de política ∇θρ(θ)

---

<!-- _header: "Aprendizaje por Imitación e Inversión del Aprendizaje por Refuerzo" -->

## Aprendizaje por Imitación

- Aprendizaje a partir de observaciones del comportamiento experto

### Enfoques

1. **Aprendizaje por Imitación**
   - Aprendizaje supervisado en pares estado-acción observados

2. **Inversión del Aprendizaje por Refuerzo (IRL)**
   - Aprender recompensas observando la política
   - Comprender la motivación del experto
   - Derivar la política óptima para la función de recompensa aprendida

---

<!-- _header: "Aplicaciones del Aprendizaje por Refuerzo" -->

## Juegos

- Red Q profunda (DQN) de DeepMind
  - Entrenada en 49 videojuegos Atari
- AlphaGo: Derrotó a los mejores jugadores humanos

## Control de Robots

- Equilibrio de carro-poste (péndulo invertido)
- Vuelo de helicóptero radiocontrolado
- Búsqueda de políticas en grandes MDPs
- Combinado con aprendizaje por imitación e IRL

![bg right:40% 80%](https://i.imgur.com/placeholder4.png)

---

<!-- _class: lead -->

# Resumen

- RL basado en modelos: Tiene modelo de transición P(s'|s,a), aprende función de utilidad U(s)
- RL sin modelo: Puede aprender función de utilidad de acción Q(s,a) o política π(s)
- Enfoques de aprendizaje de utilidad: Estimación directa de utilidad, ADP, TD
- La conformación de recompensas y el RL jerárquico ayudan a aprender comportamientos complejos
- Los métodos de búsqueda de políticas operan directamente sobre la representación de la política
- El aprendizaje por imitación es efectivo cuando es difícil especificar la función de recompensa correcta

```

## Notas sobre la traducción

1. "Reinforcement Learning" se tradujo como "Aprendizaje por Refuerzo", que es el término comúnmente usado en español argentino en contextos académicos.

2. Se mantuvo la forma "vos" implícita en las explicaciones, aunque no se usó explícitamente debido al tono formal del texto.

3. Términos técnicos como "Q-learning", "SARSA", "POMDP", y "GLIE" se mantuvieron en inglés, ya que son ampliamente reconocidos en la comunidad académica argentina.

4. "Reward shaping" se tradujo como "Conformación de recompensas", un término usado en la literatura académica en español.

5. Se mantuvo la notación matemática sin cambios, ya que es estándar en el campo.

## Aspectos desafiantes de la traducción

1. La traducción de "reward-to-go" como "recompensa-por-venir" fue desafiante, ya que no existe un término estandarizado en español para este concepto.

2. Mantener el equilibrio entre la terminología técnica en inglés y sus equivalentes en español fue complejo, especialmente en conceptos como "Deep Reinforcement Learning" o "Inverse Reinforcement Learning".

3. La traducción de "absorbing state" como "estado absorbente" requirió verificación para asegurar que es el término usado en la literatura académica en español argentino.

4. La adaptación de las explicaciones de conceptos matemáticos y de programación para que sean claras y precisas en español argentino fue un desafío constante.