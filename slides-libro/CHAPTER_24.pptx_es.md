
# Procesamiento del Lenguaje Natural
## Capítulo 24

---

<!-- footer: © 2022 Pearson Education Ltd. -->

# Esquema

- Modelos de Lenguaje
- Gramática
- Análisis Sintáctico
- Gramáticas Aumentadas
- Complejidades del Lenguaje Natural Real
- Tareas de Lenguaje Natural

---

# Modelos de Lenguaje

- Los juicios sobre el lenguaje varían de persona a persona y de tiempo en tiempo
- El lenguaje natural es ambiguo y vago
- El mapeo de símbolos a objetos no está formalmente definido
- Modelo de lenguaje: una distribución de probabilidad que describe la probabilidad de cualquier cadena

---

# El modelo de bolsa de palabras

- La aplicación de Naive Bayes a cadenas de palabras
- Modelo generativo que describe un proceso para generar una oración

Dada una oración que consiste en las palabras w1, w2, ..., wN:
1. Cada categoría tiene una bolsa llena de palabras
2. Para generar texto, primero seleccioná una de las bolsas y descartá las otras
3. Meté la mano en esa bolsa y sacá una palabra al azar

> El proceso de dividir un texto en una secuencia de palabras se llama **tokenización**

---

# Modelos de palabras n-gramas

Hacer que una palabra dependa de todas las palabras anteriores en una oración:
- Captura todas las interacciones posibles entre palabras, pero no es práctico
- Para un vocabulario de 100.000 palabras y una longitud de oración de 40, este modelo tendría 10^200 parámetros para estimar

Compromiso con un modelo de cadena de Markov:
- **modelo n-grama**: una secuencia de símbolos escritos de longitud n
  - Casos especiales: "unigrama" para 1-grama, "bigrama" para 2-grama y "trigrama" para 3-grama
- En un modelo n-grama, la probabilidad de cada palabra depende solo de las n-1 palabras anteriores

---

# Otros modelos n-grama

1. Modelo a nivel de caracteres
   - La probabilidad de cada carácter está determinada por los n-1 caracteres anteriores
   - Útil para:
     - Tratar con palabras desconocidas
     - Idiomas que tienden a unir palabras
     - Tareas de identificación de idioma

2. Modelo de salto de grama
   - Cuenta palabras que están cerca entre sí pero salta una o más palabras entre ellas

---

# Representaciones de palabras

El modelo n-grama pierde generalizaciones porque es un modelo atómico:
- Cada palabra es un átomo, distinto de todas las demás palabras, sin estructura interna

Diccionario: modelo de palabra estructurado
- **WordNet**:
  - Diccionario de código abierto, curado manualmente en formato legible por máquina
  - Ayuda a separar sustantivos de verbos
  - Proporciona categorías básicas

---

# Etiquetado de partes del habla (POS)

- Forma de categorizar palabras (categoría/etiqueta léxica)
- POS permite que los modelos de lenguaje capturen generalizaciones como "los adjetivos generalmente van antes de los sustantivos en inglés"
- Paso útil en muchas otras tareas de PLN, como responder preguntas o traducción

Modelo oculto de Markov (HMM):
- Modelo común para el etiquetado POS
- Modelo generativo que produce lenguaje comenzando en un estado (por ejemplo, IN para preposiciones)
- Dos opciones en cada paso:
  1. Qué palabra debería emitirse
  2. Qué estado debería venir después

---

# Etiquetado POS: Regresión logística

- Los pesos en el modelo de regresión logística corresponden a cuán predictiva es cada característica para cada categoría
- Los valores de los pesos se aprenden mediante descenso de gradiente

Un conjunto de características de etiquetado POS podría incluir:
- verbo (VBP)
- verbo en tiempo pasado (VBD)
- sustantivo (NN)
- verbo en tiempo presente (VBP)

---

