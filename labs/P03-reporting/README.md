# P03 — Del análisis técnico al informe ejecutivo

## Objetivo

Aprender a utilizar un LLM para transformar una misma investigación de seguridad en comunicaciones adaptadas a distintos destinatarios sin perder precisión, inventar hechos ni exagerar el impacto.

La práctica pone el foco en una habilidad muy habitual en operaciones de seguridad: convertir evidencias técnicas en información útil para analistas, responsables de seguridad y dirección.

## Duración orientativa

20–25 minutos.

## Requisitos

- navegador web;
- acceso a un LLM generalista;
- este repositorio.

## Escenario

El SOC ha investigado una actividad sospechosa en una estación de trabajo. La investigación todavía no está cerrada, pero hay suficientes datos para informar a varias audiencias.

Dispones de un resumen técnico con hechos confirmados, hipótesis y datos pendientes. Debes generar tres versiones de la comunicación:

1. una nota de traspaso para otro analista SOC;
2. un resumen para el CISO o responsable de seguridad;
3. una actualización breve para dirección no técnica.

## Material

Utiliza:

- [`datos/incidente.json`](datos/incidente.json)
- [`prompt-reporting.md`](prompt-reporting.md)
- [`plantilla-entrega.md`](plantilla-entrega.md)

Todos los datos son sintéticos.

## Tarea 1 — Separa hechos de hipótesis

Antes de usar IA, clasifica cada afirmación del incidente en una de estas categorías:

- **hecho confirmado**;
- **inferencia razonable**;
- **dato todavía desconocido**.

Esta separación es importante porque el nivel de detalle puede cambiar entre audiencias, pero la certeza de los hechos no debería hacerlo.

## Tarea 2 — Genera una nota para SOC

Pide al LLM una versión destinada al siguiente analista que continuará la investigación.

Debe conservar:

- línea temporal esencial;
- host y usuario afectados;
- evidencias disponibles;
- hipótesis actuales;
- acciones ya realizadas;
- datos todavía pendientes;
- próximos pasos concretos.

Evita lenguaje de marketing o explicaciones excesivamente generales.

## Tarea 3 — Genera un resumen para CISO

La versión para el responsable de seguridad debe responder rápidamente a:

- qué sabemos;
- qué riesgo podría existir;
- qué se está haciendo;
- qué incertidumbres permanecen;
- si se necesita alguna decisión o escalado.

No debe convertir una sospecha en un incidente confirmado solo para sonar más contundente.

## Tarea 4 — Genera una actualización para dirección

Crea una versión de máximo 120 palabras para una audiencia no técnica.

Debe evitar jerga innecesaria y centrarse en:

- impacto conocido;
- exposición potencial;
- estado actual;
- siguiente hito de la investigación.

Si el impacto no está confirmado, debe decirlo explícitamente.

## Tarea 5 — Audita las tres versiones

Compara los textos generados con `incidente.json` y marca:

- cualquier dato inventado;
- cualquier aumento injustificado del nivel de certeza;
- información crítica que se haya perdido al resumir;
- tecnicismos que no sean apropiados para la audiencia;
- recomendaciones desproporcionadas respecto a la evidencia.

## Entrega

Completa [`plantilla-entrega.md`](plantilla-entrega.md) con las tres versiones finales y la auditoría del LLM.

## Pregunta de cierre

> ¿Qué información debe cambiar al adaptar un informe a otra audiencia y qué información no debería cambiar nunca?
