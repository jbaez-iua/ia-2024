
---
marp: true
theme: default
paginate: true
---

# Inferencia en Lógica de Primer Orden

Capítulo 9

---

# Esquema

- Reducción de inferencia de primer orden a inferencia proposicional
- Unificación
- Modus Ponens Generalizado
- Encadenamiento hacia adelante y hacia atrás
- Programación lógica
- Resolución

---

# Instanciación Universal (UI)

Toda instanciación de una oración cuantificada universalmente está implicada por ella:

∀v α
Subst({v/g}, α)

para cualquier variable v y término de base g

Ejemplo:
∀x Rey(x) ∧ Codicioso(x) ⇒ Malvado(x) produce:
- Rey(Juan) ∧ Codicioso(Juan) ⇒ Malvado(Juan)
- Rey(Ricardo) ∧ Codicioso(Ricardo) ⇒ Malvado(Ricardo)
- Rey(Padre(Juan)) ∧ Codicioso(Padre(Juan)) ⇒ Malvado(Padre(Juan))

---

# Instanciación Existencial (EI)

Para cualquier oración α, variable v, y símbolo constante k que no aparezca en otra parte de la base de conocimientos:

∃v α
Subst({v/k}, α)

Ejemplo:
∃x Corona(x) ∧ EnCabeza(x, Juan) produce:
Corona(C1) ∧ EnCabeza(C1, Juan)

siempre que C1 sea un nuevo símbolo constante, llamado constante de Skolem

Otro ejemplo:
De ∃x d(xy)/dy = xy obtenemos:
d(ey)/dy = ey

siempre que e sea un nuevo símbolo constante

---

# Instanciación Existencial (cont.)

- UI se puede aplicar varias veces para agregar nuevas oraciones; la nueva BC es lógicamente equivalente a la antigua
- EI se puede aplicar una vez para reemplazar la oración existencial; la nueva BC no es equivalente a la antigua, pero es satisfacible si y solo si la BC antigua era satisfacible

---

# Reducción a Inferencia Proposicional

Supongamos que la BC contiene solo lo siguiente:

∀x Rey(x) ∧ Codicioso(x) ⇒ Malvado(x)
Rey(Juan)
Codicioso(Juan)
Hermano(Ricardo, Juan)

Instanciando la oración universal de todas las formas posibles, tenemos:

Rey(Juan) ∧ Codicioso(Juan) ⇒ Malvado(Juan)
Rey(Ricardo) ∧ Codicioso(Ricardo) ⇒ Malvado(Ricardo)
Rey(Juan)
Codicioso(Juan)
Hermano(Ricardo, Juan)

La nueva BC está proposicionalizada: los símbolos de proposición son Rey(Juan), Codicioso(Juan), Malvado(Juan), Rey(Ricardo), etc.

---

# Reducción (cont.)

Afirmación: una oración de base* está implicada por la nueva BC si y solo si está implicada por la BC original

Afirmación: toda BC de LPO puede ser proposicionalizada para preservar la implicación

Idea: proposicionalizar BC y consulta, aplicar resolución, devolver resultado

Problema: con símbolos de función, hay infinitos términos de base,
p. ej., Padre(Padre(Padre(Juan)))

Teorema (Herbrand, 1930): Si una oración α está implicada por una BC de LPO, está implicada por un subconjunto finito de la BC proposicional

Idea: Para n = 0 hasta ∞ hacer
crear una BC proposicional instanciando con términos de profundidad n
ver si α está implicada por esta BC

Problema: funciona si α está implicada, entra en bucle si α no está implicada

Teorema (Turing, 1936; Church, 1936): La implicación en LPO es semidecidible

---

# Problemas con la Proposicionalización

La proposicionalización parece generar muchas oraciones irrelevantes. Por ejemplo, de:

∀x Rey(x) ∧ Codicioso(x) ⇒ Malvado(x)
Rey(Juan)
∀y Codicioso(y)
Hermano(Ricardo, Juan)

Parece obvio que Malvado(Juan), pero la proposicionalización produce muchos hechos como Codicioso(Ricardo) que son irrelevantes

Con p predicados k-arios y n constantes, hay p · n^k instanciaciones

Con símbolos de función, ¡se vuelve mucho peor!

---

# Unificación

Podemos obtener la inferencia inmediatamente si podemos encontrar una sustitución θ tal que Rey(x) y Codicioso(x) coincidan con Rey(Juan) y Codicioso(y)

θ = {x/Juan, y/Juan} funciona

Unificar(α, β) = θ si αθ = βθ

Ejemplos:
1. Sabe(Juan, x) | Sabe(Juan, Juana) | θ = {x/Juana}
2. Sabe(Juan, x) | Sabe(y, OJ) | θ = {x/OJ, y/Juan}
3. Sabe(Juan, x) | Sabe(y, Madre(y)) | θ = {y/Juan, x/Madre(Juan)}
4. Sabe(Juan, x) | Sabe(x, OJ) | falla

