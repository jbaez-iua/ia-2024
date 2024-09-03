
# Agentes lógicos
## Capítulo 7

---

# Esquema

- Agentes basados en conocimiento
- Mundo de Wumpus
- Lógica en general—modelos y consecuencia lógica
- Lógica proposicional (booleana)
- Equivalencia, validez, satisfacibilidad  
- Reglas de inferencia y demostración de teoremas
  - resolución
  - encadenamiento hacia adelante
  - encadenamiento hacia atrás
- Verificación eficiente de modelos proposicionales

---

# Bases de conocimiento

![w:800](https://mermaid.ink/img/pako:eNp1kM1qwzAQhF9F7CmFvICPodDkkEMphZxySGOkjWMR_SCthcH2u1dK3Dg4pxV8M8zsLnvwhkNQYPFbm8O9bXUdVN-C-XieBOe6mD0FW1tNk0HpB7Cj7NeHVXDVQ9sgXGpMzRBRtJQtYc0m9_KS1qBx_LVWMkYqBHKXm5KzVZoVjT5l7DljK9Y8ZOxwzDZLKiL3tqZpzFfGNIcCPQ7q9nZAk9Qbx8JhBM8hNP11v2bOTbPwFjAI5-OUyUfqKjQ4jYKnQjhWOHoNEbHFZ1FXDp3H-jfAtygeqWf4bIyylDoH5NRijHoXLWVqyNBjfYjUMDSWmDcxl9Ib1Br_m2TYudhvMf4DIdmgqg?type=png)

---

# Una función simple de agente basado en conocimiento

```python
def Agente-BC(percepción):
    estático: BC, una base de conocimiento
              t, un contador, inicialmente 0, que indica el tiempo
    
    Decir(BC, Crear-Oración-Percepción(percepción, t))
    acción = Preguntar(BC, Crear-Consulta-Acción(t))
    Decir(BC, Crear-Oración-Acción(acción, t))
    t = t + 1
    return acción
```

El agente debe ser capaz de:
- Representar estados, acciones, etc.
- Incorporar nuevas percepciones
- Actualizar representaciones internas del mundo
- Deducir propiedades ocultas del mundo
- Deducir acciones apropiadas

---

# Descripción PEAS del Mundo de Wumpus

![bg right:40% w:400](https://mermaid.ink/img/pako:eNp1kstuwjAQRX_F8opIkPADXSCxYNGqUrtoF6jKxBPiIo-DxyGtEP-OTQikRV1ZmnvnztXYd1IaQ5QTQ3bXG7NsyjKqwXR6R3-s1aqgS1tXhvxdlm1BuJflK9-nC1oHVZe0L9ygHCIWhRrOH6kCjf7HGk2SiA2B7PKi4myWZHlNx4ydZ2zG6lPGjqdsvaAs8FYXdGPTNWOKQ44e-35zS0ETpxsne0WgIZjubT1nxk2z8JZAqCvtDfFEbZkaJwj4KZxjTiAaHVBPd1RsKugM1r8JnMP4mN3Bt1YrS7EzQE41etW4YFNKNSR6rAdPNUFtiGgVcimMRq3xf0iCrfG9rcM_xX-jjg?type=png)

- **Medida de rendimiento**: oro +1000, muerte -1000, -1 por paso, -10 por usar la flecha
- **Entorno**: 
  - Casillas adyacentes al wumpus huelen mal
  - Casillas adyacentes a un pozo son ventosas
  - Hay brillo si y solo si el oro está en la misma casilla
  - Disparar mata al wumpus si estás frente a él
  - Disparar usa la única flecha
  - Agarrar recoge el oro si está en la misma casilla
  - Soltar deja caer el oro en la misma casilla
- **Actuadores**: Girar a la izquierda, Girar a la derecha, Avanzar, Agarrar, Soltar, Disparar
- **Sensores**: Brisa, Brillo, Hedor

---

# Caracterización del mundo de Wumpus

- ¿Observable? No—solo percepción local
- ¿Determinista? Sí—resultados especificados exactamente
- ¿Episódico? No—secuencial a nivel de acciones
- ¿Estático? Sí—Wumpus y pozos no se mueven
- ¿Discreto? Sí
- ¿Un solo agente? Sí—Wumpus es esencialmente una característica natural

---

# Explorando un mundo de Wumpus

![bg right:60% w:600](https://mermaid.ink/img/pako:eNp1kc1qwzAQhF9F7CmF-AV8DAXnkEMphZxySGOktbGI_oO0Fgbb715ptePgnFbwzTCzK-0BrTIEHr-V3t-aSjVedhWY98dRcK6y2VOwtVU0GpS-BzvIfn1YeVfct2WES41pMkQULWVL2NKuN-Ml3YLC4ddayRipEMhdbnLOFmlW1PqUsdOMrVh9ytjxnG2mlEXubE3jlK-MKQ45euy77W0HNEm9cfQ7DB48-ab77teMuXEW3gIGYX2YM_lIXYUGx1HwVAjHCgevISC2-CyKwqHzWP4G-BbEQ_YMn41RllJrgZwaFEFvgqVMDRl6LPeBGgaFCfM6xFJ6g1rjf5MMWxv6LYR_ZWyguQ?type=png)

---

# Otras situaciones complicadas

![bg right:60% w:600](https://mermaid.ink/img/pako:eNp1kc1qwzAQhF9F7CmF-AV8DAXnkEMphZxySGOktbGI_oO0Fgbb715ptePgnFbwzTCzK-0BrTIEHr-V3t-aSjVedhWY98dRcK6y2VOwtVU0GpS-BzvIfn1YeVfct2WES41pMkQULWVL2NKuN-Ml3YLC4ddayRipEMhdbnLOFmlW1PqUsdOMrVh9ytjxnG2mlEXubE3jlK-MKQ45euy77W0HNEm9cfQ7DB48-ab77teMuXEW3gIGYX2YM_lIXYUGx1HwVAjHCgevISC2-CyKwqHzWP4G-BbEQ_YMn41RllJrgZwaFEFvgqVMDRl6LPeBGgaFCfM6xFJ6g1rjf5MMWxv6LYR_ZWyguQ?type=png)

- Brisa en (1,2) y (2,1) ⇒ no hay acciones seguras
- Suponiendo pozos distribuidos uniformemente, (2,2) tiene pozo con prob. 0,86, vs. 0,31
- Hedor en (1,1) ⇒ no se puede mover ⇒ seguro
- Se puede usar una estrategia de coacción: disparar recto hacia adelante
  - si el wumpus estaba ahí ⇒ muerto
  - si el wumpus no estaba ahí ⇒ seguro

---

# Lógica en general

- Las lógicas son lenguajes formales para representar información de tal manera que se puedan extraer conclusiones
- La sintaxis define las oraciones en el lenguaje
- La semántica define el "significado" de las oraciones; es decir, define la verdad de una oración en un mundo

Ejemplo: el lenguaje de la aritmética
- x + 2 ≥ y es una oración; x2 + y > no es una oración
- x + 2 ≥ y es verdadera si y solo si el número x + 2 no es menor que el número y
- x + 2 ≥ y es verdadera en un mundo donde x = 7, y = 1
- x + 2 ≥ y es falsa en un mundo donde x = 0, y = 6

---

# Consecuencia lógica

Consecuencia lógica significa que una cosa se sigue de otra:
BC |= α

La base de conocimiento BC implica lógicamente la oración α si y solo si α es verdadera en todos los mundos donde BC es verdadera

Ejemplos:
- La BC que contiene "los Gigantes ganaron" y "los Rojos ganaron" implica "O los Gigantes ganaron o los Rojos ganaron"
- x + y = 4 implica 4 = x + y

La consecuencia lógica es una relación entre oraciones (es decir, sintaxis) que se basa en la semántica

Nota: los cerebros procesan sintaxis (de algún tipo)

---

# Modelos

- Los lógicos típicamente piensan en términos de modelos, que son mundos formalmente estructurados con respecto a los cuales se puede evaluar la verdad
- Decimos que m es un modelo de una oración α si α es verdadera en m
- M(α) es el conjunto de todos los modelos de α
- Entonces BC |= α si y solo si M(BC) ⊆ M(α)

Ejemplo:
BC = Los Gigantes ganaron y los Rojos ganaron
α = Los Gigantes ganaron

![Diagrama de modelo](https://mermaid.ink/img/pako:eNp1kMFqwzAMhl9F6JRC8wI-hkF7yGGUQk45pDXCsbCI7RBLhWL73SsnbTzonNDv79OnX-zBGw5BgcVvbQ73ttV1UH0L5uN5Epzr4uwp2NpqmgxKP4AdeHY_rIKrHtoG4VJjakZEcaJsCWc2-ZOXtAaN46-1kjFSIZC73JScrdKsaPQpY88ZW7HmIWOHY7ZZUhG5tzVNY74ypjkU6HHQt7cDmqTeOBYOI3gOoemv-zVzbpqFt4BBkI9TJh-pq9DgNAqeCuFY4eg1RMQWX0RdOXQe698A36J4pJ7hszHKUuockFOLMepd9CnTjAw91odIMwwmvlc_WnxPiV5rrPFfSoad8_32j_8AkN2hbw?type=png)

---

# Consecuencia lógica en el mundo de Wumpus

Situación después de no detectar nada en [1,1], moverse a la derecha, brisa en [2,1]

Consideremos posibles modelos para ?s asumiendo solo pozos
3 opciones booleanas ⇒ 8 modelos posibles

![Mundo de Wumpus](https://mermaid.ink/img/pako:eNp1kE1qAzEMha-itJNCcwEvh0F_Fi2llHbVRRojrY1F_IOkFgbb965MJjOTdCX0nr5P0gt7cJpDUGDxW-nDvWlU7WVXgfl4HAXnKps9BVMbRaNB6Xuwg-zXh5V3xX1bRrjUmCZDRNFStoQt7XozXtItKBx-rZGMkQqB3OUm52yRZkWtTxk7zdiK1aeMHc_ZZkpZ5M7UNE75ypjikKPDvtvednBJ6rWl32Hw4Mk33Xe_ZsyNs_AWMAjrwpzJReoqNDiOgqdCWFY4OA0BscVnURQWrcPyN8C3IB6yZ_isjDKUWgPk1KAIehMsZWrI0GO5D9QwKEyY1yGW0mvUCv-bZNiY0G8h_ANjjKH8?type=png)

---

# Modelos de Wumpus

![Modelos de Wumpus](https://mermaid.ink/img/pako:eNp1kE1qAzEMha-itJNCcwEvh0F_Fi2llHbVRRojrY1F_IOkFgbb965MJjOTdCX0nr5P0gt7cJpDUGDxW-nDvWlU7WVXgfl4HAXnKps9BVMbRaNB6Xuwg-zXh5V3xX1bRrjUmCZDRNFStoQt7XozXtItKBx-rZGMkQqB3OUm52yRZkWtTxk7zdiK1aeMHc_ZZkpZ5M7UNE75ypjikKPDvtvednBJ6rWl32Hw4Mk33Xe_ZsyNs_AWMAjrwpzJReoqNDiOgqdCWFY4OA0BscVnURQWrcPyN8C3IB6yZ_isjDKUWgPk1KAIehMsZWrI0GO5D9QwKEyY1yGW0mvUCv-bZNiY0G8h_ANjjKH8?type=png)

BC = reglas del mundo de Wumpus + observaciones
α1 = "[1,2] es seguro", BC |= α1, demostrado por verificación de modelos
α2 = "[2,2] es seguro", BC |= α2

---

# Inferencia

BC ⊢i α = la oración α se puede derivar de BC mediante el procedimiento i

Las consecuencias de BC son un pajar; α es una aguja.
Consecuencia lógica = aguja en el pajar; inferencia = encontrarla

Solidez: i es sólido si siempre que BC ⊢i α, también es cierto que BC |= α

Completitud: i es completo si siempre que BC |= α, también es cierto que BC ⊢i α

Anticipo: definiremos una lógica (lógica de primer orden) que es lo suficientemente expresiva para decir casi cualquier cosa de interés, y para la cual existe un procedimiento de inferencia sólido y completo.

Es decir, el procedimiento responderá cualquier pregunta cuya respuesta se siga de lo que se conoce en la BC.

---

# Lógica proposicional: Sintaxis

La lógica proposicional es la lógica más simple—ilustra ideas básicas

- Los símbolos de proposición P1, P2, etc. son oraciones
- Si S es una oración, ¬S es una oración (negación)
- Si S1 y S2 son oraciones, S1 ∧ S2 es una oración (conjunción)
- Si S1 y S2 son oraciones, S1 ∨ S2 es una oración (disyunción)
- Si S1 y S2 son oraciones, S1⇒S2 es una oración (implicación)
- Si S1 y S2 son oraciones, S1⇔S2 es una oración (bicondicional)

---

# Lógica proposicional: Semántica

Cada modelo especifica verdadero/falso para cada símbolo de proposición
Ej., P1,2 P2,2 P3,1
     verdadero verdadero falso

(Con estos símbolos, 8 modelos posibles, se pueden enumerar automáticamente.)

Reglas para evaluar la verdad con respecto a un modelo m:
- ¬S es verdadera si y solo si S es falsa
- S1 ∧ S2 es verdadera si y solo si S1 es verdadera y S2 es verdadera
- S1 ∨ S2 es verdadera si y solo si S1 es verdadera o S2 es verdadera
- S1 ⇒ S2 es verdadera si y solo si S1 es falsa o S2 es verdadera
- S1 ⇔ S2 es verdadera si y solo si S1 ⇒ S2 es verdadera y S2 ⇒ S1 es verdadera

Un proceso recursivo simple evalúa una oración arbitraria, ej.,
¬P1,2 ∧ (P2,2 ∨ P3,1) = verdadero ∧ (falso ∨ verdadero) = verdadero ∧ verdadero = verdadero

---

# Tablas de verdad para conectivos

| P | Q | ¬P | P ∧ Q | P ∨ Q | P ⇒ Q | P ⇔ Q |
|---|---|-----|-------|-------|-------|-------|
| falso | falso | verdadero | falso | falso | verdadero | verdadero |
| falso | verdadero | verdadero | falso | verdadero | verdadero | falso |
| verdadero | falso | falso | falso | verdadero | falso | falso |
| verdadero | verdadero | falso | verdadero | verdadero | verdadero | verdadero |

---

# Oraciones del mundo de Wumpus

Sea Pi,j verdadero si hay un pozo en [i, j].
Sea Bi,j verdadero si hay una brisa en [i, j].

¬P1,1
¬B1,1
B2,1

"Los pozos causan brisas en casillas adyacentes"
B1,1 ⇔ (P1,2 ∨ P2,1)
B2,1 ⇔ (P1,1 ∨ P2,2 ∨ P3,1)

"Una casilla es ventosa si y solo si hay un pozo adyacente"

---

# Tablas de verdad para inferencia

| B1,1 | B2,1 | P1,1 | P1,2 | P2,1 | P2,2 | P3,1 | R1 | R2 | R3 | R4 | R5 | BC |
|------|------|------|------|------|------|------|----|----|----|----|----|----|
| falso | falso | falso | falso | falso | falso | falso | verdadero | verdadero | verdadero | verdadero | verdadero | falso |
| falso | falso | falso | falso | falso | falso | verdadero | falso | verdadero | verdadero | verdadero | falso | falso |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |
| verdadero | verdadero | falso | verdadero | verdadero | falso | falso | verdadero | verdadero | verdadero | verdadero | verdadero | verdadero |

Enumerar filas (diferentes asignaciones a símbolos), si BC es verdadera en la fila, verificar que α también lo sea

---

# Inferencia por enumeración

```python
def TT-Implica?(BC, α):
    símbolos = una lista de los símbolos de proposición en BC y α
    return TT-Verificar-Todo(BC, α, símbolos, [])

def TT-Verificar-Todo(BC, α, símbolos, modelo):
    if Vacío?(símbolos):
        if PL-Verdadero?(BC, modelo):
            return PL-Verdadero?(α, modelo)
        else:
            return verdadero
    else:
        P = Primero(símbolos)
        resto = Resto(símbolos)
        return (TT-Verificar-Todo(BC, α, resto, Extender(P, verdadero, modelo)) and
                TT-Verificar-Todo(BC, α, resto, Extender(P, falso, modelo)))
```

O(2^n) para n símbolos; el problema es co-NP-completo

---

# Equivalencia lógica

Dos oraciones son lógicamente equivalentes si y solo si son verdaderas en los mismos modelos:
α ≡ β si y solo si α |= β y β |= α

- (α ∧ β) ≡ (β ∧ α) conmutatividad de ∧
- (α ∨ β) ≡ (β ∨ α) conmutatividad de ∨
- ((α ∧ β) ∧ γ) ≡ (α ∧ (β ∧ γ)) asociatividad de ∧
- ((α ∨ β) ∨ γ) ≡ (α ∨ (β ∨ γ)) asociatividad de ∨
- ¬(¬α) ≡ α eliminación de doble negación
- (α ⇒ β) ≡ (¬β ⇒ ¬α) contraposición
- (α ⇒ β) ≡ (¬α ∨ β) eliminación de implicación
- (α ⇔ β) ≡ ((α ⇒ β) ∧ (β ⇒ α)) eliminación de bicondicional
- ¬(α ∧ β) ≡ (¬α ∨ ¬β) De Morgan
- ¬(α ∨ β) ≡ (¬α ∧ ¬β) De Morgan
- (α ∧ (β ∨ γ)) ≡ ((α ∧ β) ∨ (α ∧ γ)) distributividad de ∧ sobre ∨
- (α ∨ (β ∧ γ)) ≡ ((α ∨ β) ∧ (α ∨ γ)) distributividad de ∨ sobre ∧

---

# Validez y satisfacibilidad

- Una oración es **válida** si es verdadera en todos los modelos, ej., Verdadero, A ∨ ¬A, A ⇒ A, (A ∧ (A ⇒ B)) ⇒ B
- La validez está conectada a la inferencia a través del Teorema de Deducción:
  BC |= α si y solo si (BC ⇒ α) es válida
- Una oración es **satisfacible** si es verdadera en algún modelo, ej., A ∨ B, C
- Una oración es **insatisfacible** si no es verdadera en ningún modelo, ej., A ∧ ¬A
- La satisfacibilidad está conectada a la inferencia a través de lo siguiente:
  BC |= α si y solo si (BC ∧ ¬α) es insatisfacible
  es decir, demostrar α por reducción al absurdo

---

# Métodos de demostración

Los métodos de demostración se dividen (aproximadamente) en dos tipos:

1. Aplicación de reglas de inferencia
   - Generación legítima (sólida) de nuevas oraciones a partir de las antiguas
   - Demostración = una secuencia de aplicaciones de reglas de inferencia
   - Se pueden usar reglas de inferencia como operadores en un algoritmo de búsqueda estándar
   - Típicamente requieren traducción de oraciones a una forma normal

2. Verificación de modelos
   - enumeración de tablas de verdad (siempre exponencial en n)
   - retroceso mejorado, ej., Davis–Putnam–Logemann–Loveland
   - búsqueda heurística en el espacio de modelos (sólida pero incompleta)
   - ej., algoritmos de escalada de colinas tipo min-conflictos

---

# Resolución

Forma Normal Conjuntiva (FNC—universal)
- conjunción de disyunciones de literales
- Ej., (A ∨ ¬B) ∧ (B ∨ ¬C ∨ ¬D)

Regla de inferencia de resolución (para FNC): completa para lógica proposicional
```
l1 ∨ · · · ∨ lk, m1 ∨ · · · ∨ mn
l1 ∨ · · · ∨ li−1 ∨ li+1 ∨ · · · ∨ lk ∨ m1 ∨ · · · ∨ mj−1 ∨ mj+1 ∨ · · · ∨ mn
```
donde li y mj son literales complementarios.

Ej., P1,3 ∨ P2,2, ¬P2,2 ⊢ P1,3

La resolución es sólida y completa para la lógica proposicional

---

# Conversión a FNC

Ejemplo: B1,1 ⇔ (P1,2 ∨ P2,1)

1. Eliminar ⇔, reemplazando α ⇔ β con (α ⇒ β) ∧ (β ⇒ α):
   (B1,1 ⇒ (P1,2 ∨ P2,1)) ∧ ((P1,2 ∨ P2,1) ⇒ B1,1)

2. Eliminar ⇒, reemplazando α ⇒ β con ¬α ∨ β:
   (¬B1,1 ∨ P1,2 ∨ P2,1) ∧ (¬(P1,2 ∨ P2,1) ∨ B1,1)

3. Mover ¬ hacia adentro usando las reglas de De Morgan y doble negación:
   (¬B1,1 ∨ P1,2 ∨ P2,1) ∧ ((¬P1,2 ∧ ¬P2,1) ∨ B1,1)

4. Aplicar ley de distributividad (∨ sobre ∧) y aplanar:
   (¬B1,1 ∨ P1,2 ∨ P2,1) ∧ (¬P1,2 ∨ B1,1) ∧ (¬P2,1 ∨ B1,1)

---

# Algoritmo de resolución

```python
def PL-Resolución(BC, α):
    cláusulas = el conjunto de cláusulas en la representación FNC de BC ∧ ¬α
    nuevo = {}
    while True:
        for each Ci, Cj in cláusulas:
            resolventes = PL-Resolver(Ci, Cj)
            if resolventes contiene la cláusula vacía:
                return verdadero
            nuevo = nuevo ∪ resolventes
        if nuevo ⊆ cláusulas:
            return falso
        cláusulas = cláusulas ∪ nuevo
```

---

# Ejemplo de resolución

BC = (B1,1 ⇔ (P1,2 ∨ P2,1)) ∧ ¬B1,1
α = ¬P1,2

![Ejemplo de resolución](https://mermaid.ink/img/pako:eNp1kc1qwzAQhF9F7CmF-AV8DAXnkEMphZxySGOktbGI_oO0Fgbb715ptePgnFbwzTCzK-0BrTIEHr-V3t-aSjVedhWY98dRcK6y2VOwtVU0GpS-BzvIfn1YeVfct2WES41pMkQULWVL2NKuN-Ml3YLC4ddayRipEMhdbnLOFmlW1PqUsdOMrVh9ytjxnG2mlEXubE3jlK-MKQ45euy77W0HNEm9cfQ7DB48-ab77teMuXEW3gIGYX2YM_lIXYUGx1HwVAjHCgevISC2-CyKwqHzWP4G-BbEQ_YMn41RllJrgZwaFEFvgqVMDRl6LPeBGgaFCfM6xFJ6g1rjf5MMWxv6LYR_ZWyguQ?type=png)

---

# Encadenamiento hacia adelante y hacia atrás

Forma de Horn (restringida)
- BC = conjunción de cláusulas de Horn
- Cláusula de Horn = 
  - símbolo de proposición; o
  - (conjunción de símbolos) ⇒ símbolo
- Ej., C ∧ (B ⇒ A) ∧ (C ∧ D ⇒ B)

Modus Ponens (para Forma de Horn): completo para BC de Horn
```
α1, . . . , αn, α1 ∧ · · · ∧ αn ⇒ β
β
```

Se puede usar con encadenamiento hacia adelante o hacia atrás.
Estos algoritmos son muy naturales y se ejecutan en tiempo lineal

---

#