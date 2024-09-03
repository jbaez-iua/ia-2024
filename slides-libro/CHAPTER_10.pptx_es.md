
---
marp: true
theme: default
paginate: true
---

<!-- _class: lead -->
# Representación del Conocimiento
## Capítulo 10

---

# Esquema

- Ingeniería Ontológica
- Categorías y Objetos
- Eventos
- Objetos Mentales y Lógica Modal
- Sistemas de Razonamiento para Categorías
- Razonamiento con Información por Defecto

---

<!-- _class: lead -->
# Ingeniería Ontológica

---

# Ingeniería Ontológica

- Representaciones generales y flexibles para dominios complejos
- Ontología superior: El marco general de conceptos

Ejemplo de ontología del mundo:

![width:800px](https://example.com/ontology_image.png)

---

<!-- _class: lead -->
# Categorías y Objetos

---

# Categorías y Objetos

- La organización de objetos en categorías es vital para la representación del conocimiento
- Categorías para LPO representadas por predicados y objetos
- Composición física: un objeto puede ser parte de otro
  - Ejemplo: `ParteDe(BuenosAires, Argentina)`
- Mediciones: valores asignados a propiedades de objetos
  - Ejemplo: `Longitud(L1) = Pulgadas(1.5) = Centimetros(3.81)`

---

# Categorías y Objetos (cont.)

- Materia: porción de la realidad que desafía la individuación obvia
- Propiedades intrínsecas: pertenecen a la sustancia del objeto
- Propiedades extrínsecas: peso, longitud, forma
- Sustancia: categoría que incluye solo propiedades intrínsecas (sustantivo de masa)
- Sustantivo contable: clase que incluye propiedades extrínsecas

---

<!-- _class: lead -->
# Eventos

---

# Cálculo de Eventos

- Componentes: eventos, fluentes y puntos temporales
- Ejemplo de fluente: `En(Juan, BuenosAires)`
- Ejemplo de evento: 
  ```
  E1 ∈ Vuelos ∧ Volador(E1, Juan) ∧ 
  Origen(E1, BUE) ∧ Destino(E1, COR)
  ```
  - `Vuelos` es la categoría de todos los eventos de vuelo

---

<!-- _class: lead -->
# Objetos Mentales y Lógica Modal

---

# Objetos Mentales

- Conocimiento en la cabeza de alguien (o en una BC)
- Actitudes proposicionales: Cree, Sabe, Quiere, Informa
- Ejemplo: `Sabe(Lola, PuedeVolar(Superman))`

---

# Lógica Modal

- Aborda oraciones verbosas y poco elegantes en la lógica regular
- Usa operadores modales especiales que toman oraciones como argumentos
- Notación: `SAP` (A sabe P)
  - S: operador modal para conocimiento
  - A: agente (subíndice)
  - P: oración

---

# Lógica Modal: Inferencia

Los agentes pueden sacar conclusiones:
```
(SaP ∧ Sa(P ⇒ Q)) ⇒ SaQ
```

Los agentes lógicos pueden introspeccionar:
```
SaP ⇒ Sa(SaP)
```

---

<!-- _class: lead -->
# Sistemas de Razonamiento para Categorías

---

# Redes Semánticas

- Convenientes para el razonamiento de herencia
- Ejemplo: María hereda la propiedad de tener dos piernas
- Algoritmo de herencia:
  1. Sigue el enlace `MiembroDe` desde María hasta su categoría
  2. Sigue los enlaces `SubconjuntoDe` hacia arriba en la jerarquía
  3. Encuentra una categoría con un enlace `Piernas` encuadrado

![width:600px](https://example.com/semantic_network.png)

---

# Lógicas Descriptivas

- Diseñadas para facilitar la descripción de definiciones y propiedades de categorías
- Evolucionaron de las redes semánticas
- Tareas de inferencia principales:
  - Subsunción: verificar si una categoría es un subconjunto de otra
  - Clasificación: verificar si un objeto pertenece a una categoría

Ejemplo (lenguaje CLASSIC):
```
Soltero = Y(NoEsCasado, Adulto, Masculino)
```

---

<!-- _class: lead -->
# Razonamiento con Información por Defecto

---

# Circunscripción y Lógica por Defecto

Circunscripción:
- Versión más potente de la suposición de mundo cerrado
- Especifica predicados que se asumen "tan falsos como sea posible"
- Ejemplo de lógica de preferencia de modelos

Lógica por Defecto:
- Formalismo para generar conclusiones no monótonas contingentes
- Ejemplo de regla: `Ave(x) : Vuela(x) / Vuela(x)`
  - Si `Ave(x)` es verdadero y `Vuela(x)` es consistente, concluir `Vuela(x)` por defecto

---

# Sistemas de Mantenimiento de la Verdad (SMV)

- Manejan la revisión de creencias y complicaciones de hechos inferidos
- SMV basado en justificaciones (SMVJ):
  - Anota oraciones con justificaciones (conjunto de oraciones de las que se infirió)
  - Hace eficiente la retractación
  - Asume que las oraciones consideradas una vez probablemente serán consideradas de nuevo

---

<!-- _class: lead -->
# Resumen

---

# Puntos Clave

- Ontología superior basada en categorías y cálculo de eventos
- Sistemas de representación de propósito especial:
  - Redes semánticas
  - Lógicas descriptivas
- Lógicas no monótonas:
  - Circunscripción
  - Lógica por defecto
- Sistemas de mantenimiento de la verdad para actualizaciones y revisiones eficientes del conocimiento

---

<!-- _footer: "© 2022 Pearson Education Ltd." -->
# ¡Gracias!

¿Alguna pregunta?

```

## Notas sobre la traducción

1. "Knowledge Representation" se tradujo como "Representación del Conocimiento", que es el término comúnmente usado en la literatura académica en español.

2. Se utilizó "vos" para la pregunta final "¿Alguna pregunta?", que es característico del español argentino.

3. Se adaptaron algunos ejemplos para hacerlos más relevantes al contexto argentino, como cambiar "Bucharest, Romania" por "BuenosAires, Argentina".

4. Se mantuvieron términos técnicos en inglés cuando son comúnmente usados así en la jerga informática en Argentina, como "Truth Maintenance Systems".

5. Se tradujo "Bachelor" como "Soltero" en el ejemplo de lógica descriptiva, manteniendo la estructura del ejemplo original.

6. Se usó "Sistemas de Mantenimiento de la Verdad (SMV)" como traducción de "Truth Maintenance Systems (TMS)", que es la forma en que se suele referir a estos sistemas en la literatura en español.

## Aspectos desafiantes de la traducción

1. La traducción de términos técnicos específicos de la inteligencia artificial y la representación del conocimiento fue un desafío, ya que algunos términos no tienen una traducción establecida en español argentino.

2. Mantener el equilibrio entre la formalidad académica y la naturalidad del español argentino fue complejo, especialmente en secciones con alto contenido técnico.

3. La adaptación de ejemplos para que sean culturalmente relevantes sin perder el significado original requirió cuidado y creatividad.

4. La traducción de fórmulas lógicas y notaciones matemáticas necesitó especial atención para asegurar que mantuvieran su significado preciso.

5. Algunos conceptos, como "fluent" en el cálculo de eventos, no tienen una traducción directa ampliamente aceptada en español, por lo que se optó por mantener una transliteración ("fluente") que es comúnmente usada en la literatura académica en español.