![bg right:40% 80%](https://upload.wikimedia.org/wikipedia/commons/8/8e/Penn_Treebank_POS_Tags.jpg)

# Etiquetas de partes del habla

Etiquetas de partes del habla (con una palabra de ejemplo para cada etiqueta) para el corpus Penn Treebank (Marcus et al., 1993).

Nota: "3rd-sing" es una abreviatura de "tercera persona singular del presente".

---

# Gramática

- Una **gramática** es un conjunto de reglas que define la estructura de árbol de frases permitidas
- Un **lenguaje** es el conjunto de oraciones que siguen esas reglas
- Las categorías sintácticas (por ejemplo, frase nominal, frase verbal) ayudan a restringir las palabras probables dentro de una oración
- La estructura de la frase proporciona un marco para el significado o la semántica de la oración

---

# Gramática libre de contexto probabilística (PCFG)

- Una gramática probabilística asigna una probabilidad a cada cadena
- "Libre de contexto" significa que cualquier regla puede usarse en cualquier contexto

Ejemplo: gramática PCFG aplicada al Mundo Wumpus
- Define un pequeño fragmento de inglés adecuado para la comunicación entre agentes que exploran el mundo Wumpus
- Se proporcionan reglas gramaticales con probabilidades

---

# Análisis sintáctico

- El **análisis sintáctico** es el proceso de analizar una cadena de palabras para descubrir su estructura de frase, según las reglas de una gramática
- Buscar un árbol de análisis válido cuyas hojas sean las palabras de la cadena
- Se puede comenzar con el símbolo S y buscar de arriba hacia abajo, o comenzar con las palabras y buscar de abajo hacia arriba

Desafíos:
- Ineficiencia: Si el algoritmo adivina mal, tendrá que retroceder hasta la primera palabra y volver a analizar toda la oración

Soluciones:
- Programación dinámica: almacenar resultados del análisis de subcadenas para evitar reanálisis
- Analizador de tabla: registra resultados en una estructura de datos conocida como tabla

---

# El algoritmo CYK para análisis sintáctico

![bg right:60% 90%](https://upload.wikimedia.org/wikipedia/commons/6/60/CYK_Algorithm_Animation.gif)

---

# Análisis sintáctico: Usando búsqueda A*

- No hay que buscar en todo el espacio de estados
- Se garantiza que el primer análisis encontrado será el más probable (suponiendo una heurística admisible)
- Más rápido que CYK, pero (dependiendo de los detalles de la gramática) aún más lento que O(n)

---

# Análisis sintáctico: Usando búsqueda de haz

- Considerar solo las b alternativas de análisis más probables
- No se garantiza encontrar el análisis con la probabilidad más alta
- El analizador puede operar en tiempo O(n) y aun así encuentra el mejor análisis la mayoría de las veces
- El analizador de búsqueda de haz con b = 1 se llama analizador determinista

Ejemplo: análisis de desplazamiento-reducción
- Recorrer la oración palabra por palabra
- Elegir en cada punto si:
  1. Desplazar la palabra a una pila de constituyentes
  2. Reducir el/los constituyente(s) superior(es) en la pila según una regla gramatical

---

# Análisis de dependencias

Gramática de dependencias:
- Asume que la estructura sintáctica se forma por relaciones binarias entre elementos léxicos, sin necesidad de constituyentes sintácticos
- El árbol de estructura de frase se anota con el núcleo de cada frase
- Se puede recuperar el árbol de dependencias
- Convertir el árbol de dependencias a estructura de frase con categorías arbitrarias

![bg right:40% 90%](https://upload.wikimedia.org/wikipedia/commons/0/0d/Dependency_grammar_tree.png)

---

# Aprendizaje de un analizador a partir de ejemplos

Dado un banco de árboles, crear una PCFG contando el número de veces que aparece cada tipo de nodo en un árbol (con suavizado para conteos bajos)

Ejemplo:
Si hay 1000 nodos S de los cuales 600 son de esta forma, entonces creamos la regla:
```
S → NP VP [0.6]
```

Desafíos:
- Penn Treebank tiene más de 10.000 tipos de nodos diferentes
- Casos especiales como "lo bueno y lo malo" analizados como una sola frase nominal

---

# Otros enfoques para el aprendizaje de analizadores

1. Análisis no supervisado:
   - Aprender nueva gramática (o mejorar la gramática existente) usando un corpus de oraciones sin árboles

2. Aprendizaje curricular:
   - Comenzar con la parte fácil del plan de estudios: oraciones cortas y no ambiguas de 2 palabras

3. Análisis semisupervisado:
   - Comenzar con un pequeño número de árboles para construir una gramática inicial
   - Agregar un gran número de oraciones sin analizar para mejorar la gramática

---

# Gramáticas Aumentadas

Ejemplo de categorías de pronombres:
- "Yo": puede ser sujeto de una oración, singular
- "me": no puede ser sujeto de una oración, plural

Subcategoría: Pronombre aumentado con características como "caso subjetivo, primera persona singular"

PCFG lexicalizada:
- Tipo de gramática aumentada
- Permite asignar probabilidades basadas en propiedades de las palabras en una frase más allá de las categorías sintácticas
- Notación: VP(v) denota una frase con categoría VP cuya palabra núcleo es v
- P1(v, n) significa la probabilidad de que un VP encabezado por v se una con un NP encabezado por n para formar un VP

---

# Ejemplos de Gramática Aumentada

1. Codificar hechos en entradas de probabilidad:
   - P1(v, ella) se hace muy pequeña para todos los verbos v

2. Reglas de concordancia:
   ```
   S(v) → NP(Sbj, pn, n) VP(pn, v) [P5(n, v)]
   ```
   NP es seguido por VP para formar S, pero solo si:
   - NP tiene caso subjetivo (Sbj)
   - La persona y el número (pn) de NP y VP son idénticos

---

# Gramáticas Semánticas

Ejemplo:
```
Oración: ¿Qué estados limitan con Texas?
Forma Lógica: λx.estado(x) ∧ λx.limita_con(x, Texas)
```

Aprendizaje de gramáticas semánticas:
- Usar una gran colección de pares y conocimiento codificado a mano para cada nuevo dominio
- El sistema genera entradas léxicas plausibles

Enfoque más fácil: Recopilar ejemplos de pares pregunta/respuesta
```
P: ¿Qué estados limitan con Texas?
R: Louisiana, Arkansas, Oklahoma, Nuevo México.

P: ¿Cuántas veces cabría Rhode Island en California?
R: 135
```

---

# Complejidades del Lenguaje Natural Real

1. Cuantificación:
   - Usar forma cuasi-lógica, luego convertir a oración lógica
   - Aplicar reglas de preferencia para elegir el alcance del cuantificador

2. Pragmática:
   - Resolver el significado de los indexicales (frases que se refieren a la situación actual)
   - Interpretar la intención del hablante (actos de habla)

3. Dependencias de larga distancia:
   - Usar forma cuasi-lógica y algoritmos de conversión

4. Tiempo y tiempo verbal:
   - El inglés usa tiempos verbales (pasado, presente, futuro) para indicar el tiempo relativo
   - La notación del cálculo de eventos puede representar el tiempo de los eventos

---

# Ambigüedad en el Lenguaje Natural

Tipos de ambigüedad:
1. Ambigüedad léxica:
   - Palabras con múltiples significados
   - Ejemplo: "banco" puede ser una institución financiera o un asiento

2. Ambigüedad sintáctica:
   - Frases con múltiples análisis
   - Ejemplo: "Vi un wumpus en 2,2" tiene dos interpretaciones posibles

3. Ambigüedad semántica:
   - Resulta de la ambigüedad sintáctica

---

# Desambiguación

Desambiguación: Recuperar el significado pretendido más probable de un enunciado

Cuatro modelos para la desambiguación:
1. Modelo del mundo: Probabilidad de que una proposición ocurra en el mundo
2. Modelo mental: Probabilidad de la intención del hablante de comunicar un hecho
3. Modelo de lenguaje: Probabilidad de elección de cadena de palabras dada la intención del hablante
4. Modelo acústico: Probabilidad de generación de secuencia de sonidos (para comunicación hablada)

---

# Tareas de Lenguaje Natural

1. Reconocimiento de voz:
   - Transformar sonido hablado en texto
   - Sistemas actuales: 3-5% de tasa de error de palabras

2. Síntesis de texto a voz:
   - Convertir texto a sonido

3. Traducción automática:
   - Transformar texto de un idioma a otro

4. Extracción de información:
   - Adquirir conocimiento al leer superficialmente el texto en busca de clases de objetos y relaciones específicas

5. Recuperación de información:
   - Encontrar documentos relevantes e importantes para una consulta dada

6. Respuesta a preguntas:
   - Proporcionar respuestas específicas a consultas formuladas como preguntas

---

# Resumen

- Los modelos de lenguaje probabilísticos basados en n-gramas recuperan información significativa sobre un idioma
- Las incrustaciones de palabras proporcionan representaciones de palabras más ricas y similitudes
- Las gramáticas de estructura de frase (especialmente las gramáticas libres de contexto) capturan la estructura jerárquica del lenguaje
- Las oraciones de lenguaje libre de contexto se pueden analizar en tiempo O(n³) usando analizadores de tabla como el algoritmo CYK
- Los bancos de árboles se pueden usar para aprender parámetros de gramática PCFG
- Las gramáticas aumentadas pueden manejar la interpretación semántica

```

## Notas sobre la traducción

1. "Vos": Se utilizó la forma de tratamiento "vos" característica del español argentino en lugar del "tú" usado en otras variantes del español.

2. Términos técnicos: Se mantuvieron en inglés algunos términos técnicos ampliamente utilizados en la comunidad informática argentina, como "tokenización", "n-grama", "WordNet", entre otros.

3. "Banco de árboles": Se tradujo "treebank" como "banco de árboles", que es el término más comúnmente usado en el ámbito académico argentino.

4. "Analizador": Se utilizó "analizador" en lugar de "parser" para mantener la coherencia con la terminología académica en español.

## Aspectos desafiantes de la traducción

1. Terminología técnica: Fue necesario equilibrar entre mantener términos en inglés ampliamente reconocidos y traducir otros para facilitar la comprensión.

2. Ejemplos específicos del idioma: Algunos ejemplos basados en la estructura del inglés (como el orden de adjetivos y sustantivos) requirieron adaptación para mantener la relevancia en español.

3. Siglas y abreviaturas: Se mantuvieron algunas siglas en inglés (como POS, HMM, PCFG) por ser de uso común en la literatura técnica en español.

4. Estructuras gramaticales complejas: Algunas oraciones con estructuras complejas propias del inglés académico requirieron reestructuración para mantener la claridad en español.