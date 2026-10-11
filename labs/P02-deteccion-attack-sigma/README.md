# P02 — De logs a MITRE ATT&CK y Sigma

## Objetivo

Investigar una secuencia de eventos **sintéticos** de endpoint, reconstruir qué ocurrió,
formular hipótesis, relacionar la actividad con MITRE ATT&CK y proponer una regla Sigma
de detección.

La práctica está orientada a análisis defensivo. No se ejecuta código ni se interactúa
con sistemas reales.

---

## Duración estimada

**35–45 minutos**

---

## Escenario

El equipo SOC recibe una alerta por actividad inusual en un equipo de usuario.

Dispones de un conjunto reducido de eventos de procesos y autenticación. Tu objetivo es
determinar qué hechos pueden afirmarse, qué hipótesis son razonables y qué información
adicional necesitarías antes de cerrar la investigación.

El flujo recomendado es:

`telemetría → línea temporal → hipótesis → ATT&CK → detección → validación`

---

## Material proporcionado

- `datos/eventos.jsonl` — telemetría sintética.
- `datos/contexto-entorno.md` — contexto mínimo.
- `prompt-investigacion.md` — prompt estructurado para el LLM.
- `plantilla-entrega.md` — plantilla del alumno.
- `solucion/solucion-orientativa.md` — referencia para el instructor.
- `solucion/regla-sigma-orientativa.yml` — ejemplo de detección defensiva.

---

## Parte 1 — Reconstrucción temporal

1. Ordena los eventos por fecha y hora.
2. Identifica relaciones padre-hijo entre procesos.
3. Señala qué eventos son claramente normales, cuáles son inusuales y cuáles requieren contexto.
4. Resume la secuencia en no más de 8 pasos.

---

## Parte 2 — Hipótesis

Formula al menos dos hipótesis:

- una que explique la actividad como potencialmente maliciosa;
- otra que contemple una explicación legítima o administrativa.

Para cada hipótesis indica qué evidencia la respalda y qué evidencia la debilitaría.

---

## Parte 3 — MITRE ATT&CK

Relaciona la actividad con técnicas ATT&CK solo cuando exista evidencia suficiente.

No conviertas una coincidencia superficial en una atribución definitiva.

Incluye:

- técnica o subtécnica;
- evidencia concreta;
- confianza;
- observaciones.

---

## Parte 4 — Sigma

Propón una regla Sigma que detecte el patrón más relevante de forma generalizable.

La regla debe:

- centrarse en comportamiento observable;
- evitar nombres de usuario o host excesivamente específicos;
- documentar falsos positivos esperables;
- ser revisable por otro analista antes de desplegarla.

---

## Parte 5 — Validación crítica

Compara la propuesta del LLM con los datos originales.

Marca cualquier:

- evento inventado;
- técnica ATT&CK no sustentada;
- causalidad asumida sin evidencia;
- condición Sigma demasiado amplia o demasiado específica.

---

## Criterios de evaluación

Se valorará:

- fidelidad a la telemetría;
- separación hecho/inferencia;
- calidad de la línea temporal;
- prudencia en el mapeo ATT&CK;
- utilidad defensiva de la regla Sigma;
- consideración de falsos positivos;
- capacidad para identificar información faltante.

---

## Mensaje didáctico

La IA puede acelerar la lectura y organización de telemetría, pero no sustituye
la validación del analista.

Una buena investigación conserva siempre la trazabilidad entre conclusión y evidencia.