La estandarización aparte elimina la superposición de variables, p. ej., Sabe(z17, OJ)

---

# Modus Ponens Generalizado (MPG)

p1', p2', ..., pn', (p1 ∧ p2 ∧ ... ∧ pn ⇒ q)
-----------------------------------------------
                    qθ

donde pi'θ = piθ para todo i

Ejemplo:
p1' es Rey(Juan)
p2' es Codicioso(y)
p1 es Rey(x)
p2 es Codicioso(x)
θ es {x/Juan, y/Juan}
q es Malvado(x)
qθ es Malvado(Juan)

MPG se usa con BC de cláusulas definidas (exactamente un literal positivo)
Todas las variables se asumen cuantificadas universalmente

---

# Solidez de MPG

Necesitamos demostrar que:
p1', ..., pn', (p1 ∧ ... ∧ pn ⇒ q) |= qθ
siempre que pi'θ = piθ para todo i

Lema: Para cualquier cláusula definida p, tenemos p |= pθ por UI

1. (p1 ∧ ... ∧ pn ⇒ q) |= (p1 ∧ ... ∧ pn ⇒ q)θ = (p1θ ∧ ... ∧ pnθ ⇒ qθ)
2. p1', ..., pn' |= p1' ∧ ... ∧ pn' |= p1'θ ∧ ... ∧ pn'θ
3. De 1 y 2, qθ se sigue por Modus Ponens ordinario

---

# Ejemplo de Base de Conocimientos

La ley dice que es un crimen para un estadounidense vender armas a naciones hostiles. El país Nono, un enemigo de Estados Unidos, tiene algunos misiles, y todos sus misiles le fueron vendidos por el Coronel West, que es estadounidense.

Demostrar que el Coronel West es un criminal

---

# Ejemplo de Base de Conocimientos (cont.)

1. ... es un crimen para un estadounidense vender armas a naciones hostiles:
   Estadounidense(x) ∧ Arma(y) ∧ Vende(x,y,z) ∧ Hostil(z) ⇒ Criminal(x)

2. Nono ... tiene algunos misiles:
   Posee(Nono, M1) y Misil(M1)

3. ... todos sus misiles le fueron vendidos por el Coronel West:
   ∀x Misil(x) ∧ Posee(Nono, x) ⇒ Vende(West, x, Nono)

4. Los misiles son armas:
   Misil(x) ⇒ Arma(x)

5. Un enemigo de Estados Unidos cuenta como "hostil":
   Enemigo(x, EstadosUnidos) ⇒ Hostil(x)

6. West, que es estadounidense ...:
   Estadounidense(West)

7. El país Nono, un enemigo de Estados Unidos ...:
   Enemigo(Nono, EstadosUnidos)

---

# Algoritmo de Encadenamiento hacia Adelante

```python
función LPO-EA-Preguntar(BC, α) devuelve una sustitución o falso
    repetir hasta que nuevo esté vacío
        nuevo ← { }
        para cada oración r en BC hacer
            (p1 ∧ ... ∧ pn ⇒ q) ← Estandarizar-Aparte(r)
            para cada θ tal que (p1' ∧ ... ∧ pn')θ = (p1 ∧ ... ∧ pn)θ
                para algún p1', ..., pn' en BC
                    q' ← Sust(θ, q)
                    si q' no es un renombramiento de una oración ya en BC o nuevo entonces hacer
                        agregar q' a nuevo
                        φ ← Unificar(q', α)
                        si φ no es fallo entonces devolver φ
        agregar nuevo a BC
    devolver falso
```

---

# Demostración de Encadenamiento hacia Adelante

