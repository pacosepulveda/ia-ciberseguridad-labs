# P02 — De logs a MITRE ATT&CK y Sigma

## Objetivo

Utilizar un LLM como apoyo para investigar una secuencia breve de eventos de seguridad, formular una hipótesis, relacionarla con MITRE ATT&CK y proponer una regla Sigma que después debe revisarse manualmente.

La práctica está diseñada para trabajar con telemetría sintética y no requiere SIEM ni instalaciones locales.

## Duración orientativa

25–30 minutos.

## Requisitos

- navegador web;
- acceso a un LLM generalista;
- acceso a la web pública de MITRE ATT&CK para comprobar las técnicas;
- este repositorio.

## Escenario

El equipo SOC recibe una alerta asociada a una estación Windows. No se dispone de una investigación previa: solo de una pequeña secuencia de eventos exportados desde distintas fuentes.

Tu tarea es reconstruir qué pudo ocurrir, distinguir hechos de hipótesis y diseñar una detección sencilla que pueda ser revisada por otro analista.

## Material

Utiliza:

- [`datos/eventos.jsonl`](datos/eventos.jsonl)
- [`prompt-investigacion.md`](prompt-investigacion.md)
- [`plantilla-entrega.md`](plantilla-entrega.md)

Los nombres de host, usuarios, hashes, dominios y direcciones son sintéticos y están preparados para formación.

## Tarea 1 — Reconstruye la línea temporal

Sin utilizar todavía el LLM:

1. Ordena los eventos por hora.
2. Identifica usuario, host y procesos implicados.
3. Señala relaciones padre-hijo entre procesos cuando estén disponibles.
4. Marca los eventos que te parezcan más relevantes.
5. Escribe una primera hipótesis en una sola frase.

## Tarea 2 — Pide una segunda lectura a la IA

Utiliza [`prompt-investigacion.md`](prompt-investigacion.md) junto con el contenido de `eventos.jsonl`.

Compara la respuesta del modelo con tu análisis inicial.

Comprueba especialmente si el modelo:

- inventa eventos que no existen;
- da por demostrado un compromiso cuando solo existe actividad sospechosa;
- atribuye intención al usuario o al proceso sin evidencia suficiente;
- propone técnicas ATT&CK sin justificar qué evento las respalda.

## Tarea 3 — Valida MITRE ATT&CK

Para cada técnica propuesta por el LLM:

1. busca la técnica en MITRE ATT&CK;
2. comprueba que el comportamiento observado encaja realmente;
3. anota el evento que sustenta el mapeo;
4. descarta cualquier técnica que dependa de hechos no presentes en los datos.

No se evalúa cuántas técnicas consigues asociar, sino la calidad de la justificación.

## Tarea 4 — Diseña una regla Sigma

Pide al LLM que proponga una regla Sigma para detectar el comportamiento más claro de la secuencia.

Después revísala manualmente:

- ¿el `logsource` corresponde con los datos disponibles?
- ¿los campos utilizados existen en los eventos?
- ¿la condición es demasiado amplia?
- ¿podría generar falsos positivos razonables?
- ¿el título y la descripción explican qué detecta realmente?

No aceptes la regla solo porque el YAML sea válido visualmente.

## Tarea 5 — Mejora la detección

Propón al menos una mejora, por ejemplo:

- añadir contexto del proceso padre;
- exigir una combinación de argumentos;
- limitar la detección a un tipo concreto de telemetría;
- documentar una exclusión legítima conocida;
- separar una detección de alta cobertura de otra de mayor precisión.

## Entrega

Completa [`plantilla-entrega.md`](plantilla-entrega.md).

El resultado debe permitir que otro analista entienda:

- qué ocurrió según las evidencias;
- qué parte sigue siendo una hipótesis;
- qué técnicas ATT&CK se han validado;
- qué detecta exactamente la regla Sigma;
- qué falsos positivos podrían aparecer.

## Pregunta de cierre

> ¿Qué parte te resultó más fiable en el LLM: ordenar y resumir los eventos, mapear ATT&CK o escribir la regla Sigma? ¿Cuál necesitó más verificación manual?
