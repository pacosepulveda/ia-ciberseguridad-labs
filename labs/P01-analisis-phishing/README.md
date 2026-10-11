# P01 — Análisis de phishing asistido por IA

## Objetivo

Analizar un correo electrónico **sintético** potencialmente fraudulento utilizando un LLM como apoyo, sin delegar en el modelo la decisión final.

La práctica está diseñada para trabajar:

- extracción de evidencias observables;
- separación entre hechos e inferencias;
- identificación de señales de riesgo;
- formulación de hipótesis;
- estimación razonada del nivel de confianza;
- propuesta de acciones de validación;
- revisión humana antes de cualquier decisión operativa.

> Todo el material de esta práctica es ficticio y ha sido creado exclusivamente con fines formativos.

---

## Duración estimada

**25–35 minutos**

---

## Escenario

Trabajas en un equipo de seguridad que recibe una alerta sobre un correo sospechoso remitido a una persona del área financiera.

Tu tarea consiste en revisar el mensaje, identificar señales relevantes y preparar una conclusión que pueda ser revisada por otro analista.

No debes asumir que el mensaje es malicioso solo porque parezca sospechoso. La conclusión debe estar vinculada a evidencias concretas.

---

## Material proporcionado

- `datos/correo-sintetico.txt` — correo ficticio a analizar.
- `datos/contexto-organizacion.md` — contexto mínimo del entorno.
- `datos/indicadores-sinteticos.json` — datos complementarios preparados para la práctica.
- `prompt-analisis.md` — prompt estructurado recomendado.
- `plantilla-entrega.md` — plantilla para documentar el análisis.
- `solucion/solucion-orientativa.md` — propuesta de resolución para el instructor.

---

## Parte 1 — Revisión humana inicial

Antes de utilizar IA:

1. Lee el correo completo.
2. Identifica al menos **5 elementos observables** que puedan ser relevantes.
3. Clasifica cada uno como:
   - normal;
   - sospechoso;
   - desconocido / requiere validación.
4. Anota qué información adicional necesitarías para decidir con mayor seguridad.

No busques todavía una conclusión definitiva.

---

## Parte 2 — Análisis con un LLM

Utiliza el contenido de `prompt-analisis.md`.

Copia en el modelo:

1. el prompt;
2. el correo sintético;
3. el contexto de la organización;
4. los indicadores sintéticos.

No introduzcas datos reales de tu empresa, credenciales ni información personal.

---

## Parte 3 — Verificación crítica

Compara tu análisis inicial con la respuesta del modelo.

Para cada afirmación importante del LLM, responde:

- ¿Está respaldada por una evidencia concreta?
- ¿Es una inferencia razonable?
- ¿Es una afirmación no demostrada?
- ¿Qué dato adicional permitiría confirmarla o descartarla?

Presta especial atención a cualquier afirmación excesivamente categórica.

---

## Parte 4 — Decisión

Completa `plantilla-entrega.md`.

La decisión final debe incluir:

- nivel de riesgo estimado;
- confianza de la conclusión;
- evidencias principales;
- aspectos no verificados;
- siguiente acción recomendada;
- justificación de por qué esa acción es proporcional.

---

## Criterios de evaluación

Se valorará especialmente que el alumno:

- no confunda indicadores con pruebas definitivas;
- cite evidencias específicas del artefacto;
- separe observación e inferencia;
- mantenga la incertidumbre cuando falten datos;
- no copie ciegamente la respuesta del modelo;
- proponga acciones de validación realistas.

---

## Mensaje didáctico

La IA puede acelerar el análisis, resumir señales y ayudar a estructurar una hipótesis.

Pero la calidad del resultado depende de tres factores:

**evidencia + contexto + validación humana**

Una respuesta convincente del modelo no equivale a una conclusión verificada.
