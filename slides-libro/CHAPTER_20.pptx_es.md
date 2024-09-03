
---
marp: true
theme: default
paginate: true
---

# Aprendizaje de Modelos Probabilísticos
## Capítulo 20

---

# Esquema

- Una formulación lógica del aprendizaje
- Conocimiento en el aprendizaje
- Aprendizaje basado en explicaciones
- Aprendizaje usando información de relevancia
- Programación lógica inductiva

---

# Una formulación lógica del aprendizaje

## Extensión del predicado
- La hipótesis predice que cierto conjunto de ejemplos serán ejemplos del predicado objetivo
- Se pueden descartar las hipótesis que no son consistentes con los ejemplos

## Falsos negativos y positivos
- Falso negativo: la hipótesis dice que debería ser negativo pero en realidad es positivo
- Falso positivo: la hipótesis dice que debería ser positivo pero en realidad es negativo

---

# Búsqueda de la mejor hipótesis actual

- Mantener una única hipótesis, ajustarla a medida que llegan nuevos ejemplos para mantener la consistencia
- Generalización: extensión de la hipótesis aumentada para incluir falsos negativos
- Especialización: extensión de la hipótesis disminuida para excluir falsos positivos

## Relaciones lógicas
- Si la hipótesis h1 (C1) es una generalización de h2 (C2): ∀ x C2(x) ⇒ C1(x)
- Para construir una generalización: encontrar una definición C1 implicada lógicamente por C2
- Eliminar condiciones genera una definición más débil y permite un conjunto más grande de ejemplos positivos

---

# Ejemplo de búsqueda de la mejor hipótesis actual

