---
marp: true
theme: default
paginate: true
---

# Problemas de Satisfacción de Restricciones
## Capítulo 5

---

# Esquema

- Definición de Problemas de Satisfacción de Restricciones (CSP)
- Ejemplos de CSP
- Búsqueda con retroceso para CSPs
- Búsqueda local para CSPs
- Estructura del problema y descomposición del problema

---

# Definición de Problemas de Satisfacción de Restricciones

Un problema de satisfacción de restricciones (CSP) consta de tres componentes, X, D y C:

- X es un conjunto de variables, { X1 ….. Xn}
- D es un conjunto de dominios, { D1, …. , Dn}, uno para cada variable 
- C es un conjunto de restricciones que especifican combinaciones permitidas de valores 

Los CSPs tratan con asignaciones de valores a variables:
- Una asignación completa es aquella en la que se asigna un valor a cada variable, y una solución a un CSP es una asignación completa y consistente.
- Una asignación parcial es aquella que deja algunas variables sin asignar.
- Una solución parcial es una asignación parcial que es consistente

---

# Problemas de Satisfacción de Restricciones (CSPs)

Problema de búsqueda estándar:
- El estado es una "caja negra": cualquier estructura de datos que admita prueba de objetivo, evaluación y sucesor

CSP:
- El estado se define por variables Xi con valores del dominio Di
- La prueba de objetivo es un conjunto de restricciones que especifican combinaciones permitidas de valores para subconjuntos de variables

Ejemplo simple de un lenguaje de representación formal:
- Permite algoritmos de propósito general útiles con más poder que los algoritmos de búsqueda estándar

---

# Ejemplo: Colorear el Mapa de Australia Occidental

