
# Cuantificación de la Incertidumbre
## Capítulo 12

---

# Esquema

- Actuando bajo incertidumbre
- Notación básica de probabilidad
- Inferencia usando distribuciones conjuntas completas
- Independencia
- Regla de Bayes y su uso
- Modelos Bayesianos ingenuos
- El mundo de Wumpus revisitado

---

# Actuando bajo incertidumbre

- Los problemas del mundo real contienen incertidumbres debido a:
  - Observabilidad parcial
  - No determinismo
  - Adversarios

- Ejemplo de diagnóstico dental usando lógica proposicional:
  ```
  Dolor de muelas ⇒ Caries
  ```
  - Inexacto, no todos los pacientes con dolor de muelas tienen caries
  ```
  Dolor de muelas ⇒ Caries ∨ Problema de encías ∨ Absceso ...
  ```
  - Se necesita agregar una lista casi ilimitada de posibles problemas

---

# Actuando bajo incertidumbre (cont.)

- Un agente se esfuerza por elegir la decisión racional
- Depende de:
  - Importancia relativa de varios objetivos
  - Probabilidad y grado de logro

- Los dominios grandes (por ej., diagnóstico médico) fallan debido a:
  1. Pereza: Demasiado trabajo para listar el conjunto completo de antecedentes/consecuentes
  2. Ignorancia teórica: Teoría científica incompleta
  3. Ignorancia práctica: Incertidumbre debido a la falta de pruebas

- Un agente solo tiene un grado de creencia en oraciones relevantes

---

# Actuando bajo incertidumbre (cont.)

- **Teoría de la probabilidad**
  - Herramienta para manejar grados de creencia
  - Resume la incertidumbre de la pereza y la ignorancia

- **Incertidumbre y decisiones racionales**
  - Requiere preferencia entre diferentes posibles resultados
  - **Teoría de la utilidad**: Calidad del resultado siendo útil
    - Cada estado tiene un grado de utilidad
    - Se prefiere una utilidad más alta
  - **Teoría de la decisión** = Teoría de la probabilidad + Teoría de la utilidad
    - Un agente es racional si elige la acción con la utilidad esperada más alta
    - Principio de máxima utilidad esperada (MUE)

---

# Agente de teoría de decisiones

```python
función AGENTE-TD(percepción) devuelve una acción
    persistente: estado_creencia, creencias probabilísticas sobre el estado actual del mundo
                 acción, la acción del agente

    actualizar estado_creencia basado en acción y percepción
    calcular probabilidades de resultado para acciones,
        dadas las descripciones de acción y el estado_creencia actual
    seleccionar acción con la utilidad esperada más alta
        dadas las probabilidades de resultados e información de utilidad
    devolver acción
```

---

# Notación básica de probabilidad

- **Espacio muestral**: Conjunto de todos los mundos posibles
  - Mutuamente excluyentes y exhaustivos

- **Modelo de probabilidad**: Asocia probabilidad numérica P(ω) con cada mundo posible

- **Axiomas básicos de la teoría de la probabilidad**:
  - 0 ≤ P(ω) ≤ 1 para cada ω y ω ∈ Ω
  - ∑ P(ω) = 1 para ω ∈ Ω

- **Probabilidad incondicional o previa**: Grados de creencia en proposiciones sin otra información

---

# Notación básica de probabilidad (cont.)

- **Probabilidad condicional o posterior**: Dado evidencia, grado de creencia de nuevo evento

- Probabilidad de a dado b:
  ```
  P(a|b) = P(a ∧ b) / P(b)
  ```

- También se puede escribir como:
  ```
  P(a ∧ b) = P(a|b)P(b)
  ```

- Ejemplo: Tirando dados justos, dobles cuando el primer dado es 5
  ```
  P(dobles|Dado1 = 5) = P(dobles ∧ Dado1 = 5) / P(Dado1 = 5)
  ```

---

# Notación básica de probabilidad (cont.)

- **Representación factorizada**: Mundo posible representado por conjunto de pares variable/valor

- **Variables aleatorias**: Variables en teoría de probabilidad (nombres en mayúsculas)

- Notación de distribución de probabilidad:
  ```
  P(Clima) = (0.6, 0.1, 0.29, 0.01)
  ```
  Representa:
  ```
  P(Clima = sol) = 0.6
  P(Clima = lluvia) = 0.1
  P(Clima = nublado) = 0.29
  P(Clima = nieve) = 0.01
  ```

---

# Inferencia usando distribuciones conjuntas completas