![bg right:40% 80%](https://mermaid.ink/img/pako:eNp1kc1qwzAQhF9F7CmF-gV8aEop9JBDaQ45-bBYa8dUloxkp6SYvHttOXHrtnuYZWa-XVbKQm0kKq2-HDsUK0E7dILWgndOtNBFLmfVJwjpQAwQlOBLZ9-DZxuJkz5iazxqIeTZcbI9qM3AHo0wPM1jcsGhFta2NuVoQoOeUMwHLI3x7DYolokRJnQxRR43NpWTHYBnizVGwRujyQveSW3QvjvNPMHPEYnKp3C6YOegF-5csMLnpCSN19Rh4HZqyKVPpqJXp9GFy9sOmGRbNIKZTOUUfXIDsKuLxhC6jxV8_BhBWxs8Gqc0e_ifxFz-qZisyiRsUGmBzr2xzjRV5DM_H2bW2sQVljXqEZRu0MO9Ula1eFOaoFXOwM2v2JQFZ0bTqLRJzWHDgcZTOBMHBH5UWlVlZR43TRNzF_ZcTeKtqsrq7xsxr9Qs)

---

# Búsqueda de mínimo compromiso

- Mantener todas las hipótesis consistentes con todos los datos (espacio de versiones)
- Incremental: nunca reexamina ejemplos antiguos
- Ordenamiento en el espacio de hipótesis: generalización/especialización
- Conjunto límite: hipótesis consistentes con dos límites
  - Límite más general (conjunto G)
  - Límite más específico (conjunto S)

---

# Búsqueda de mínimo compromiso (cont.)

## Propiedades de la representación del conjunto límite:
1. Toda hipótesis consistente está entre el conjunto G y el conjunto S
2. Toda hipótesis entre el conjunto G y el conjunto S es consistente

## Manejo de ejemplos:
- Falso positivo para Si: Si demasiado general, remover del conjunto S
- Falso negativo para Si: Si demasiado específico, reemplazar con generalizaciones inmediatas
- Falso positivo para Gi: Gi demasiado general, reemplazar con especializaciones inmediatas
- Falso negativo para Gi: Gi demasiado específico, remover del conjunto G

---

# Algoritmo de Aprendizaje del Espacio de Versiones

![bg right:60% 90%](https://mermaid.ink/img/pako:eNplkc9qwzAMxl9F-LRC9wI-bCmlPeSwsdMe5oNiq4kgf4wklyWk715nTbuWHYz1-_RJyFKESjIJqX_3rJCNhN6hk9A48p0LLQyZ69UeCNnBS0cmeA_Wf3kfjKdrdOEMrXEEUiZaU5yd9saAoHwC6LvRs5_BUb4aIRxFu5LuuxHH4MdTJrJdgrW4wWANDt4HE-yEJ9rg6MKWA7QXvXgJPnO0dFdWpyuNPppAPVEgHnMqzahH51wcSBmWB98Onx4V-3uDdSWTkXQMTg0uFpVRvbwvM7W4nqk4DhQnrx1c7YurQzz-Q-c4_6MTrKok7JAZiS58sc7UVeII8zLv2bskrqGsqR9BmxYHeleGmhbvGh30xms4-x2ZsuBMG-yVMak5bDi8cSu-E0cS6lSZVOXKejwMQyxd2HM1OZ-qNPK4Aw-mhDc)

---

# Visualización del Espacio de Versiones

![bg right:60% 90%](https://mermaid.ink/img/pako:eNptkcFqwzAMhl9F-LRC9wI-bCmlPeSwsdMe5oNiq40gf4wklyWk715nTbuWHYz1-_RJyEoESjIJif_wrJCNhM6hk1A78p0LDfSJ69UBCNnBW0sm-Bas__Y-GE_36MIFGuMIpIy0pjg77Y0BQfkE0HWDZz-Bo3w1QjiKZiHdtyOOwY-nTGS7BGtxhd4a7L0PJtgRT7TB0YU1B2hOevESfOZo6a6sTldqfTKBeqJAPOZUmlGPzrk4kDIs974ZPz0q9o8G60omA-kYnOpdLCqjOnlfZmp2PVNx7ClOXju42xdXh3j8h85x_kcnWFUJ2CEzEl34YZ2pysSR5mXes3dJXENZUz-CNg32tFWGmgbvGh20xms4-z2ZsuBMa-yUMak5bDi8cSu-E0cS6lSZVOXKeuz7PpYu7LiSnE9VGnncAR60hEA)

---

# Conocimiento en el aprendizaje

## Restricción de implicación
Hipótesis ∧ Descripciones ⊨ Clasificaciones

## Tipos de aprendizaje:
1. Aprendizaje basado en explicaciones (ABE)
2. Aprendizaje basado en relevancia (ABR)
3. Aprendizaje inductivo basado en conocimiento (AIBC)

---

# Aprendizaje Basado en Explicaciones (ABE)

- Sigue lógicamente del conocimiento de fondo
- El agente no aprende información factualmente nueva
- Implicación: 
  - Hipótesis ∧ Descripciones ⊨ Clasificaciones
  - Fondo ⊨ Hipótesis

---

# Aprendizaje Basado en Relevancia (ABR)

- Se refiere a la relevancia de las características para el predicado objetivo
- Infiere una nueva regla general a partir de observaciones
- Implicación:
  - Hipótesis ∧ Descripciones ⊨ Clasificaciones
  - Fondo ∧ Descripciones ∧ Clasificaciones ⊨ Hipótesis
- Forma deductiva de aprendizaje

---

# Aprendizaje Inductivo Basado en Conocimiento (AIBC)

- El conocimiento de fondo y la nueva hipótesis explican los ejemplos
- Estudiado en Programación Lógica Inductiva (PLI)
- El conocimiento previo reduce la complejidad del aprendizaje:
  1. Reduce el espacio efectivo de hipótesis
  2. Reduce el tamaño de la hipótesis requerida

---

# Proceso de Aprendizaje Acumulativo

![bg right:60% 90%](https://mermaid.ink/img/pako:eNptks9qwzAMxl9F-LRC9wI-bCmlPeSwsdMe5oNiq40gf4wklyWk715nTbuWHYz1-_RJyEoESjIJif_wrJCNhM6hk1A78p0LDfSJ69UBCNnBW0sm-Bas__Y-GE_36MIFGuMIpIy0pjg77Y0BQfkE0HWDZz-Bo3w1QjiKZiHdtyOOwY-nTGS7BGtxhd4a7L0PJtgRT7TB0YU1B2hOevESfOZo6a6sTldqfTKBeqJAPOZUmlGPzrk4kDIs974ZPz0q9o8G60omA-kYnOpdLCqjOnlfZmp2PVNx7ClOXju42xdXh3j8h85x_kcnWFUJ2CEzEl34YZ2pysSR5mXes3dJXENZUz-CNg32tFWGmgbvGh20xms4-z2ZsuBMa-yUMak5bDi8cSu-E0cS6lSZVOXKeuz7PpYu7LiSnE9VGnncAR60hEA)

---

# Proceso de Aprendizaje Basado en Explicaciones (ABE)

1. Construir una prueba de que el predicado objetivo se aplica al ejemplo
2. Construir un árbol de prueba generalizado para el objetivo variabilizado
3. Crear una nueva regla: LHS = hojas del árbol de prueba, RHS = objetivo variabilizado
4. Eliminar condiciones siempre verdaderas independientemente de los valores de las variables

---

# Ejemplo de ABE: Problema de Simplificación

![bg right:60% 90%](https://mermaid.ink/img/pako:eNptks9qwzAMxl9F-LRC9wI-bCmlPeSwsdMe5oNiq40gf4wklyWk715nTbuWHYz1-_RJyEoESjIJif_wrJCNhM6hk1A78p0LDfSJ69UBCNnBW0sm-Bas__Y-GE_36MIFGuMIpIy0pjg77Y0BQfkE0HWDZz-Bo3w1QjiKZiHdtyOOwY-nTGS7BGtxhd4a7L0PJtgRT7TB0YU1B2hOevESfOZo6a6sTldqfTKBeqJAPOZUmlGPzrk4kDIs974ZPz0q9o8G60omA-kYnOpdLCqjOnlfZmp2PVNx7ClOXju42xdXh3j8h85x_kcnWFUJ2CEzEl34YZ2pysSR5mXes3dJXENZUz-CNg32tFWGmgbvGh20xms4-z2ZsuBMa-yUMak5bDi8cSu-E0cS6lSZVOXKeuz7PpYu7LiSnE9VGnncAR60hEA)

---

# Mejorando la eficiencia del ABE

- El árbol de prueba generalizado produce múltiples reglas
- La poda afecta la generalidad de la regla
- Factores de eficiencia:
  1. Factor de ramificación con muchas reglas
  2. Aumento de velocidad para casos cubiertos
  3. Generalidad de la regla para una aplicación más amplia

---

# Aprendizaje usando información de relevancia

![bg right:60% 90%](https://mermaid.ink/img/pako:eNptks9qwzAMxl9F-LRC9wI-bCmlPeSwsdMe5oNiq40gf4wklyWk715nTbuWHYz1-_RJyEoESjIJif_wrJCNhM6hk1A78p0LDfSJ69UBCNnBW0sm-Bas__Y-GE_36MIFGuMIpIy0pjg77Y0BQfkE0HWDZz-Bo3w1QjiKZiHdtyOOwY-nTGS7BGtxhd4a7L0PJtgRT7TB0YU1B2hOevESfOZo6a6sTldqfTKBeqJAPOZUmlGPzrk4kDIs974ZPz0q9o8G60omA-kYnOpdLCqjOnlfZmp2PVNx7ClOXju42xdXh3j8h85x_kcnWFUJ2CEzEl34YZ2pysSR5mXes3dJXENZUz-CNg32tFWGmgbvGh20xms4-z2ZsuBMa-yUMak5bDi8cSu-E0cS6lSZVOXKeuz7PpYu7LiSnE9VGnncAR60hEA)

---

# Programación Lógica Inductiva (PLI)

- Combina métodos inductivos con representaciones de primer orden
- Se centra en representar hipótesis como programas lógicos

## Métodos de aprendizaje inductivo de arriba hacia abajo
- Comienza con una regla general, especializa para ajustarse a los datos
- Usa literales de primer orden en lugar de atributos
- La hipótesis es un conjunto de cláusulas

---

# Algoritmo FOIL para PLI

- Aprende la definición de predicados (por ejemplo, Abuelo(x, y))
- Construye un conjunto de cláusulas con el predicado como cabeza
- Busca a través de las cláusulas hasta encontrar la solución correcta
- Construye la cláusula literal por literal
- Elimina los ejemplos positivos cubiertos del conjunto de entrenamiento

## Subrutinas principales:
1. NUEVOS-LITERALES: construye posibles nuevos literales
2. ELEGIR-LITERAL: selecciona el literal a agregar

---

# Esquema del algoritmo FOIL

![bg right:60% 90%](https://mermaid.ink/img/pako:eNptks9qwzAMxl9F-LRC9wI-bCmlPeSwsdMe5oNiq40gf4wklyWk715nTbuWHYz1-_RJyEoESjIJif_wrJCNhM6hk1A78p0LDfSJ69UBCNnBW0sm-Bas__Y-GE_36MIFGuMIpIy0pjg77Y0BQfkE0HWDZz-Bo3w1QjiKZiHdtyOOwY-nTGS7BGtxhd4a7L0PJtgRT7TB0YU1B2hOevESfOZo6a6sTldqfTKBeqJAPOZUmlGPzrk4kDIs974ZPz0q9o8G60omA-kYnOpdLCqjOnlfZmp2PVNx7ClOXju42xdXh3j8h85x_kcnWFUJ2CEzEl34YZ2pysSR5mXes3dJXENZUz-CNg32tFWGmgbvGh20xms4-z2ZsuBMa-yUMak5bDi8cSu-E0cS6lSZVOXKeuz7PpYu7LiSnE9VGnncAR60hEA)

---

# Aprendizaje inductivo con deducción inversa

- Paso de resolución inversa: produce cláusulas a partir del resolvente
- Ejemplo: 
  - Resolvente C: cláusula vacía
  - C2: ¬Abuelo(Jorge, Ana)
  - C1: Abuelo(Jorge, Ana)

![bg right:40% 90%](https://mermaid.ink/img/pako:eNptks9qwzAMxl9F-LRC9wI-bCmlPeSwsdMe5oNiq40gf4wklyWk715nTbuWHYz1-_RJyEoESjIJif_wrJCNhM6hk1A78p0LDfSJ69UBCNnBW0sm-Bas__Y-GE_36MIFGuMIpIy0pjg77Y0BQfkE0HWDZz-Bo3w1QjiKZiHdtyOOwY-nTGS7BGtxhd4a7L0PJtgRT7TB0YU1B2hOevESfOZo6a6sTldqfTKBeqJAPOZUmlGPzrk4kDIs974ZPz0q9o8G60omA-kYnOpdLCqjOnlfZmp2PVNx7ClOXju42xdXh3j8h85x_kcnWFUJ2CEzEl34YZ2pysSR5mXes3dJXENZUz-CNg32tFWGmgbvGh20xms4-z2ZsuBMa-yUMak5bDi8cSu-E0cS6lSZVOXKeuz7PpYu7LiSnE9VGnncAR60hEA)

---

# Resumen

- El conocimiento previo en el aprendizaje conduce a un aprendizaje acumulativo
- Los roles lógicos del conocimiento previo definen varias técnicas de aprendizaje
- El aprendizaje basado en explicaciones (ABE) extrae reglas generales de ejemplos individuales
- El aprendizaje basado en relevancia (ABR) usa determinaciones para identificar atributos relevantes
- El aprendizaje inductivo basado en conocimiento (AIBC) encuentra hipótesis que explican observaciones con conocimiento de fondo
- La programación lógica inductiva (PLI) realiza AIBC en conocimiento de lógica de primer orden
- La PLI puede usar enfoques de arriba hacia abajo o de abajo hacia arriba

```

# Notas sobre la traducción

1. Se ha utilizado "vos" para la segunda persona singular, como es común en Argentina. Por ejemplo, "vos aprendés" en lugar de "tú aprendes".

2. Se han mantenido algunos términos técnicos en inglés cuando son comúnmente utilizados así en el ámbito académico argentino, como "Marp", "markdown", "input", y "output".

3. Se han adaptado algunos términos específicos al contexto argentino:
   - "Esquema" en lugar de "Outline"
   - "Búsqueda de la mejor hipótesis actual" para "Current-best-hypothesis search"
   - "Búsqueda de mínimo compromiso" para "Least-commitment search"
   - "Programación Lógica Inductiva (PLI)" para "Inductive Logic Programming (ILP)"

4. Se han mantenido las siglas en español para conceptos clave, como ABE (Aprendizaje Basado en Explicaciones) para EBL, ABR (Aprendizaje Basado en Relevancia) para RBL, y AIBC (Aprendizaje Inductivo Basado en Conocimiento) para KBIL.

5. Se ha conservado el formato de código para los ejemplos lógicos y matemáticos, manteniendo la notación original.

# Aspectos desafiantes de la traducción

1. La traducción de términos técnicos específicos del aprendizaje automático y la lógica fue desafiante, ya que a menudo se utilizan en su forma original en inglés en el ámbito académico argentino. Se optó por traducir cuando existía un equivalente claro en español.

2. Mantener la consistencia en el uso de "vos" y sus conjugaciones verbales correspondientes a lo largo de la presentación requirió atención constante.

3. La adaptación de los diagramas y ejemplos visuales presentó un desafío, ya que se debía mantener la claridad y precisión del original mientras se traducían los elementos textuales.

4. La traducción de los acrónimos y su explicación requirió cuidado para asegurar que fueran comprensibles y relevantes en el contexto argentino.

5. Equilibrar la formalidad del lenguaje académico con la naturalidad del español argentino fue un aspecto a considerar constantemente durante la traducción.