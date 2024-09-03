
---
marp: true
theme: default
paginate: true
---

# Programación Probabilística
## Capítulo 18

<footer>Inteligencia Artificial: Un Enfoque Moderno Cuarta Edición, Edición Global © 2022 Pearson Education Ltd.</footer>

---

# Esquema

- Modelos de Probabilidad Relacionales
- Modelos de Probabilidad de Universo Abierto
- Seguimiento de un Mundo Complejo
- Programas como Modelos de Probabilidad

---

# Modelos de Probabilidad Relacionales

- Sin suposiciones de mundo cerrado
- Sintaxis y semántica:
  - Símbolos constantes, de función y de predicado
  - Firma de tipo para cada función
- Elimina mundos posibles

---

# Ejemplo del Dominio de Recomendación de Libros

- Tipos: Cliente y Libro
- Firmas de tipo para funciones y predicados:
  ```
  Honesto : Cliente → {verdadero, falso}
  Amabilidad : Cliente → {1, 2, 3, 4, 5}
  Calidad : Libro → {1, 2, 3, 4, 5}
  Recomendación : Cliente × Libro → {1, 2, 3, 4, 5}
  ```

---

# Modelos de Probabilidad Relacionales: Variables Básicas

- Obtenidas al instanciar cada función con cada combinación posible de objetos
  ```
  Honesto(C1), Calidad(B2), Recomendación(C1, B2)
  ```
- Una declaración de dependencia para cada función
- Ejemplo:
  ```
  Recomendación(c, b) ∼ RecTCP(Honesto(c), Amabilidad(c), Calidad(b))
  ```
  donde RecTCP es una tabla de probabilidad condicional con 2 x 5 x 5 = 50 filas, cada una con 5 entradas.

---

# Independencia Específica del Contexto

```
Recomendación(c, b) ∼ 
  si Honesto(c) entonces 
    HonestoRecTCP(Amabilidad(c), Calidad(b))
  sino 
    (0.4, 0.1, 0.0, 0.1, 0.4)
```

Elaboración adicional:

```
Recomendación(c, b) ∼ 
  si Honesto(c) entonces 
    si Fan(c, Autor(b)) entonces 
      Exactamente(5)
    sino 
      HonestoRecTCP(Amabilidad(c), Calidad(b))
  sino 
    (0.4, 0.1, 0.0, 0.1, 0.4)
```

---

# Red Bayesiana para MPR de Recomendación de Libros