- Comenzar con la distribución conjunta:

  | Dolor de muelas | Atrapa | Caries | Probabilidad |
  |-----------------|--------|--------|--------------|
  | verdadero       | verdadero | verdadero | 0.108    |
  | verdadero       | verdadero | falso     | 0.012    |
  | verdadero       | falso     | verdadero | 0.072    |
  | verdadero       | falso     | falso     | 0.008    |
  | falso           | verdadero | verdadero | 0.016    |
  | falso           | verdadero | falso     | 0.064    |
  | falso           | falso     | verdadero | 0.144    |
  | falso           | falso     | falso     | 0.576    |

- Para cualquier proposición φ, sumar los eventos atómicos donde es verdadera:
  ```
  P(φ) = Σω:ω |= φ P(ω)
  ```

---

# Inferencia usando distribuciones conjuntas completas (cont.)

- Ejemplos:
  ```
  P(dolor de muelas) = 0.108 + 0.012 + 0.016 + 0.064 = 0.2
  ```
  ```
  P(caries ∨ dolor de muelas) = 0.108 + 0.012 + 0.072 + 0.008 + 0.016 + 0.064 = 0.28
  ```

- Cálculo de probabilidades condicionales:
  ```
  P(¬caries | dolor de muelas) = P(¬caries ∧ dolor de muelas) / P(dolor de muelas)
                                = (0.016 + 0.064) / (0.108 + 0.012 + 0.016 + 0.064)
                                = 0.4
  ```

---

# Normalización

- El denominador puede verse como una constante de normalización α
  ```
  P(Caries | dolor de muelas) = α P(Caries, dolor de muelas)
                               = α [P(Caries, dolor de muelas, atrapa) + P(Caries, dolor de muelas, ¬atrapa)]
                               = α [(0.108, 0.016) + (0.012, 0.064)]
                               = α (0.12, 0.08) = (0.6, 0.4)
  ```

- Idea general: Calcular la distribución en la variable de consulta fijando las variables de evidencia y sumando sobre las variables ocultas

---

# Inferencia usando distribuciones conjuntas completas (cont.)

- Sea X todas las variables, Y las variables de consulta, E las variables de evidencia y H las variables ocultas

- La distribución conjunta posterior:
  ```
  P(Y|E = e) = αP(Y, E = e) = αΣh P(Y, E = e, H = h)
  ```

- Problemas:
  1. Complejidad temporal en el peor caso O(d^n) donde d es la aridad más grande
  2. Complejidad espacial O(d^n) para almacenar la distribución conjunta
  3. Dificultad para encontrar números para O(d^n) entradas

---

# Independencia

