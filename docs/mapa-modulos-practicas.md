# Mapa de módulos y prácticas

Este documento relaciona las prácticas del repositorio con el recorrido didáctico del curso **Introducción a la IA para Ciberseguridad**.

## M01 — Fundamentos de IA y ciberseguridad

### Objetivo del módulo

Introducir qué puede aportar la IA a tareas de ciberseguridad, qué límites tiene y por qué una respuesta convincente no equivale a una conclusión verificada.

### Práctica relacionada

**P01 — Análisis de phishing asistido por IA** puede utilizarse como primera demostración práctica del ciclo:

`artefacto → análisis → hipótesis → validación → decisión`

En M01 interesa especialmente observar cómo el alumno distingue señales evidentes, dudas y datos que faltan antes de apoyarse en el modelo.

---

## M02 — Uso profesional de LLM en Ciberseguridad

### Objetivo del módulo

Trabajar contexto, evidencia, restricciones, incertidumbre, formato de salida y validación. El flujo de referencia es:

`Contexto → Tarea → Evidencias → Restricciones → Formato → Validación`

### Prácticas relacionadas

**P01 — Análisis de phishing asistido por IA** es la práctica principal del módulo. Permite comparar:

- análisis humano inicial;
- prompt básico;
- prompt estructurado;
- revisión de afirmaciones;
- clasificación con nivel de confianza.

**P03 — Del análisis técnico al informe ejecutivo** puede utilizarse como extensión para trabajar formato, audiencia y conservación de la incertidumbre.

---

## M03 — IA para Detección, Investigación y Respuesta

### Objetivo del módulo

Pasar de telemetría y contexto a una investigación reproducible y, posteriormente, a una detección reutilizable.

### Práctica principal

**P02 — De logs a MITRE ATT&CK y Sigma**.

La práctica cubre:

- reconstrucción temporal;
- interpretación de procesos y relaciones padre-hijo;
- formulación de hipótesis;
- validación de técnicas MITRE ATT&CK;
- generación y revisión de una regla Sigma;
- discusión de falsos positivos y datos adicionales necesarios.

La IA se utiliza como copiloto de análisis, no como sustituto de la evidencia ni de la validación del analista.

---

## M04 — Seguridad de IA Generativa y Agentes

### Objetivo del módulo

Comprender riesgos como prompt injection, fuga de contexto, contaminación de fuentes RAG, exceso de capacidad de actuación y ausencia de límites de privilegio.

### Práctica principal

**P04 — Prompt injection y uso seguro de LLM**.

La práctica trabaja:

- separación entre instrucciones y datos;
- procedencia y confianza de fuentes;
- contenido no confiable recuperado por un sistema RAG;
- límites del prompting como mecanismo de seguridad;
- mínimo privilegio;
- validación de salida;
- Human-in-the-Loop;
- registro y auditoría.

Todo el escenario es sintético y no interactúa con sistemas reales ni credenciales.

---

## M05 — Gobernanza, Uso Responsable y Adopción Segura de IA

### Objetivo del módulo

Cerrar el curso conectando los casos de uso con riesgo, datos, controles, trazabilidad y supervisión humana.

### Uso de las prácticas del curso

M05 no necesita introducir un laboratorio técnico nuevo. Puede reutilizar las cuatro prácticas como casos para una revisión de gobernanza.

Para cada una, el alumno debería poder responder:

1. ¿Cuál es el problema que intentamos resolver?
2. ¿Cuál es el caso de uso de IA?
3. ¿Qué datos consume?
4. ¿Qué riesgos introduce?
5. ¿Qué controles ya existen?
6. ¿Qué controles adicionales necesita?
7. ¿Qué decisiones requieren revisión humana?
8. ¿Qué evidencias deberían registrarse para mantener trazabilidad?

### Matriz de cierre sugerida

| Práctica | Riesgo principal | Control clave | Revisión humana |
|---|---|---|---|
| P01 Phishing | sobreconfianza y alucinación | verificación contra evidencia | antes de clasificar o escalar |
| P02 Detección | mapeos o reglas incorrectas | validación ATT&CK/Sigma | antes de desplegar una detección |
| P03 Reporting | exageración del impacto | separación hecho/inferencia | antes de comunicación ejecutiva |
| P04 Prompt injection | instrucciones no confiables y exceso de agencia | aislamiento de datos, permisos mínimos y validación | antes de cualquier acción sensible |

El mensaje final del curso es que la adopción segura no depende solo del modelo elegido. Depende de diseñar correctamente el flujo completo: datos, instrucciones, permisos, validación, supervisión, registro y responsabilidad.
