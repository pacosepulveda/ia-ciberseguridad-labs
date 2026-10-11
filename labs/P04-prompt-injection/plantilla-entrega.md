# Plantilla de entrega — P04

## 1. Fronteras de confianza

| Elemento | Confiable como instrucción | Puede contener datos útiles | Riesgo principal |
|---|---|---|---|
| Instrucción del analista | Sí / No | Sí / No | |
| Procedimiento interno | Sí / No | Sí / No | |
| Ticket de usuario | Sí / No | Sí / No | |
| Metadatos del ticket | Sí / No | Sí / No | |
| Salida del LLM | Sí / No | Sí / No | |

## 2. Resultado de la Prueba A

- **Decisión producida por el modelo:**
- **¿Siguió contenido incrustado como si fuera una instrucción?:**
- **Evidencia:**
- **Otro problema observado:**

## 3. Fragmento de prompt injection identificado

- **Documento:**
- **Fragmento relevante:**
- **Por qué debe tratarse como dato y no como instrucción:**
- **Qué riesgo introduce en un sistema RAG o asistente conectado a herramientas:**

## 4. Resultado de la Prueba B

- **Decisión producida por el modelo:**
- **Evidencias citadas correctamente:**
- **¿Identificó el contenido no confiable?:**
- **Diferencias respecto a la Prueba A:**

## 5. Controles fuera del prompt

Propón al menos cuatro.

| Control | Qué riesgo reduce | Dónde se aplicaría |
|---|---|---|
| | | |
| | | |
| | | |
| | | |

## 6. Decisión final sobre TCK-1042

- **Decisión:** Aprobar / No aprobar / Requiere verificación adicional
- **Evidencia principal:**
- **Control que falta:**
- **Acción humana recomendada:**

## 7. Reflexión

En 3–5 líneas explica por qué la salida de un LLM que procesa contenido no confiable no debería conectarse directamente a una acción sensible sin controles adicionales.
