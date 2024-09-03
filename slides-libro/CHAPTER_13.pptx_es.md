
# Razonamiento Probabilístico
Capítulo 13

---

## Esquema

- Representación del Conocimiento en un Dominio Incierto
- Semántica de las Redes Bayesianas
- Inferencia Exacta en Redes Bayesianas  
- Inferencia Aproximada para Redes Bayesianas
- Redes Causales

---

## Representación del Conocimiento en un Dominio Incierto

Redes bayesianas:
- Representan dependencias entre variables
- Grafo simple y dirigido con nodos anotados con información cuantitativa de probabilidad

Sintaxis:
- Conjunto de nodos, uno por variable
- Grafo dirigido acíclico (enlace ≈ "influye directamente")
- Distribución condicional para cada nodo dados sus padres: P(Xi|Padres(Xi))
- En el caso más simple, la distribución condicional se representa como una tabla de probabilidad condicional (TPC)

---

## Ejemplo: Red del Clima

![width:700px](https://mermaid.ink/img/pako:eNpNjsEKwjAQRH8l7LkFf0DwUHoQvHjzHpJNbGGbLMmmUEr_3Wi19OBtHjOzb5jMiBKGaA0ZnCPjwDDwjJ6t5VUY9OLcYpXSWs-L0lrrQ6WUPpJSffKcTCBfijSwpZZOZh_Jknbs2KG3LhFD7xxmbGHAsfdG_Odt8OLRkcdgff4rl7ClgB5bGNNfKT-V8lMxlnlx2ZXHIq-OedkcD02-L5tmlR2yfQS8iiUJGKHiMw7vD4xwT_4)

- El clima es independiente de las otras variables
- Dolor de muelas y Caries son condicionalmente independientes dado Cavidad

---

## Ejemplo: Red de Alarma Antirrobo

Escenario: Estoy en el trabajo, mi vecino Juan llama para decir que mi alarma está sonando, pero mi vecina María no llama. A veces se activa por terremotos menores. ¿Hay un ladrón?

Variables: Ladrón, Terremoto, Alarma, JuanLlama, MaríaLlama

La topología de la red refleja conocimiento "causal":
- Un ladrón puede activar la alarma
- Un terremoto puede activar la alarma
- La alarma puede hacer que María llame
- La alarma puede hacer que Juan llame

---

## Red de Alarma Antirrobo (cont.)

![width:700px](https://mermaid.ink/img/pako:eNplkE1uwjAQha8y8iopUg-QBVLVRaqyQN1VdhN7Aq7i2MhOEEIcnaVX6EmauKEUmM3M-97MexMnJJSAHmWOFL6oCoqTKiZprGJFFvMipjxjwQbw1nAhuOCs3GK1KyoxyfMsiUFrnnIu-IbHsT7Uqo0cWupIyf9Qh5rWn2htNSfbbNM7rYhzkq6qBVmTdb5cP3UG8FLO-ZLzVq9_csFrWeF96WsuOsIfzOcpUVeF-cJd87IvN-3Ks-Q-mMBD0bFCFlRgAO_GE1sXmJ2M0cVIgX5T2xvmXoLO3-o8nPZ2g6fgFOpSFqUE_TtKQPt-lX1l5LRf4hEzqXJk4M-lB1-qY1A4fEVA0lOGJeiRe_RwQ9QeuYQ__2HeBrPhdDi5Hw0n9-PZ7el2Pj3MZneD0WwwuP0Gv6WMTA)

---

## Compacidad

- La TPC para Xi booleana con k padres booleanos tiene 2^k filas
- Cada fila requiere un número p para Xi = verdadero
- Si cada variable tiene no más de k padres, la red completa requiere O(n · 2^k) números
- Crece linealmente con n, vs. O(2^n) para la distribución conjunta completa
- Para la red de robo, 1 + 1 + 4 + 2 + 2 = 10 números (vs. 2^5 − 1 = 31)

---

## La Semántica de las Redes Bayesianas

La semántica global define la distribución conjunta completa como el producto de las distribuciones condicionales locales:

P(x1, ..., xn) = Πn i=1 P(xi|padres(Xi))

Ejemplo:
P(j ∧ m ∧ a ∧ ¬b ∧ ¬e) = P(j|a)P(m|a)P(a|¬b, ¬e)P(¬b)P(¬e)
= 0.9 × 0.7 × 0.001 × 0.999 × 0.998 ≈ 0.00063

---

## Semántica local

Semántica local: cada nodo es condicionalmente independiente de sus no descendientes dados sus padres

![width:700px](https://mermaid.ink/img/pako:eNptkMFqwzAMhl9F-NyCX2DQQ7dDYYceetu1h9hKG4iTYDsbjPDunVOWjK2XIPTp1y_9E8zWoYKBeotH-LLetmDZOTJOohNDyYVmOqnGkBNgTPGwf3t_2z8-dxoIwVFwHGWJF8VNZPRWfhG72sQATGANvZpSEyPficfoWZrYY-hyUxjXK2IklOJIqN1RcVEupktv7xoUZCwk-Xkty6pcL8pZWVWz5WxZz-p6Xq2qef0AXxkTBoywNT84uP5HNMsAv-TQTC5CGKFhT81ZGIGl7vRWmIGhGc8OhqsOK6zPHlOAoX-lIQbOt-n6C6QOjKs)

Teorema: Semántica local ⇔ semántica global

---

## Manta de Markov

Cada nodo es condicionalmente independiente de todos los demás dados su manta de Markov: padres + hijos + padres de los hijos

![width:700px](https://mermaid.ink/img/pako:eNptkMFqwzAMhl9F-NyCX2DQQ7dDYYceetu1h9hKG4iTYDsbjPDunVOWjK2XIPTp1y_9E8zWoYKBeotH-LLetmDZOTJOohNDyYVmOqnGkBNgTPGwf3t_2z8-dxoIwVFwHGWJF8VNZPRWfhG72sQATGANvZpSEyPficfoWZrYY-hyUxjXK2IklOJIqN1RcVEupktv7xoUZCwk-Xkty6pcL8pZWVWz5WxZz-p6Xq2qef0AXxkTBoywNT84uP5HNMsAv-TQTC5CGKFhT81ZGIGl7vRWmIGhGc8OhqsOK6zPHlOAoX-lIQbOt-n6C6QOjKs)

---

## Construcción de redes bayesianas

Método para garantizar la semántica global requerida:

1. Elegir un ordenamiento de variables X1, ..., Xn
2. Para i = 1 hasta n
   - Agregar Xi a la red
   - Seleccionar padres de X1, ..., Xi−1 tales que P(Xi|Padres(Xi)) = P(Xi|X1, ..., Xi−1)

Esta elección de padres garantiza la semántica global:
P(X1, ..., Xn) = Πn i=1 P(Xi|X1, ..., Xi−1) (regla de la cadena)
               = Πn i=1 P(Xi|Padres(Xi)) (por construcción)

---

## Ejemplo: Red de seguro de automóvil

![width:900px](https://mermaid.ink/img/pako:eNqNk91uwjAMhV8l8nUn9gK9QBoSiLHLXVWaxI1FkpYkZUMT7z5nLYy1dLsiiXN8bH_-WZJjR1zCmFhNA7oqY2XQdtqhmkrrEhfPtQXFEmxoWudnATRKh8LhoHCoLDGT0jowXOpVIqNODLZlcyX9z0vz_Zp2qtMHiU2nfE70bWTQmjQ46PzZm0QnYRZsBm2LhSgL-R8t5FBaHWQODZGb2S-yHNRplBZtB7EYwVPFXnXZA2xMUUPBLnvNwgimKRgnSoYgIQDSGKVAkWELx10qBcdGRIENRPBq0DQsG7uCUaGVILsjDYEsRXnZZ5Eg1DgLe4qbFzBLjNGe6OuYbFNS9C07TRXPjhU6D7Y1Ju_uHy63FwT3oeJg2N5gXqI91AX3fXL-ZdGmO-xfm5Hhwbhe10_v6-16vX5ar57X2-f1y-Z1s3nE5ehTCh7hzRr9oM7EJHwrUpSuZhZ8FxOo3yw8zKnr3StwpEfDVMKYOIPdSqLHlMIXObAHn-mEtD-oNFMk4VKKzs6pZMrIHOBcSAczsS9VPPc_6dEy4w)

---

## Distribuciones condicionales compactas

- La TPC crece exponencialmente con el número de padres
- La TPC se vuelve infinita con padre o hijo de valor continuo

Solución: distribuciones canónicas que se definen de forma compacta

Los nodos deterministas son el caso más simple:
- X = f(Padres(X)) para alguna función f
- Por ejemplo, funciones booleanas: Norteamericano ⇔ Canadiense ∨ Estadounidense ∨ Mexicano
- Por ejemplo, relaciones numéricas entre variables continuas: ∂Nivel/∂t = entrada + precipitación - salida - evaporación

---

## Distribuciones condicionales compactas (cont.)

Las distribuciones OR-ruidoso modelan múltiples causas no interactuantes:

1. Los padres U1...Uk incluyen todas las causas (se puede agregar nodo de fuga)
2. Probabilidad de fallo independiente qi para cada causa sola

P(X|U1...Uj, ¬Uj+1...¬Uk) = 1 − Πji=1qi

Ejemplo:
![width:500px](https://mermaid.ink/img/pako:eNp9kL1uwzAMhF-F4JyC8AsYHtoOBTp06FZ1ECw6FmBLgiQ7MIK8e-k4aYqiRS-k7nj3kZxh7xwqWJLXdIBPa9mC9449eifOiyJnGumg9o48AU3rYbbaTBfLl0EDoXiOnKMs8a24iUyDlZ_EvjYxABc4Q6-m1MTId-IxepYm9hi63BTG9YoYDaV4Emp3VFyUi-HS27sGBRkLSX5Wy7Iq14tyVlbVbDlb1rO6nlerap7MfmVMGDDC1vzkYPo_zywD_JJDM7kIYYSG92jOwggs9V5vhRkYmvHsYLjqsMb67DEFGPpXGmLgfJuuvwBKcKVm)

Número de parámetros lineal en número de padres

---

## Redes híbridas (discretas+continuas)

![width:700px](https://mermaid.ink/img/pako:eNptkMFqwzAMhl9F-NyCX2DQQ7dDYYceetu1h9hKG4iTYDsbjPDunVOWjK2XIPTp1y_9E8zWoYKBeotH-LLetmDZOTJOohNDyYVmOqnGkBNgTPGwf3t_2z8-dxoIwVFwHGWJF8VNZPRWfhG72sQATGANvZpSEyPficfoWZrYY-hyUxjXK2IklOJIqN1RcVEupktv7xoUZCwk-Xkty6pcL8pZWVWz5WxZz-p6Xq2qef0AXxkTBoywNT84uP5HNMsAv-TQTC5CGKFhT81ZGIGl7vRWmIGhGc8OhqsOK6zPHlOAoX-lIQbOt-n6C6QOjKs)

Opción 1: discretización—posiblemente grandes errores, TPC grandes
Opción 2: familias canónicas con parámetros finitos
1. Variable continua, padres discretos+continuos (por ej., Costo)
2. Variable discreta, padres continuos (por ej., ¿Compra?)

---

## Variables hijo continuas

Se necesita una función de densidad condicional para la variable hijo dados los padres continuos, para cada asignación posible a los padres discretos

El más común es el modelo gaussiano lineal, por ejemplo:
P(Costo = c|Cosecha = h, ¿Subsidio? = verdadero) = N(ath + bt, σt)(c)

El Costo medio varía linealmente con la Cosecha, la varianza es fija
La variación lineal no es razonable en todo el rango pero funciona bien si el rango probable de Cosecha es estrecho

---

## Variables hijo continuas (cont.)

![width:700px](https://i.imgur.com/QY3atnP.png)

Red totalmente continua con distribuciones GL ⇒ la distribución conjunta completa es una gaussiana multivariada
Una red GL discreta+continua es una red gaussiana condicional
es decir, una gaussiana multivariada sobre todas las variables continuas para cada combinación de valores de variables discretas

---

## Variable discreta con padres continuos

La probabilidad de ¿Compra? dado el Costo debería ser un umbral "suave":

La distribución probit usa la integral de la gaussiana: Φ(x) = ∫x−∞ N(0, 1)(x)dx
P(¿Compra? = verdadero | Costo = c) = Φ((−c + µ)/σ)

![width:700px](https://i.imgur.com/QnQI9vU.png)

(a) Una distribución normal (gaussiana) para el umbral de costo, centrada en µ = 6.0 con desviación estándar σ = 1.0.
(b) Modelos expit y probit para la probabilidad de compra dado el costo, para los parámetros µ = 6.0 y σ = 1.0.

---

## ¿Por qué el probit?

1. Tiene más o menos la forma correcta
2. Se puede ver como un umbral duro cuya ubicación está sujeta a ruido

![width:500px](https://mermaid.ink/img/pako:eNptkMFqwzAMhl9F-NyCX2DQQ7dDYYceetu1h9hKG4iTYDsbjPDunVOWjK2XIPTp1y_9E8zWoYKBeotH-LLetmDZOTJOohNDyYVmOqnGkBNgTPGwf3t_2z8-dxoIwVFwHGWJF8VNZPRWfhG72sQATGANvZpSEyPficfoWZrYY-hyUxjXK2IklOJIqN1RcVEupktv7xoUZCwk-Xkty6pcL8pZWVWz5WxZz-p6Xq2qef0AXxkTBoywNT84uP5HNMsAv-TQTC5CGKFhT81ZGIGl7vRWmIGhGc8OhqsOK6zPHlOAoX-lIQbOt-n6C6QOjKs)

---

## Variable discreta (cont.)

La distribución sigmoide (o logit) también se usa en redes neuronales:
P(¿Compra? = verdadero | Costo = c) = 1 / (1 + exp(−2(−c+µ)/σ))

La sigmoide tiene una forma similar al probit pero con colas mucho más largas:

![width:600px](https://i.imgur.com/QnQI9vU.png)

---

## Inferencia Exacta en Redes Bayesianas

Consultas simples: calcular la marginal posterior P(Xi|E = e)
por ej., P(SinGasolina|Medidor = vacío, Luces = encendidas, Arranca = falso)

Consultas conjuntivas: P(Xi, Xj|E = e) = P(Xi|E = e)P(Xj|Xi, E = e)

Decisiones óptimas: las redes de decisión incluyen información de utilidad;
se requiere inferencia probabilística para P(resultado|acción, evidencia)

Valor de la información: ¿qué evidencia buscar a continuación?

Análisis de sensibilidad: ¿qué valores de probabilidad son más críticos?

Explicación: ¿por qué necesito un nuevo motor de arranque?

---

## Inferencia por enumeración

Forma ligeramente inteligente de sumar variables de la conjunta sin construir realmente su representación explícita

Consulta simple en la red de robo:

P(B|j, m) = P(B, j, m)/P(j, m) = αP(B, j, m)
          = α Σe Σa P(B, e, a, j, m)

Reescribir entradas conjuntas completas usando el producto de entradas de TPC:

P(B|j, m) = α Σe Σa P(B)P(e)P(a|B, e)P(j|a)P(m|a)
          = αP(B) Σe P(e) Σa P(a|B, e)P(j|a)P(m|a)

Enumeración recursiva en profundidad: O(n) espacio, O(d^n) tiempo

---

## Algoritmo de enumeración

```python
función Preguntar-Enumeración(X, e, rb) devuelve una distribución sobre X
    entradas: X, la variable de consulta
              e, valores observados para variables E
              rb, una red bayesiana con variables {X} ∪ E ∪ Y
    Q(X) ← una distribución sobre X, inicialmente vacía
    para cada valor xi de X hacer
        extender e con el valor xi para X
        Q(xi) ← Enumerar-Todo(Vars[rb], e)
    devolver Normalizar(Q(X))

función Enumerar-Todo(vars, e) devuelve un número real
    si Vacía?(vars) entonces devolver 1.0
    Y ← Primero(vars)
    si Y tiene valor y en e
        entonces devolver P(y | Pa(Y)) × Enumerar-Todo(Resto(vars), e)
        si no devolver Σy P(y | Pa(Y)) × Enumerar-Todo(Resto(vars), ey)
                 donde ey es e extendido con Y = y
```

---

## Árbol de evaluación

![width:900px](https://i.imgur.com/QnQI9vU.png)

La enumeración es ineficiente: cómputo repetido
por ej., calcula P(j|a)P(m|a) para cada valor de e

---

## Inferencia por eliminación de variables

Eliminación de variables: realizar las sumas de derecha a izquierda,
almacenando resultados intermedios (factores) para evitar recálculos

P(B|j, m) = α P(B) Σe P(e) Σa P(a|B, e) P(j|a) P(m|a)
          = αP(B)ΣeP(e)ΣaP(a|B, e)fJ(a)fM(a)
          = αP(B)ΣeP(e)fA̅JM(b, e) (sumar A)
          = αP(B)fE̅A̅JM(b) (sumar E)
          = αfB(b) × fE̅A̅JM(b)

---

## Eliminación de variables: Operaciones básicas

Sumar una variable de un producto de factores:
- Mover cualquier factor constante fuera de la suma
- Sumar submatrices en el producto punto a punto de los factores restantes

Σx f1 × · · · × fk = f1 × · · · × fi Σx fi+1 × · · · × fk = f1 × · · · × fi × fX̅

asumiendo que f1, ..., fi no dependen de X

Producto punto a punto de factores f1 y f2:
f1(x1, ..., xj, y1, ..., yk) × f2(y1, ..., yk, z1, ..., zl)
= f(x1, ..., xj, y1, ..., yk, z1, ..., zl)

Por ej., f1(a, b) × f2(b, c) = f(a, b, c)

---

## Algoritmo de eliminación de variables

```python
función Preguntar-Eliminación(X, e, rb) devuelve una distribución sobre X
    entradas: X, la variable de consulta
              e, evidencia especificada como un evento
              rb, una red de creencias que especifica la distribución conjunta P(X1, ..., Xn)
    factores ← []
    vars ← Invertir(Vars[rb])
    para cada var en vars hacer
        factores ← [Hacer-Factor(var, e)|factores]
        si var es una variable oculta entonces factores ← Sumar-Fuera(var, factores)
    devolver Normalizar(Producto-Punto-a-Punto(factores))
```

---

## Variables irrelevantes

Considera la consulta P(JuanLlama|Ladrón = verdadero)

P(J|b) = αP(b) Σe P(e) Σa P(a|b, e)P(J|a) Σm P(m|a)

La suma sobre m es idénticamente 1; M es irrelevante para la consulta

Teorema 1: Y es irrelevante a menos que Y ∈ Antecesores({X} ∪ E)
Aquí, X = JuanLlama, E = {Ladrón}, y
Antecesores({X} ∪ E) = {Alarma, Terremoto}
así que MaríaLlama es irrelevante

(Compara esto con el encadenamiento hacia atrás desde la consulta en BCs de cláusulas de Horn)

---

## Variables irrelevantes (cont.)

Def: grafo moral de una red bayesiana: casar todos los padres y quitar flechas
Def: A está m-separado de B por C si está separado por C en el grafo moral

Teorema 2: Y es irrelevante si está m-separado de X por E

![width:600px](https://mermaid.ink/img/pako:eNptkMFqwzAMhl9F-NyCX2DQQ7dDYYceetu1h9hKG4iTYDsbjPDunVOWjK2XIPTp1y_9E8zWoYKBeotH-LLetmDZOTJOohNDyYVmOqnGkBNgTPGwf3t_2z8-dxoIwVFwHGWJF8VNZPRWfhG72sQATGANvZpSEyPficfoWZrYY-hyUxjXK2IklOJIqN1RcVEupktv7xoUZCwk-Xkty6pcL8pZWVWz5WxZz-p6Xq2qef0AXxkTBoywNT84uP5HNMsAv-TQTC5CGKFhT81ZGIGl7vRWmIGhGc8OhqsOK6zPHlOAoX-lIQbOt-n6C6QOjKs)

Para P(JuanLlama|Alarma = verdadero), tanto Ladrón como Terremoto son irrelevantes

---

## Complejidad de la inferencia exacta

Redes con conexión simple (o politrees):
- Cualesquiera dos nodos están conectados por a lo sumo un camino (no dirigido)
- El costo de tiempo y espacio de la eliminación de variables es O(d^kn)

Redes con conexión múltiple:
- Se puede reducir 3SAT a inferencia exacta ⇒ NP-duro
- Equivalente a contar modelos 3SAT ⇒ #P-completo

![width:400px](https://mermaid.ink/img/pako:eNptkMFqwzAMhl9F-NyCX2DQQ7dDYYceetu1h9hKG4iTYDsbjPDunVOWjK2XIPTp1y_9E8zWoYKBeotH-LLetmDZOTJOohNDyYVmOqnGkBNgTPGwf3t_2z8-dxoIwVFwHGWJF8VNZPRWfhG72sQATGANvZpSEyPficfoWZrYY-hyUxjXK2IklOJIqN1RcVEupktv7xoUZCwk-Xkty6pcL8pZWVWz5WxZz-p6Xq2qef0AXxkTBoywNT84uP5HNMsAv-TQTC5CGKFhT81ZGIGl7vRWmIGhGc8OhqsOK6zPHlOAoX-lIQbOt-n6C6QOjKs)

---

## Inferencia Aproximada para Redes Bayesianas

Idea básica:
1. Extraer N muestras de una distribución de muestreo S
2. Calcular una probabilidad posterior aproximada P̂
3. Mostrar que esto converge a la probabilidad verdadera P

Esquema:
- Muestreo de una red vacía
- Muestreo por rechazo: rechazar muestras que no concuerden con la evidencia
- Ponderación por verosimilitud: usar evidencia para ponderar muestras
- Cadena de Markov Monte Carlo (MCMC): muestrear de un proceso estocástico cuya distribución estacionaria es la posterior verdadera

---

## Muestreo de una red vacía

```python
función Muestra-Previa(rb) devuelve un evento muestreado de rb
    entradas: rb, una red de creencias que especifica la distribución conjunta P(X1, ..., Xn)
    x ← un evento con n elementos
    para i = 1 hasta n hacer
        xi ← una muestra aleatoria de P(Xi | padres(Xi))
               dados los valores de Padres(Xi) en x
    devolver x
```

---

## Ejemplo: Muestreo de la Red del Aspersor

![width:700px](https://mermaid.ink/img/pako:eNp1kc1uwjAQhF_F8hUk3oDDgVaVeujvpVKFnExiiBXHjuwNqhDvXidASwM-efabWe96T1A4TxpyaAN94oeV1EYo5f1jofydM9nBmGxRsC6tJWOwZCQZdSCWYNnYe7aDI5iTTqyj7RDnEPJWaErwvBBvcD-_3T3Mb_L5C7wejcOKEgTrGlbGOlIKBh-xGXbCUlD8DPrNZv0CL6enp6dp3hRpkeV5vjhKBU5Lv7vxOJDfb0n1R-pC5x0q2IUmtCe4qbUNKNl50h5C66wwFNqf6ZJC8KFTJwlbLbWGLOXM3Gxr2qxq_0uKzs9KH0Jnw-Qfd4c-mGnU0uNUm3EUq1LhVeAWfPFk-