---
marp: true
theme: default
paginate: true
---

# Agentes Inteligentes
## Capítulo 2

---

# Esquema

- Agentes y entornos
- Racionalidad
- PEAS (medida de Rendimiento, Entorno, Actuadores, Sensores)
- Tipos de entornos
- Tipos de agentes

---

# Agentes y entornos

![Interacción Agente-Entorno](https://mermaid.ink/img/pako:eNptkMEKgzAMhl8l5DRBdtDLXmHsdNjNk9BSrVAtlVYYvvtabReGkEOS7_-TkAU6bQk4-IGwp2JcOxKsKUQvg1aaXuTARhnQ6e6EyxsKzgfveFJ4QVcoOWHvPWnW0MJFg2-IWRVFURIj1Uh1lFvI87wsixzr8hHrb-XYXpG_eaU4-pFsoJk8-dG6V3qGp8GePNGfaTa4GDwvM4xhFVvz9Qb-_0vi)

Un agente puede ser cualquier cosa que pueda verse como percibiendo su entorno a través de sensores y actuando sobre ese entorno a través de actuadores

---

# Función del Agente

- La función del agente mapea desde historias de percepciones a acciones:
  $f : P^* \rightarrow A$
- El programa del agente se ejecuta en la arquitectura física para producir $f$

---

# Mundo de la aspiradora

![Mundo de la Aspiradora](https://mermaid.ink/img/pako:eNpNjrEOgzAMRH8l8gwSA0MXJFbEwNCpUxcUuQRBghOZGIr495pAKXfy6e7eWTMYowgYmxZxpGbuZ0tCBXLEE01K0XtO4FQEDHp4wk3xdwR56lD0gYrk2Xm9oUZzNagOG-NrAB2uLrGlhRaq8_xpQrIs2_Z-_zxer3fbtq_TtO_TdBynGUTjbHAK_1NwFGb0ZIkOEsm5WOVcXCmQJz9TNDT_rr8A9LlOyA)

- Percepciones: ubicación y contenidos, por ejemplo, [A, Sucio]
- Acciones: Izquierda, Derecha, Aspirar, NoOp

---

# Un agente aspiradora

| Secuencia de percepción | Acción |
|-------------------------|--------|
| [A, Limpio]             | Derecha|
| [A, Sucio]              | Aspirar|
| [B, Limpio]             | Izquierda|
| [B, Sucio]              | Aspirar|
| [A, Limpio], [A, Limpio]| Derecha|
| [A, Limpio], [A, Sucio] | Aspirar|

---

# Agente Aspiradora Reflejo

```python
función Agente-Aspiradora-Reflejo([ubicación, estado]) devuelve una acción
    si estado = Sucio entonces devolver Aspirar
    sino si ubicación = A entonces devolver Derecha
    sino si ubicación = B entonces devolver Izquierda
```

¿Cuál es la función correcta?
¿Se puede implementar en un programa de agente pequeño?

---

# Racionalidad

- Medida de rendimiento fija evalúa la secuencia del entorno
  - ¿Un punto por cuadrado limpiado en tiempo T?
  - ¿Un punto por cuadrado limpio por paso de tiempo, menos uno por movimiento?
  - ¿Penalizar por > k cuadrados sucios?

- Un agente racional elige la acción que maximiza el valor esperado de la medida de rendimiento dada la secuencia de percepciones hasta la fecha

---

# Racionalidad (cont.)

- Racional ≠ omnisciente
  - Las percepciones pueden no proporcionar toda la información relevante
- Racional ≠ clarividente
  - Los resultados de las acciones pueden no ser los esperados
- Por lo tanto, racional ≠ exitoso
- Racional ⇒ exploración, aprendizaje, autonomía

---

# PEAS

Para diseñar un agente racional, debemos especificar el entorno de la tarea

Consideremos, por ejemplo, la tarea de diseñar un taxi automatizado:
- ¿Medida de rendimiento?
- ¿Entorno?
- ¿Actuadores?
- ¿Sensores?

---

# PEAS para Taxi Automatizado

- Medida de rendimiento: seguridad, destino, ganancias, legalidad, comodidad, ...
- Entorno: calles/autopistas de EE. UU., tráfico, peatones, clima, ...
- Actuadores: dirección, acelerador, freno, bocina, altavoz/pantalla, ...
- Sensores: video, acelerómetros, medidores, sensores del motor, teclado, GPS, ...

---

# PEAS para Agente de Compras por Internet

- Medida de rendimiento: precio, calidad, pertinencia, eficiencia
- Entorno: sitios web actuales y futuros, vendedores, transportistas
- Actuadores: mostrar al usuario, seguir URL, completar formulario
- Sensores: páginas HTML (texto, gráficos, scripts)

---

# Tipos de Entornos

| Propiedad | Solitario | Backgammon | Compras por Internet | Taxi |
|-----------|-----------|------------|----------------------|------|
| Observable | Sí | Sí | No | No |
| Determinista | Sí | No | Parcialmente | No |
| Episódico | Sí | No | No | No |
| Estático | Sí | Semi | Semi | No |
| Discreto | Sí | Sí | Sí | No |
| Agente único | Sí | No | Sí (excepto subastas) | No |

---

# Tipos de Entornos (cont.)

- El tipo de entorno determina en gran medida el diseño del agente
- El mundo real es (por supuesto) parcialmente observable, estocástico, secuencial, dinámico, continuo, multiagente

---

# Tipos de Agentes

Cuatro tipos básicos en orden de generalidad creciente:
1. Agentes de reflejo simple
2. Agentes de reflejo con estado
3. Agentes basados en objetivos
4. Agentes basados en utilidad

Todos estos pueden convertirse en agentes de aprendizaje

---

# Agentes de Reflejo Simple

![Agente de Reflejo Simple](https://mermaid.ink/img/pako:eNp1kc1OwzAQhF9l5QuVEidOaKFHJA5cOCFxQD20h9RZJxbOD7ZDFfXdcduUNgifsrMz3_rIFkpjkKEwNZwpD9VUO0TeY0dC1HvJ0RtG2JsbgrUaQr4G6jHuqZvZ2f4TipZwFFX0DBMHsnYNNYYdPYJiJCd-uAf-7lI4OD49O0_TbL5YLOfL1Wp9c7u5u3-4XC9nm_k8TZ_sBmoXiBwbzg7mEjx6qlzgyCR4VK2rOwl03SQVkPVNdWXNW2WgNI5qVWpA79GiA8kxOErKNQZyEo-Cna4QBn-w2_cAZGLnqAl9VflY8TlJf8kPuTi5fBhVqyWbSuKI7Y5i7L7tRHT_R5K_4uT_EcNJj1-6_tU-Aw7Jm7JV6LEhBmqcj_Wht3EtHyQk4c8Zd-SptDMVUtW0vGMF7_Q1pK-VKd6ZlTJZNXVrGF4ggwPzqxe_B9jF)

---

# Agentes de Reflejo con Estado

![Agente de Reflejo con Estado](https://mermaid.ink/img/pako:eNp1kstuwjAQRX_F8gaJJMYPIFl2qLro0krdoC7a4thDYuHYwR4qCvn3OgmFCsGsZu6c63lI21NtDDIUpob30oP8qB0h73FLQuw6ydEbRjiZHYK1GkLeBOoxnmiapXL-CUVLOIgi-gszB7J2CTVmC8_wm5Gc-OER-KVJ4ezy6vomTbPZfLGYzZfL1d397cPj0-1qOVvP52n6bB_g2QUix4azg7kEj55KFzgyCR6VdVUngS6bpAKyvqkurXkTDNra0ZtUGtA7tOhAcgyOknKNgZzEk2CnFcLgD3b7HoBM7Bw1oa8KHyt-TdK_5IdcnKwfRrVqzaaSuGE7oZi6L3sR3f-R5K84-X_EeNHxRZdX7RVgkLwqW4YeG2KgxvlYHwYb1_JCQhJ-yNiRp8LOVEhV0_KGFWzou4TktZbilVkpk1VTt4bhDTLYMb948QtuJV6i)

---

# Agentes Basados en Modelos

![Agente Basado en Modelos](https://mermaid.ink/img/pako:eNp1ks1u4jAUhV_FmgVSk4bwEwjLCqoWXXYxtKhddDG1L4mLY0f2DRUh3n3sBAZG6Cw-Ofc7vvZV9lQZgwyFKeBO9lC8VZaQ97glIernzFFuGOF9cAjWagi5CdRj3FN3HJWze4iWsBO58wczC7J2DsHZws8SBLmBbjRckBMvkHn3xUfB-9Pz81Wvl06nTqfT2Wx5f796fHq-Wczmi-k0SR7tI7y6QOTYsLYwleDRU-ECaybBo7JVWTuBzZqkBLJVXZ5Z8yEYNJWjjSg1oHdo0YHkGBwl5RoDOYl7wV3pEAa_s_P3AGRi66gOfVX4UPHVJPklP-TipHwYRVWLNpXEo7YjiYP3eSSi-z-S_BWH_I8YMrq4aPOqXQK0khdl89BjTQyuJg0VOrSxLK8kJOHPHDvyVNixCqmqG96xgE_6LqGrGz9dMitlsqxvGsbXyGDH_OCDXwxmcN0)

---

# Agentes Basados en Objetivos

![Agente Basado en Objetivos](https://mermaid.ink/img/pako:eNp1kstu2zAQRX-F4MZALFuSX7K8C9AF0UXRouhCWYjiSGJNkQxJuYiM_HtJS0lkoJ7NcOZyHsORR2pqjYwkiw5eZA31R-OIecdHEvJRqoxLwwiv2YHqukNMlxuNGE40TiLTvELeMu4id_5gYkG2dgmdswtPOQjqBl5HwwXVyBNkPn3xXvD-9Px8mSTpdOp0Op3Nlo-Pq6fnl7vFbL6YTtP00b7Cm_OkM9asLWwlZexpc4ENk-pRubrqnMBmTbJVZquuOLP2QzA4VI52YqtV3WNXo1KaY3Dkiu0YyEncSzfVDkHaH538HatMbB0NoS_zGCu-mqS_5IdcnJQfRlG3Yk2lcKPtRGLzvkxEdf9HUrzikP8RQ0ZXF21etUuATvGmbB57bInB1aRhCz1YOssbSUn4M8eefFYu10JV1fCBBXzSdwld1YTpW7ZVJsv6J2J8gwx2LN5t9AsV8HMz)

---

# Agentes Basados en Utilidad

![Agente Basado en Utilidad](https://mermaid.ink/img/pako:eNp1kstu2zAQRX-F4MZALFuSX7K8C9AF0UXRouhCWYjiSGJNkQxJuYiM_HtJS0lkoJ7NcOZyHsORR2pqjYwkiw5eZA31R-OIecdHEvJRqoxLwwiv2YHqukNMlxuNGE40TiLTvELeMu4id_5gYkG2dgmdswtPOQjqBl5HwwXVyBNkPn3xXvD-9Px8mSTpdOp0Op3Nlo-Pq6fnl7vFbL6YTtP00b7Cm_OkM9asLWwlZexpc4ENk-pRubrqnMBmTbJVZquuOLP2QzA4VI52YqtV3WNXo1KaY3Dkiu0YyEncSzfVDkHaH538HatMbB0NoS_zGCu-mqS_5IdcnJQfRlG3Yk2lcKPtRGLzvkxEdf9HUrzikP8RQ0ZXF21etUuATvGmbB57bInB1aRhCz1YOssbSUn4M8eefFYu10JV1fCBBXzSdwld1YTpW7ZVJsv6J2J8gwx2LN5t9AsV8HMz)

---

# Agentes de Aprendizaje

![Agente de Aprendizaje](https://mermaid.ink/img/pako:eNp1ks1u2zAMx1-F0CVAndhOPnzZpcCu2w4btsMuRQ-MRSVCLNGQ5HYo8u4jLSUxgvoikj--JZPU0UbXyEiyLOBVNlC91Y6Y93wgIe-lVLwyAng-OlRNcwzx8qMe44mmSVSar5BvGXeZB38wsSBrLWt2duZTDpK6gddouKAaeQLmyxevBe-Pj4-XWZZPJk6n09ls-fCwenp-uVvM5ovJJM8f7Ru8O886Y83awlZSxp42F9gyqR6Vq8rGCWzWJFtl1rLiv9Z-CAb7xtFGbBpV99g0qJTmGBy5YjsGchL30k21Q5D2RyX_xCoTW0d96KsixoqncfpffsjFCfxQiqoWjVLyWtuJxOZ9mYjq_o-keMUh_yOGjE7P2rxqlwCd4lXZItbYEoOrScMWe7B0lFeSkvBngT35rFyhharK-gMLqPTdzufr6fybWSmTZWNR-BNkMLD4MMEviWJvTQ)

---

# Resumen

- Los agentes interactúan con los entornos a través de actuadores y sensores
- La función del agente describe lo que el agente hace en todas las circunstancias
- La medida de rendimiento evalúa la secuencia del entorno
- Un agente perfectamente racional maximiza el rendimiento esperado
- Los programas de agente implementan (algunas) funciones de agente
- Las descripciones PEAS definen entornos de tareas
- Los entornos se categorizan a lo largo de varias dimensiones:
  ¿observable? ¿determinista? ¿episódico? ¿estático? ¿discreto? ¿agente único?
- Existen varias arquitecturas básicas de agentes:
  reflejo, reflejo con estado, basado en objetivos, basado en utilidad
