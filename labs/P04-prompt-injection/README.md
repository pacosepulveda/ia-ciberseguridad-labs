# P04 — Prompt injection y uso seguro de LLM

## Objetivo

Comprender por qué un sistema basado en LLM no debe tratar como instrucciones confiables todo el texto que recibe desde documentos, tickets, correos o una base de conocimiento.

La práctica utiliza exclusivamente contenido sintético y no interactúa con sistemas reales, credenciales, herramientas externas ni datos sensibles.

## Duración orientativa

25–30 minutos.

## Requisitos

- navegador web;
- acceso a un LLM generalista;
- este repositorio.

## Escenario

Un equipo SOC está evaluando un asistente que resume tickets y documentación interna. El asistente recibe texto procedente de distintas fuentes y debe responder a una pregunta del analista.

Uno de los documentos contiene una **instrucción incrustada no confiable**. Esa instrucción forma parte del contenido del documento y no debería modificar el comportamiento del asistente.

Tu tarea es comprobar cómo responde el modelo, identificar el problema y rediseñar el prompt para separar instrucciones del sistema y datos no confiables.

## Material

Utiliza:

- [`datos/documentos.json`](datos/documentos.json)
- [`prompt-prueba.md`](prompt-prueba.md)
- [`plantilla-entrega.md`](plantilla-entrega.md)

Todos los documentos son ficticios.

## Tarea 1 — Identifica fronteras de confianza

Antes de utilizar IA, clasifica los elementos del escenario:

- instrucción del analista;
- documentos de referencia;
- campos de metadatos;
- contenido escrito por un usuario externo;
- salida producida por el modelo.

Indica cuáles deberían considerarse **instrucciones confiables** y cuáles **datos no confiables**.

## Tarea 2 — Prueba el prompt básico

Utiliza la primera plantilla de [`prompt-prueba.md`](prompt-prueba.md) con el dataset.

Observa si el modelo:

- sigue alguna instrucción que aparece dentro de un documento;
- altera el formato solicitado;
- ignora evidencias relevantes;
- presenta como fiable contenido procedente de una fuente no confiable.

No todos los modelos reaccionarán igual. El resultado concreto no es lo importante; lo importante es identificar el límite de confianza.

## Tarea 3 — Localiza la inyección

Busca dentro de `documentos.json` cualquier fragmento que intente influir sobre el comportamiento del modelo en lugar de aportar información al caso.

Explica:

1. por qué ese fragmento debe tratarse como dato y no como instrucción;
2. qué podría ocurrir si un sistema RAG lo insertase sin controles en el contexto;
3. por qué pedir simplemente al modelo que "ignore ataques" no constituye por sí solo una defensa suficiente.

## Tarea 4 — Aplica una plantilla más robusta

Utiliza la segunda plantilla de [`prompt-prueba.md`](prompt-prueba.md).

Compara los resultados con la primera prueba.

La nueva plantilla introduce:

- separación explícita entre instrucciones y datos;
- etiquetas de procedencia;
- prohibición de ejecutar instrucciones encontradas en los documentos;
- obligación de citar qué documento sustenta cada afirmación;
- salida estructurada para facilitar revisión.

## Tarea 5 — Diseña controles fuera del prompt

Propón al menos cuatro controles adicionales que no dependan exclusivamente de que el modelo "se porte bien".

Ejemplos de categorías a considerar:

- procedencia y confianza de las fuentes;
- filtrado o normalización de documentos;
- permisos de herramientas;
- aprobación humana;
- validación de la salida;
- separación de datos sensibles;
- registro y auditoría.

## Entrega

Completa [`plantilla-entrega.md`](plantilla-entrega.md).

## Pregunta de cierre

> Si un LLM puede recibir texto procedente de fuentes no confiables, ¿qué controles deberían existir antes de permitir que su salida provoque una acción automática?