![Ejemplos de independencia](https://i.imgur.com/YXYPxWq.png)

- Dos eventos a y b son independientes si:
  ```
  P(a|b) = P(a) o P(b|a) = P(b) o P(a ∧ b) = P(a)P(b)
  ```

- Ejemplo: Problemas dentales y clima
  ```
  P(dolor de muelas, atrapa, caries, nublado) = P(nublado|dolor de muelas, atrapa, caries) P(dolor de muelas, atrapa, caries)
  P(nublado|dolor de muelas, atrapa, caries) = P(nublado)
  P(dolor de muelas, atrapa, caries, nublado) = P(nublado)P(dolor de muelas, atrapa, caries)
  ```

---

# Regla de Bayes y su uso

- Derivada de la regla del producto:
  ```
  P(a ∧ b) = P(a|b)P(b) y P(a ∧ b) = P(b|a)P(a)
  ```

- Regla de Bayes:
  ```
  P(b|a) = P(a|b)P(b) / P(a)
  ```

- A menudo se usa para determinar causas desconocidas a partir de efectos observados:
  ```
  P(causa|efecto) = P(efecto|causa)P(causa) / P(efecto)
  ```

- P(efecto|causa): Dirección causal
- P(causa|efecto): Dirección diagnóstica

---

# Ejemplo de la Regla de Bayes

- La meningitis causa cuello rígido el 70% de las veces
- Probabilidad previa de meningitis: 1/50.000
- Probabilidad previa de cuello rígido: 1%

Sea:
- c: el paciente tiene cuello rígido
- m: el paciente tiene meningitis

Dado:
```
P(c|m) = 0,7
P(m) = 1/50000
P(c) = 0,01
```

Calcular:
```
P(m|c) = P(c|m)P(m) / P(c) = 0,7 × 1/50000 / 0,01 = 0,0014
```

Solo el 0,14% de los pacientes con cuello rígido tienen meningitis.

---

# Modelos Bayesianos ingenuos

![Modelo Bayesiano ingenuo](https://i.imgur.com/XWNXsdg.png)

- Ejemplo:
  ```
  P(Caries|dolor de muelas ∧ atrapa) = α P(dolor de muelas ∧ atrapa|Caries)P(Caries)
                                      = α P(dolor de muelas|Caries)P(atrapa|Caries)P(Caries)
  ```

- Forma general:
  ```
  P(Causa, Efecto1, ..., Efecton) = P(Causa) Πi P(Efectoi|Causa)
  ```

- El número total de parámetros es lineal en n

---

# El mundo de Wumpus revisitado

![Mundo de Wumpus](https://i.imgur.com/JXNhzfL.png)

- Pij = verdadero si y solo si [i, j] contiene un pozo
- Bij = verdadero si y solo si [i, j] es ventoso
- Incluir solo B1,1, B1,2, B2,1 en el modelo de probabilidad

---

# Especificación del modelo de probabilidad

- Distribución conjunta completa: P(P1,1, ..., P4,4, B1,1, B1,2, B2,1)
- Aplicar regla del producto: P(B1,1, B1,2, B2,1 | P1,1, ..., P4,4)P(P1,1, ..., P4,4)

- Primer término: 1 si los pozos son adyacentes a brisas, 0 en caso contrario
- Segundo término: los pozos se colocan aleatoriamente, probabilidad 0,2 por cuadrado
  ```
  P(P1,1, ..., P4,4) = Π4,4i,j=1,1 P(Pi,j) = 0,2n × 0,816-n para n pozos
  ```

---

# Observaciones y consulta

Dado:
- b = ¬b1,1 ∧ b1,2 ∧ b2,1
- conocido = ¬p1,1 ∧ ¬p1,2 ∧ ¬p2,1

Consulta: P(P1,3|conocido, b)

Definir:
- Desconocido = Pijs distintos de P1,3 y Conocido

Para inferencia por enumeración:
```
P(P1,3|conocido, b) = α Σdesconocido P(P1,3, desconocido, conocido, b)
```

Problema: ¡Crece exponencialmente con el número de cuadrados!

---

# Usando independencia condicional

![Independencia condicional](https://i.imgur.com/XWNXsdg.png)

- Las observaciones son condicionalmente independientes de otros cuadrados ocultos dados los cuadrados ocultos vecinos
- Definir Desconocido = Franja ∪ Otros
- P(b|P1,3, Conocido, Desconocido) = P(b|P1,3, Conocido, Franja)

---

# Usando independencia condicional (cont.)

Después de la manipulación:
```
P(P1,3|conocido, b) = α P(P1,3) Σfranja P(b|conocido, P1,3, franja)P(franja)
```

Cálculo:
```
P(P1,3|conocido, b) = α (0,2(0,04 + 0,16 + 0,16), 0,8(0,04 + 0,16))
                    ≈ (0,31, 0,69)
```

```
P(P2,2|conocido, b) ≈ (0,86, 0,14)
```

---

# Resumen

- Las probabilidades expresan la incapacidad del agente para tomar decisiones definitivas
- La teoría de la decisión combina las creencias y deseos del agente
- Las declaraciones básicas de probabilidad incluyen probabilidades previas y condicionales
- Los axiomas de probabilidad restringen las probabilidades de proposiciones lógicamente relacionadas
- La distribución de probabilidad conjunta completa especifica la probabilidad de cada asignación completa
- La independencia absoluta permite factorizar la distribución conjunta completa
- La regla de Bayes permite calcular probabilidades desconocidas a partir de probabilidades condicionales conocidas
- La independencia condicional permite factorizar la distribución conjunta completa en distribuciones condicionales más pequeñas

```

# Notas sobre la traducción

1. "Wumpus World" se tradujo como "Mundo de Wumpus", manteniendo el nombre propio "Wumpus".
2. Se utilizó "vos" implícito en las explicaciones, manteniendo un tono formal y profesional.
3. Términos técnicos como "Naive Bayes" se tradujeron como "Bayesiano ingenuo", que es el término comúnmente usado en Argentina.
4. Se mantuvieron los símbolos matemáticos y lógicos sin cambios (∧, ∨, ¬, etc.).
5. "Catch" en el contexto dental se tradujo como "atrapa", refiriéndose a cuando el hilo dental se atasca entre los dientes.

# Aspectos desafiantes de la traducción

1. La traducción de "catch" en el contexto dental fue desafiante, ya que no tiene una traducción directa en español. Se optó por "atrapa" para mantener la brevedad y el sentido.

2. Algunos términos técnicos como "Naive Bayes" tienen traducciones establecidas en español, pero se tuvo que verificar su uso en el contexto académico argentino.

3. La adaptación de las explicaciones matemáticas y probabilísticas requirió atención para mantener la precisión técnica mientras se aseguraba que fueran comprensibles en español.

4. Se mantuvo un equilibrio entre el uso de términos técnicos en inglés (cuando son comúnmente usados así en el ámbito académico argentino) y su traducción al español cuando era más apropiado.

5. La traducción de los ejemplos, especialmente los relacionados con probabilidades y diagnósticos médicos, requirió cuidado para mantener la coherencia y la precisión numérica.