![width:900px](https://i.imgur.com/example1.png)

(a) Red bayesiana para un solo cliente C1 recomendando un solo libro B1. 
(b) Red bayesiana con dos clientes y dos libros.

---

# Red Bayesiana con Autor Desconocido

![width:900px](https://i.imgur.com/example2.png)

Fragmento de la red bayesiana equivalente para el MPR de recomendación de libros cuando Autor(B2) es desconocido.

---

# Inferencia en Modelos de Probabilidad Relacionales

- Enfoque: Construir la red bayesiana equivalente
- Dado: Símbolos constantes conocidos pertenecientes a cada tipo
- Proceso: Puesta a tierra/desenrollado

---

# Desventajas de la Puesta a Tierra

1. Red bayesiana grande
2. Muchos padres de variables

Contramedidas:
- Algoritmo de eliminación, encadenando desde la consulta y la evidencia
- Subestructura repetida
- Algoritmos de inferencia MCMC: muestreo de mundos posibles completos
- Demostradores de teoremas de resolución: instanciación de variables lógicas solo según sea necesario

---

# Modelos de Probabilidad de Universo Abierto

- Ejemplo: ISBN para identificación de libros
  - Puede tener varios ID para el mismo libro (tapa dura, rústica, letra grande, etc.)
- Sybils: múltiples ID
- Ataque Sybil: confundir un sistema de reputación
- Incertidumbre de existencia, por ejemplo, ¿cuáles son los libros y clientes reales subyacentes a los datos observados?
- Incertidumbre de identidad, por ejemplo, ¿qué términos lógicos realmente se refieren al mismo objeto?

---

# Modelo de Probabilidad de Universo Abierto (MPUA)

- Permite pasos generativos en comparación con MPR
- Puede agregar objetos al mundo posible en construcción
- El número y tipo de objetos puede depender de objetos existentes, sus propiedades y relaciones

Ejemplo:
```
#Cliente ∼ UniformeInt(1, 3)
#Libro ∼ UniformeInt(2, 4)
#IDLogin(Propietario = c) ∼ 
  si Honesto(c) entonces 
    Exactamente(1)
  sino 
    UniformeInt(2, 5)
```

Nota: La función Propietario es una función de origen

---

# Distribuciones en MPUA

- UniformeInt: Distribución uniforme utilizada en el ejemplo
- Para enteros no negativos, la Distribución de Poisson se usa comúnmente:
  P(X = k) = λ^k * e^(-λ) / k!
- Para números grandes: 
  - Distribución log-normal discreta
  - Distribución de orden de magnitud donde OM(3,1) = 10^3 (Desviación estándar entre 10^2 y 10^4)

---

# Variables en MPUA

Variables de número:
- Determinan el número de objetos de cada tipo con cada posible origen en cada mundo posible
- Ejemplo: #IDLogin(Propietario, (Cliente,,2))(ω) = 4, en el mundo ω, el cliente 2 posee 4 ID de login

Variables aleatorias básicas:
- Determinan valores de predicados y funciones para todas las tuplas de objetos
- Ejemplo: Honesto(Cliente,,2)(ω) = verdadero significa que en el mundo ω, el cliente 2 es honesto

---

# Ejemplo de Mundo para MPUA de Recomendación de Libros

![width:900px](https://i.imgur.com/example3.png)

Un mundo particular para el MPUA de recomendación de libros. Se muestran las variables de número y las variables aleatorias básicas en orden topológico, junto con sus valores elegidos y las probabilidades de esos valores.

---

# Inferencia en Modelos de Probabilidad de Universo Abierto

Ejemplo de coincidencia de citas:

```
tipo Investigador, Artículo, Cita
aleatorio String Nombre(Investigador)
aleatorio String Título(Artículo)
aleatorio Artículo ArtículoCitado(Cita)
aleatorio String Texto(Cita)
aleatorio Booleano Profesor(Investigador)
origen Investigador Autor(Artículo)

#Investigador ∼ OM(3, 1)
Nombre(r) ∼ PriorNombre()
Profesor(r) ∼ Booleano(0.2)
#Artículo(Autor = r) ∼ 
  si Profesor(r) entonces 
    OM(1.5, 0.5) 
  sino 
    OM(1, 0.5)
Título(p) ∼ PriorTítuloArtículo()
ArtículoCitado(c) ∼ ElecciónUniforme({Artículo p})
Texto(c) ∼ GramáticaHMM(Nombre(Autor(ArtículoCitado(c))), Título(ArtículoCitado(c)))
```

---

# Monitoreo de Tratados Nucleares

![width:900px](https://i.imgur.com/example4.png)

Una versión simplificada del modelo NET-VISA

---

# Seguimiento de un Mundo Complejo

Problema de asociación de datos: asociar datos de observación con los objetos que los generaron

Seguimiento de múltiples objetivos:
- A1 y A2 son objetos garantizados
- Posiciones verdaderas: X(A1,t) y X(A2,t), donde t es un entero no negativo que indexa los tiempos de actualización del sensor
- La primera observación llega en t = 1
- La distribución previa para la ubicación de cada aeronave en t = 0 es InitX()
- Cada aeronave se mueve independientemente según un modelo de transición conocido
- Modelo del sensor: modelo lineal-gaussiano donde una aeronave en posición x produce un punto b con posición observada Z(b)

---

# Desafíos en la Asociación de Datos

- Falsas alarmas (ruido): no causadas por objetos reales
- Fallos de detección: no se informa observación para un objeto real
- Complejidad de la inferencia en MPUA

Enfoques:
1. Elegir una única asignación "mejor" en cada paso de tiempo (por ejemplo, filtro del vecino más cercano)
2. Algoritmo MCMC para explorar el espacio de historiales de asignación

---

# MPUA para Seguimiento por Radar

![width:900px](https://i.imgur.com/example5.png)

Un MPUA para el seguimiento por radar de múltiples objetivos con falsas alarmas, fallas de detección, y entrada y salida de aeronaves.

---

# Ejemplo: Monitoreo de Tráfico

![width:700px](https://i.imgur.com/example6.png)

Imágenes de cámaras de vigilancia (a) aguas arriba y (b) aguas abajo a aproximadamente dos millas de distancia en la Autopista 99 en Sacramento, California. El vehículo encuadrado ha sido identificado en ambas cámaras.

---

# MPUA de Reconocimiento Óptico de Caracteres

![width:900px](https://i.imgur.com/example7.png)

Programa generativo para un modelo de probabilidad de universo abierto para el reconocimiento óptico de caracteres. El programa produce imágenes degradadas que contienen secuencias de letras generando cada secuencia, renderizándola en una imagen 2D e incorporando ruido aditivo en cada píxel.

---

# Programas como Modelos de Probabilidad

Lenguajes de programación probabilística (LPP):
- Construidos sobre la idea de que los modelos de probabilidad pueden definirse usando código ejecutable
- Heredan todo el poder expresivo de los lenguajes de programación
- Computacionalmente universales

Ejemplo: Lectura de texto degradado
- Puede manejar texto manchado, borroso o con puntos debido a daños por agua o envejecimiento
- Puede usarse para romper algunos tipos de CAPTCHAs

---

# Componentes del Programa Generativo

1. Una forma de generar una secuencia de letras
2. Una forma de generar una representación ruidosa y borrosa de estas letras usando una biblioteca gráfica estándar

Definiciones:
- Xi: variable aleatoria correspondiente a la i-ésima elección aleatoria realizada por el programa
- xi: un posible valor de Xi
- ω = {xi}: traza de ejecución (secuencia de posibles valores para las elecciones aleatorias)

Distribución de probabilidad sobre trazas: P(ω) = ∏i P(xi | x1, ..., xi-1)

---

# Ventajas de LPP

- Modular: Fácil de explorar mejoras al modelo subyacente
- Puede mejorarse incorporando un Modelo de Markov

---

# Programa Generativo de ROC

![width:900px](https://i.imgur.com/example8.png)

Programa generativo para un modelo de probabilidad de universo abierto para el reconocimiento óptico de caracteres. El programa produce imágenes degradadas que contienen secuencias de letras generando cada secuencia, renderizándola en una imagen 2D e incorporando ruido aditivo en cada píxel.

---

# Resultados de Inferencia de ROC

![width:900px](https://i.imgur.com/example9.png)

Imagen de entrada ruidosa (arriba) y resultados de inferencia (abajo) producidos por tres ejecuciones, cada una de 25 iteraciones MCMC, con el modelo del programa generativo anterior. Nótese que el proceso de inferencia identifica correctamente la secuencia de letras.

---

# Modelo de ROC Mejorado

![width:900px](https://i.imgur.com/example10.png)

Programa generativo para un modelo mejorado de reconocimiento óptico de caracteres que genera letras de acuerdo con un modelo de bigramas de letras cuyas frecuencias de pares de letras se estiman a partir de una lista de palabras en inglés.

---

# Comparación de Modelos de ROC

![width:900px](https://i.imgur.com/example11.png)

Arriba: imagen de entrada extremadamente ruidosa. 
Abajo a la izquierda: tres resultados de inferencia de 25 iteraciones MCMC con el modelo de letras independientes. 
Abajo a la derecha: tres resultados de inferencia con el modelo de bigramas de letras. 
Ambos modelos exhiben ambigüedad en los resultados, pero los resultados del último modelo reflejan conocimiento previo de secuencias de letras plausibles.

---

# Resumen

- Los modelos de probabilidad relacionales (MPR) definen modelos de probabilidad en mundos derivados de la semántica de bases de datos para lenguajes de primer orden
- Los MPR proporcionan modelos concisos para mundos con gran número de objetos y pueden manejar incertidumbre relacional
- Los modelos de probabilidad de universo abierto (MPUA) se basan en la semántica completa de la lógica de primer orden, permitiendo incertidumbre de identidad y existencia
- Los programas generativos representan modelos de probabilidad (incluyendo MPUA) como programas ejecutables en un lenguaje de programación probabilística (LPP)
- Un programa generativo representa una distribución sobre las trazas de ejecución del programa
- Los LPP típicamente proporcionan poder expresivo universal para modelos de probabilidad
```

Notas sobre la traducción:

1. "Honesto" se utilizó como traducción de "Honest" en lugar de "Sincero" para mantener la coherencia con el uso común en contextos académicos en Argentina.
2. "RecCPT" se tradujo como "RecTCP" (Tabla de Probabilidad Condicional de Recomendación) para mantener la abreviatura pero hacerla comprensible en español.
3. Se mantuvo "MCMC" sin traducir, ya que es un acrónimo comúnmente usado en su forma original incluso en textos académicos en español.
4. "ROC" se usó como abreviatura de "Reconocimiento Óptico de Caracteres", que es la traducción estándar de "OCR" en español.

Aspectos desafiantes de la traducción:

1. La traducción de términos técnicos específicos como "Relational Probability Models" y "Open-Universe Probability Models" requirió cuidado para mantener su significado preciso mientras se adaptaban al español.
2. La traducción de código y pseudocódigo presentó un desafío, ya que se debía decidir qué partes traducir (como nombres de variables y comentarios) y qué partes mantener en inglés (como palabras clave de programación).
3. La adaptación de conceptos académicos específicos del sistema educativo anglosajón al contexto argentino requirió considerar cuidadosamente las equivalencias y el uso común en el ámbito universitario argentino.

```