![bg right:40% 80%](https://i.imgur.com/ZY8dKpJ.png)

Variables: WA, NT, Q, NSW, V, SA, T
Dominios Di = {rojo, verde, azul}

Restricciones: las regiones adyacentes deben tener colores diferentes
Por ejemplo, WA ≠ NT, o 
(WA, NT) ∈ {(rojo, verde), (rojo, azul), (verde, rojo), (verde, azul), ...}

---

# Ejemplo: Colorear el Mapa (continuación)

![bg right:40% 80%](https://i.imgur.com/ZY8dKpJ.png)

Las soluciones son asignaciones que satisfacen todas las restricciones, por ejemplo,
{WA = rojo, NT = verde, Q = rojo, NSW = verde, V = rojo, SA = azul, T = verde}

---

# Grafo de Restricciones

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

- CSP binario: cada restricción relaciona como máximo dos variables
- Grafo de restricciones: los nodos son variables, los arcos muestran restricciones
- Los algoritmos de CSP de propósito general usan la estructura del grafo para acelerar la búsqueda. Por ejemplo, ¡Tasmania es un subproblema independiente!

---

# Variedades de CSPs

1. Variables discretas
   - Dominios finitos; tamaño d ⇒ O(d^n) asignaciones completas
   - Por ejemplo, CSPs booleanos, incluyendo satisfacibilidad booleana (NP-completo)
   - Dominios infinitos (enteros, cadenas, etc.)
     - Por ejemplo, programación de trabajos, las variables son días de inicio/fin para cada trabajo
     - Se necesita un lenguaje de restricciones, por ejemplo, InicioTrabajo1 + 5 ≤ InicioTrabajo3
     - Restricciones lineales son resolubles, las no lineales son indecidibles

2. Variables continuas
   - Por ejemplo, tiempos de inicio/fin para observaciones del Telescopio Hubble
   - Restricciones lineales resolubles en tiempo polinómico mediante métodos de PL

---

# Variedades de Restricciones

1. Restricciones unarias involucran una sola variable, por ejemplo, SA ≠ verde
2. Restricciones binarias involucran pares de variables, por ejemplo, SA ≠ WA
3. Restricciones de orden superior involucran 3 o más variables, por ejemplo, restricciones de columna en criptoaritmética
4. Preferencias (restricciones blandas), por ejemplo, rojo es mejor que verde
   - A menudo representables por un costo para cada asignación de variable
   - → problemas de optimización con restricciones

---

# Ejemplo: Criptoaritmética

![bg right:40% 80%](https://i.imgur.com/JGkHzZC.png)

Variables: F T U W R O X1 X2 X3
Dominios: {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
Restricciones:
- alldiff(F, T, U, W, R, O)
- O + O = R + 10 · X1, etc.

---

# CSPs del mundo real

- Problemas de asignación (por ejemplo, quién da qué clase)
- Problemas de horarios (por ejemplo, ¿qué clase se ofrece cuándo y dónde?)
- Configuración de hardware
- Hojas de cálculo
- Programación de transporte
- Programación de fábricas
- Planificación de espacios

Notá que muchos problemas del mundo real involucran variables de valor real

---

# Formulación de Búsqueda Estándar (Incremental)

Empecemos con el enfoque directo y simple, luego lo arreglaremos:

Los estados se definen por los valores asignados hasta el momento:
- Estado inicial: la asignación vacía, { }
- Función sucesora: asigna un valor a una variable no asignada que no entre en conflicto con la asignación actual.
  - Falla si no hay asignaciones legales (¡no se puede arreglar!)
- Prueba de objetivo: la asignación actual está completa

1. ¡Esto es lo mismo para todos los CSPs!
2. Cada solución aparece a profundidad n con n variables ⇒ usar búsqueda en profundidad
3. El camino es irrelevante, por lo que también se puede usar la formulación de estado completo
4. b = (n - ℓ)d a profundidad ℓ, ¡¡¡por lo tanto n!d^n hojas!!!!

---

# Búsqueda con Retroceso

- Las asignaciones de variables son conmutativas, es decir, [WA = rojo luego NT = verde] es lo mismo que [NT = verde luego WA = rojo]
- Solo hay que considerar asignaciones a una sola variable en cada nodo ⇒ b = d y hay d^n hojas
- La búsqueda en profundidad para CSPs con asignaciones de una sola variable se llama búsqueda con retroceso
- La búsqueda con retroceso es el algoritmo básico no informado para CSPs
- Puede resolver n-reinas para n ≈ 25

---

# Función de Búsqueda con Retroceso

```python
función Búsqueda-Con-Retroceso(csp) devuelve solución/fallo
    devolver Retroceso-Recursivo({}, csp)

función Retroceso-Recursivo(asignación, csp) devuelve solución/fallo
    si asignación está completa entonces devolver asignación
    var ← Seleccionar-Variable-No-Asignada(Variables[csp], asignación, csp)
    para cada valor en Ordenar-Valores-Dominio(var, asignación, csp) hacer
        si valor es consistente con asignación dadas Restricciones[csp] entonces
            agregar {var = valor} a asignación
            resultado ← Retroceso-Recursivo(asignación, csp)
            si resultado ≠ fallo entonces devolver resultado
            quitar {var = valor} de asignación
    devolver fallo
```

---

# Ejemplo de Retroceso

![bg 80%](https://i.imgur.com/nTtZxyz.png)

---

# Mejorando la Eficiencia del Retroceso

Los métodos de propósito general pueden dar grandes ganancias en velocidad:

1. ¿Qué variable debería asignarse a continuación?
2. ¿En qué orden deberían probarse sus valores?
3. ¿Podemos detectar el fracaso inevitable temprano?
4. ¿Podemos aprovechar la estructura del problema?

---

# Valores Mínimos Restantes

Valores mínimos restantes (MRV):
- Elegir la variable con la menor cantidad de valores legales

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

---

# Heurística de Grado

Desempate entre variables MRV:
- Heurística de grado: elegir la variable con más restricciones sobre las variables restantes

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

---

# Valor Menos Restrictivo

Dada una variable, elegir el valor menos restrictivo:
- El que descarta la menor cantidad de valores en las variables restantes

![bg right:40% 80%](https://i.imgur.com/JGkHzZC.png)

Combinar estas heurísticas hace factible 1000 reinas

---

# Verificación hacia adelante

Idea: Mantener un registro de los valores legales restantes para variables no asignadas
Terminar la búsqueda cuando cualquier variable no tenga valores legales

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

---

# Propagación de Restricciones

La verificación hacia adelante propaga información de variables asignadas a no asignadas, pero no proporciona detección temprana para todos los fallos:

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

¡NT y SA no pueden ser ambos azules!

La propagación de restricciones aplica restricciones localmente de forma repetida

---

# Consistencia de Arco

La forma más simple de propagación hace que cada arco sea consistente

X → Y es consistente si y solo si para cada valor x de X hay algún y permitido

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

Si X pierde un valor, los vecinos de X deben ser revisados nuevamente

La consistencia de arco detecta fallos antes que la verificación hacia adelante
Se puede ejecutar como preprocesador o después de cada asignación

---

# Algoritmo de Consistencia de Arco

```python
función AC-3(csp) devuelve el CSP, posiblemente con dominios reducidos
    entradas: csp, un CSP binario con variables {X1, X2, ..., Xn}
    variables locales: cola, una cola de arcos, inicialmente todos los arcos en csp
    mientras cola no esté vacía hacer
        (Xi, Xj) ← Quitar-Primero(cola)
        si Quitar-Valores-Inconsistentes(Xi, Xj) entonces
            para cada Xk en Vecinos[Xi] hacer
                agregar (Xk, Xi) a cola

función Quitar-Valores-Inconsistentes(Xi, Xj) devuelve verdadero si tiene éxito
    quitado ← falso
    para cada x en Dominio[Xi] hacer
        si no hay valor y en Dominio[Xj] que permita que (x,y) satisfaga la restricción Xi↔Xj
            entonces eliminar x de Dominio[Xi]; quitado ← verdadero
    devolver quitado
```

O(n^2d^3), se puede reducir a O(n^2d^2) (pero detectar todo es NP-hard)

---

# Búsqueda Local para CSPs

- Los algoritmos de búsqueda local pueden ser muy efectivos para resolver muchos CSPs
- Usan una formulación de estado completo donde cada estado asigna un valor a cada variable
- La búsqueda cambia el valor de una variable a la vez
- Heurística de mínimos conflictos: valor que resulta en el mínimo número de conflictos con otras variables
- Usualmente tiene una serie de mesetas
- Búsqueda en meseta: permitir movimientos laterales a otro estado con el mismo puntaje
- La ponderación de restricciones busca concentrar la búsqueda en restricciones importantes
  - A cada restricción se le da un peso numérico, inicialmente todos 1
  - Los pesos se ajustan incrementando cuando son violados por la asignación actual

---

# Ejemplo: 4-Reinas

- Estados: 4 reinas en 4 columnas (4^4 = 256 estados)
- Operadores: mover reina en columna
- Prueba de objetivo: sin ataques
- Evaluación: h(n) = número de ataques

![bg right:40% 80%](https://i.imgur.com/JGkHzZC.png)

---

# Rendimiento de Mínimos Conflictos

- Dado un estado inicial aleatorio, puede resolver n-reinas en tiempo casi constante para n arbitrario con alta probabilidad (por ejemplo, n = 10.000.000)
- Lo mismo parece ser cierto para cualquier CSP generado aleatoriamente, excepto en un rango estrecho de la relación:

  R = número de restricciones / número de variables

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

---

# Estructura del Problema

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

Tasmania y el continente son subproblemas independientes
Identificables como componentes conectados del grafo de restricciones

---

# Estructura del Problema (continuación)

Supongamos que cada subproblema tiene c variables de un total de n:
- El costo de solución en el peor caso es n/c · d^c, lineal en n

Ejemplo:
- n = 80, d = 2, c = 20
- 2^80 = 4 mil millones de años a 10 millones de nodos/seg
- 4 · 2^20 = 0,4 segundos a 10 millones de nodos/seg

---

# CSPs con Estructura de Árbol

![bg right:40% 80%](https://i.imgur.com/JGkHzZC.png)

Teorema: Si el grafo de restricciones no tiene bucles, el CSP se puede resolver en tiempo O(nd^2)

Comparar con CSPs generales, donde el tiempo en el peor caso es O(d^n)

Esta propiedad también se aplica al razonamiento lógico y probabilístico: un ejemplo importante de la relación entre restricciones sintácticas y la complejidad del razonamiento.

---

# Algoritmo para CSPs con Estructura de Árbol

1. Elegir una variable como raíz, ordenar las variables de la raíz a las hojas de manera que cada nodo padre preceda a sus hijos en el ordenamiento
2. Para j desde n hasta 2, aplicar QuitarInconsistente(Padre(Xj), Xj)
3. Para j desde 1 hasta n, asignar Xj de manera consistente con Padre(Xj)

![bg right:40% 80%](https://i.imgur.com/JGkHzZC.png)

---

# CSPs Casi con Estructura de Árbol

Condicionamiento: instanciar una variable, podar los dominios de sus vecinos

![bg right:40% 80%](https://i.imgur.com/nTtZxyz.png)

Condicionamiento de conjunto de corte: instanciar (de todas las formas posibles) un conjunto de variables de modo que el grafo de restricciones restante sea un árbol

Tamaño del conjunto de corte c ⇒ tiempo de ejecución O(d^c · (n - c)d^2), muy rápido para c pequeño

---

# Algoritmos Iterativos para CSPs

La escalada de colinas y el recocido simulado típicamente trabajan con estados "completos", es decir, todas las variables asignadas

Para aplicar a CSPs:
- Permitir estados con restricciones insatisfechas
- Los operadores reasignan valores de variables

Selección de variable: seleccionar aleatoriamente cualquier variable en conflicto
Selección de valor por heurística de mínimos conflictos: elegir el valor que viola la menor cantidad de restricciones

Es decir, escalada de colinas con h(n) = número total de restricciones violadas

---

# Resumen

- Los CSPs son un tipo especial de problema:
  - Estados definidos por valores de un conjunto fijo de variables
  - Prueba de objetivo definida por restricciones sobre valores de variables
- Retroceso = búsqueda en profundidad con una variable asignada por nodo
- Las heurísticas de ordenamiento de variables y selección de valores ayudan significativamente
- La verificación hacia adelante previene asignaciones que garantizan fallos posteriores
- La propagación de restricciones (por ejemplo, consistencia de arco) realiza trabajo adicional para restringir valores y detectar inconsistencias
- La búsqueda local usando la heurística de mínimos conflictos también se ha aplicado a problemas de satisfacción de restricciones con gran éxito
- La representación CSP permite el análisis de la estructura del problema
- Los CSPs con estructura de árbol se pueden resolver en tiempo lineal
