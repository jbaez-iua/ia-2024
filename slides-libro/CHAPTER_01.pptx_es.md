---
marp: true
theme: default
paginate: true
---

<!-- Diapositiva de título -->
# Inteligencia Artificial: Un Enfoque Moderno
## Capítulo 1: Introducción
### Cuarta Edición, Edición Global

---

<!-- Diapositiva de esquema -->
# Esquema

- ¿Qué es la IA?
- Una breve historia
- El estado del arte

---

<!-- Diapositiva: ¿Qué es la IA? -->
# ¿Qué es la IA?

Cuatro enfoques:
1. Sistemas que piensan como humanos
2. Sistemas que piensan racionalmente
3. Sistemas que actúan como humanos
4. Sistemas que actúan racionalmente

---

<!-- Diapositiva: Prueba de Turing -->
# Actuar humanamente: La Prueba de Turing

![width:800px](https://mermaid.ink/img/pako:eNptkLsOgzAMRX8l8gxUYmBHVKqXgaVDh6pLFBKqSiHBSdSHEP9eHkVl6Gb7-Nq-uoEKNUEO9WAbdGhb3ljT4sE5a3RwRhM1Bm3bykMwJL0JbopPpb7ni8fjjYjkGBHlNCFKY0QcZ0QhT4hyHpDkOKrYxxJRKaUQEfu-f1Vb9A22qLytA3bBW3QU0qDMYfwR5PgHsNZbPyDjrKuiH-mQsmw9Oo_-m0Iel9bVWKCPFp1vQnaZLLBEW5HPuUzz5Zxmy3SbZqts-y9MkWlO)

- Turing (1950) "Maquinaria de cómputo e inteligencia"
- "¿Pueden pensar las máquinas?" → "¿Pueden las máquinas comportarse de manera inteligente?"
- Prueba operativa para el comportamiento inteligente: el Juego de Imitación

---

<!-- Diapositiva: Predicciones de la Prueba de Turing -->
# Predicciones de la Prueba de Turing

- Predijo que para el 2000, una máquina podría tener un 30% de posibilidades de engañar a una persona común durante 5 minutos
- Anticipó todos los principales argumentos contra la IA en los siguientes 50 años
- Sugirió los componentes principales de la IA: conocimiento, razonamiento, comprensión del lenguaje, aprendizaje

**Problema:** La prueba de Turing no es reproducible, constructiva, ni se presta al análisis matemático

---

<!-- Diapositiva: Pensar humanamente -->
# Pensar humanamente: Ciencia Cognitiva

- "Revolución cognitiva" de los años 60: la psicología del procesamiento de información reemplazó la ortodoxia prevaleciente del conductismo
- Requiere teorías científicas de las actividades internas del cerebro
  - ¿Qué nivel de abstracción? "Conocimiento" o "circuitos"?
  - ¿Cómo validar?
    1. Prediciendo y probando el comportamiento de sujetos humanos (de arriba hacia abajo)
    2. Identificación directa a partir de datos neurológicos (de abajo hacia arriba)

---

<!-- Diapositiva: Pensar racionalmente -->
# Pensar racionalmente: Leyes del Pensamiento

- Normativo (o prescriptivo) en lugar de descriptivo
- Aristóteles: ¿cuáles son los argumentos/procesos de pensamiento correctos?
- Varias escuelas griegas desarrollaron diversas formas de lógica
- Línea directa a través de las matemáticas y la filosofía hasta la IA moderna

**Problemas:**
1. No todo el comportamiento inteligente está mediado por la deliberación lógica
2. ¿Cuál es el propósito de pensar? ¿Qué pensamientos debería tener entre todos los pensamientos (lógicos o no) que podría tener?

---

<!-- Diapositiva: Actuar racionalmente -->
# Actuar racionalmente

- Comportamiento racional: hacer lo correcto
- Lo correcto: aquello que se espera que maximice el logro de los objetivos, dada la información disponible
- No necesariamente implica pensar —por ejemplo, el reflejo de parpadeo— pero el pensamiento debería estar al servicio de la acción racional

> Aristóteles (Ética a Nicómaco):
> "Toda arte y toda investigación, y del mismo modo toda acción y elección, parecen tender a algún bien"

---

<!-- Diapositiva: Agentes racionales -->
# Agentes racionales

- Un agente es una entidad que percibe y actúa
- Este curso trata sobre el diseño de agentes racionales
- De manera abstracta, un agente es una función de historias de percepciones a acciones:
  ```
  f : P* → A
  ```
- Para cualquier clase dada de entornos y tareas, buscamos el agente (o clase de agentes) con el mejor desempeño

**Advertencia:** las limitaciones computacionales hacen que la racionalidad perfecta sea inalcanzable
→ diseñar el mejor programa para los recursos de máquina dados

---

<!-- Diapositiva: Prehistoria de la IA -->
# Prehistoria de la IA

| Campo | Contribución |
|-------|--------------|
| Filosofía | lógica, métodos de razonamiento, mente como sistema físico, fundamentos del aprendizaje, lenguaje, racionalidad |
| Matemáticas | representación formal y prueba, algoritmos, computación, (in)decidibilidad, (in)tratabilidad, probabilidad |
| Psicología | adaptación, fenómenos de percepción y control motor, técnicas experimentales (psicofísica, etc.) |
| Economía | teoría formal de las decisiones racionales |
| Lingüística | representación del conocimiento, gramática |
| Neurociencia | sustrato físico plástico para la actividad mental |
| Teoría de control | sistemas homeostáticos, estabilidad, diseños simples de agentes óptimos |

---

<!-- Diapositiva: Historia de la IA -->
# Historia resumida de la IA

<style scoped>
table {
  font-size: 0.7em;
}
</style>

| Año | Evento |
|------|-------|
| 1943 | McCulloch y Pitts: modelo de circuito booleano del cerebro |
| 1950 | "Maquinaria de cómputo e inteligencia" de Turing |
| 1952–69 | Primeros programas de IA, incluyendo el programa de damas de Samuel, el Logic Theorist de Newell y Simon, el Geometry Engine de Gelernter |
| 1956 | Reunión de Dartmouth: se adopta el término "Inteligencia Artificial" |
| 1965 | Algoritmo completo de Robinson para el razonamiento lógico |
| 1966–74 | La IA descubre la complejidad computacional, la investigación en redes neuronales casi desaparece |
| 1969–79 | Desarrollo temprano de sistemas basados en conocimiento |
| 1980–88 | Auge de la industria de sistemas expertos |
| 1988–93 | Caída de la industria de sistemas expertos: "Invierno de la IA" |
| 1985–95 | Las redes neuronales vuelven a ser populares |
| 1988– | Resurgimiento de la probabilidad; aumento general en la profundidad técnica |
| 1995– | "IA Nouvelle": Vida Artificial, Algoritmos Genéticos, computación suave |
| 2003– | La IA a nivel humano vuelve a la agenda |

---

<!-- Diapositiva: Estado del arte -->
# Estado del arte

¿Cuál de las siguientes tareas se puede realizar en la actualidad?

<style scoped>
ul {
  font-size: 0.8em;
  columns: 2;
}
</style>

- Jugar un partido decente de ping pong
- Conducir de forma segura por una carretera de montaña con curvas
- Conducir de forma segura por la Avenida 9 de Julio
- Comprar víveres para una semana en la web
- Comprar víveres para una semana en el Mercado Central
- Jugar una partida decente de bridge
- Descubrir y demostrar un nuevo teorema matemático
- Diseñar y ejecutar un programa de investigación en biología molecular
- Escribir una historia intencionalmente graciosa
- Dar asesoramiento legal competente en un área especializada del derecho
- Traducir inglés hablado a sueco hablado en tiempo real
- Conversar exitosamente con otra persona durante una hora
- Realizar una operación quirúrgica compleja
- Descargar cualquier lavavajillas y guardar todo

---

<!-- Diapositiva: Riesgos y beneficios de la IA -->
# Riesgos y beneficios de la IA

> "Primero resolvé la IA, luego usá la IA para resolver todo lo demás." 
> — Demis Hassabis, CEO de Google DeepMind

**Beneficios:**
- Disminución del trabajo repetitivo
- Aumento de la producción de bienes y servicios
- Aceleración de la investigación científica (curas de enfermedades, soluciones para el cambio climático y la escasez de recursos)

**Riesgos:**
- Armas autónomas letales
- Vigilancia y persuasión
- Toma de decisiones sesgada
- Impacto en el empleo
- Aplicaciones críticas para la seguridad
- Amenazas de ciberseguridad

---

<!-- Diapositiva: Superinteligencia de IA -->
# Superinteligencia de IA

- El desarrollo de una superinteligencia artificial que supere la inteligencia humana puede representar un riesgo significativo
- Análogo al "problema del gorila"
  - Los humanos y los gorilas evolucionaron de la misma especie, pero los humanos tienen más control que otros primates
- Deberíamos diseñar sistemas de IA de tal manera que no terminen tomando el control de la forma en que Turing sugiere que podrían hacerlo