![Demostración de Encadenamiento hacia Adelante](https://i.imgur.com/hQplNLs.png)

---

# Propiedades del Encadenamiento hacia Adelante

- Sonoro y completo para cláusulas definidas de primer orden
- Datalog = cláusulas definidas de primer orden + sin funciones (p. ej., BC de crimen)
- EA termina para Datalog en iteraciones polinómicas: como máximo p · n^k literales
- Puede no terminar en general si α no está implicada
- Esto es inevitable: la implicación con cláusulas definidas es semidecidible

---

# Eficiencia del Encadenamiento hacia Adelante

- Observación simple: no es necesario hacer coincidir una regla en la iteración k si una premisa no se agregó en la iteración k − 1
  ⇒ hacer coincidir cada regla cuya premisa contiene un literal recién agregado
- El emparejamiento en sí puede ser costoso
- La indexación de bases de datos permite recuperación O(1) de hechos conocidos
  p. ej., la consulta Misil(x) recupera Misil(M1)
- Hacer coincidir premisas conjuntivas con hechos conocidos es NP-difícil
- El encadenamiento hacia adelante se usa ampliamente en bases de datos deductivas

---

# Ejemplo de Emparejamiento Difícil

![Ejemplo de Emparejamiento Difícil](https://i.imgur.com/QZ8Z8Zq.png)

Coloreable() se infiere si y solo si el CSP tiene una solución
Los CSP incluyen 3SAT como un caso especial, por lo tanto el emparejamiento es NP-difícil

---

# Algoritmo de Encadenamiento hacia Atrás

```python
función LPO-EA-Preguntar(BC, metas, θ) devuelve un conjunto de sustituciones
    entradas: BC, una base de conocimientos
              metas, una lista de conjunciones que forman una consulta (θ ya aplicado)
              θ, la sustitución actual, inicialmente la sustitución vacía { }
    variables locales: respuestas, un conjunto de sustituciones, inicialmente vacío
    
    si metas está vacío entonces devolver {θ}
    q' ← Sust(θ, Primero(metas))
    para cada oración r en BC
        donde Estandarizar-Aparte(r) = (p1 ∧ ... ∧ pn ⇒ q)
        y θ' ← Unificar(q, q') tiene éxito
            nuevas_metas ← [p1, ..., pn|Resto(metas)]
            respuestas ← LPO-EA-Preguntar(BC, nuevas_metas, Componer(θ', θ)) ∪ respuestas
    devolver respuestas
```

---

# Ejemplo de Encadenamiento hacia Atrás

![Ejemplo de Encadenamiento hacia Atrás](https://i.imgur.com/hQplNLs.png)

---

# Propiedades del Encadenamiento hacia Atrás

- Búsqueda de prueba recursiva en profundidad: el espacio es lineal en el tamaño de la prueba
- Incompleto debido a bucles infinitos
  ⇒ se soluciona verificando la meta actual contra cada meta en la pila
- Ineficiente debido a submetas repetidas (tanto éxito como fracaso)
  ⇒ se soluciona usando caché de resultados anteriores (¡espacio extra!)
- Ampliamente utilizado (¡sin mejoras!) para programación lógica

---

# Programación Lógica

Resumen: cómputo como inferencia en BC lógicas

| Programación Lógica | Programación Ordinaria |
|---------------------|------------------------|
| 1. Identificar problema | Identificar problema |
| 2. Reunir información | Reunir información |
| 3. Pausa para el té | Idear solución |
| 4. Codificar información en BC | Programar solución |
| 5. Codificar instancia del problema como hechos | Codificar instancia del problema como datos |
| 6. Hacer consultas | Aplicar programa a datos |
| 7. Encontrar hechos falsos | Depurar errores de procedimiento |

Debería ser más fácil depurar Capital(NuevaYork, EEUU) que x := x + 2!

---

# Sistemas Prolog

Base: encadenamiento hacia atrás con cláusulas de Horn + características adicionales
- Ampliamente utilizado en Europa, Japón (base del proyecto de 5ª Generación)
- Técnicas de compilación ⇒ acercándose a mil millones de LIPS

Programa = conjunto de cláusulas = cabeza :- literal1, ..., literaln.
```prolog
criminal(X) :- estadounidense(X), arma(Y), vende(X,Y,Z), hostil(Z).
```

- Unificación eficiente mediante codificación abierta
- Recuperación eficiente de cláusulas coincidentes mediante enlace directo
- Encadenamiento hacia atrás en profundidad, de izquierda a derecha
- Predicados incorporados para aritmética, etc., p. ej., X is Y*Z+3
- Suposición de mundo cerrado ("negación como falla")
  p. ej., dado vivo(X) :- not muerto(X).
  vivo(jose) tiene éxito si muerto(jose) falla

---

# Ejemplos de Prolog

Búsqueda en profundidad desde un estado inicial X:
```prolog
bep(X) :- meta(X).
bep(X) :- sucesor(X,S), bep(S).
```
No es necesario iterar sobre S: sucesor tiene éxito para cada uno

Concatenar dos listas para producir una tercera:
```prolog
concatenar([], Y, Y).
concatenar([X|L], Y, [X|Z]) :- concatenar(L, Y, Z).
```
consulta: concatenar(A,B,[1,2]) ?
respuestas: A=[] B=[1,2]
            A=[1] B=[2]
            A=[1,2] B=[]

---

# Resolución: Resumen Breve

Versión completa de primer orden:

```
l1 ∨ · · · ∨ lk, m1 ∨ · · · ∨ mn
(l1 ∨ · · · ∨ li−1 ∨ li+1 ∨ · · · ∨ lk ∨ m1 ∨ · · · ∨ mj−1 ∨ mj+1 ∨ · · · ∨ mn)θ
```

donde Unificar(li, ¬mj) = θ.

Por ejemplo:
```
¬Rico(x) ∨ Infeliz(x)
Rico(Ken)
--------------------
Infeliz(Ken)
```
con θ = {x/Ken}

Aplicar pasos de resolución a FNC (BC ∧ ¬α); completo para LPO

---

# Conversión a FNC

1. Eliminar bicondicionales e implicaciones
2. Mover ¬ hacia adentro: ¬∀x p ≡ ∃x ¬p, ¬∃x p ≡ ∀x ¬p
3. Estandarizar variables: cada cuantificador debe usar una diferente
4. Skolemizar: reemplazar variables existenciales con funciones de Skolem
5. Eliminar cuantificadores universales
6. Distribuir ∧ sobre ∨

Ejemplo:
"Todos los que aman a todos los animales son amados por alguien"

1. ∀x[∀y Animal(y) ⇒ Ama(x,y)] ⇒ [∃y Ama(y,x)]
2. ∀x[∃y Animal(y) ∧ ¬Ama(x,y)] ∨ [∃z Ama(z,x)]
3. ∀x[∃y Animal(y) ∧ ¬Ama(x,y)] ∨ [∃z Ama(z,x)]
4. ∀x[Animal(F(x)) ∧ ¬Ama(x,F(x))] ∨ Ama(G(x),x)
5. [Animal(F(x)) ∧ ¬Ama(x,F(x))] ∨ Ama(G(x),x)
6. [Animal(F(x)) ∨ Ama(G(x),x)] ∧ [¬Ama(x,F(x)) ∨ Ama(G(x),x)]

---

# Demostración de Resolución: Cláusulas Definidas

![Demostración de Resolución](https://i.imgur.com/hQplNLs.png)

---

# Teorema de Incompletitud de Gödel

- Existen oraciones aritméticas verdaderas que no se pueden demostrar
- Para cualquier conjunto de oraciones verdaderas de la teoría de números, y en particular cualquier conjunto de axiomas básicos, hay otras oraciones verdaderas que no se pueden demostrar a partir de esos axiomas.
- Nunca podremos probar todos los teoremas de las matemáticas dentro de ningún sistema dado de axiomas.

---

# Estrategias de Resolución

- Preferencia de unidad: prefiere hacer resoluciones donde una de las oraciones es un solo literal (cláusula unitaria)
- Conjunto de soporte: cada paso de resolución involucra al menos un elemento de un conjunto especial de cláusulas
- Resolución de entrada: cada resolución combina una de las oraciones de entrada de la BC con otras oraciones
- Subsunción: elimina todas las oraciones que están subsumidas por oraciones de la BC
- Aprendizaje: aprender de la experiencia (aprendizaje automático)

---

# Resumen

- La unificación identifica sustituciones apropiadas para variables, eliminando el paso de instanciación en pruebas de primer orden, haciendo el proceso más eficiente en muchos casos
- El encadenamiento hacia adelante se usa en bases de datos deductivas, donde se puede combinar con operaciones de bases de datos relacionales. También se usa en sistemas de producción
- El encadenamiento hacia atrás se usa en sistemas de programación lógica, que emplean tecnología de compilador sofisticada para proporcionar inferencia muy rápida
- Prolog, a diferencia de la lógica de primer orden, usa un mundo cerrado con la suposición de nombres únicos y negación como falla.
- La regla de inferencia de resolución generalizada proporciona un sistema de prueba completo para la lógica de primer orden, usando bases de conocimientos en forma normal conjuntiva.

```

Notas sobre la traducción:

1. Términos específicos:
   - "Modus Ponens Generalizado" se mantuvo como tal, ya que es un término técnico utilizado en lógica.
   - "Skolem constant" se tradujo como "constante de Skolem", que es el término usado en español.
   - "LIPS" (Logical Inferences Per Second) se mantuvo en inglés, ya que es una abreviatura técnica.

2. Adaptaciones culturales:
   - Los nombres propios como "John" y "Richard" se tradujeron a sus equivalentes en español "Juan" y "Ricardo" para mantener la coherencia con el uso del español argentino.
   - "America" se tradujo como "Estados Unidos" cuando se refería al país, para evitar ambigüedades.

3. Desafíos en la traducción:
   - La traducción de términos técnicos de lógica y programación requirió cuidado para mantener la precisión y el significado original.
   - La adaptación de ejemplos y código fuente para que tengan sentido en español mientras se mantiene su función ilustrativa fue un desafío, especialmente en los ejemplos de Prolog.

4. Aspectos del español argentino:
   - Se utilizó el "voseo" en las instrucciones implícitas, por ejemplo, "Supongamos que la BC contiene solo lo siguiente" en lugar de "Supón que...".
   - Se mantuvieron estructuras formales en la mayoría del texto debido a la naturaleza técnica y académica del contenido.