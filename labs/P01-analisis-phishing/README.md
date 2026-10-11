# P01 — Análisis de phishing asistido por IA

## Objetivo

Usar un LLM generalista como apoyo para analizar correos sospechosos, extraer evidencias y redactar una conclusión que pueda ser revisada por un analista.

La práctica no consiste en preguntar simplemente «¿es phishing?». El objetivo es aprender a construir una investigación trazable y a detectar cuándo el modelo afirma más de lo que permiten las evidencias.

## Duración orientativa

20–25 minutos.

## Requisitos

- navegador web;
- acceso a un LLM generalista;
- este repositorio.

No se necesita instalar software ni utilizar una plataforma SIEM.

## Escenario

Formas parte de un pequeño equipo de seguridad. El servicio de soporte ha escalado varios mensajes recibidos por usuarios porque podrían ser intentos de phishing.

Tu tarea es realizar un primer triage asistido por IA. Para cada correo debes determinar qué evidencias son relevantes, qué hipótesis son razonables y qué información adicional necesitarías antes de tomar una decisión definitiva.

## Material

Utiliza el fichero [`datos/correos.json`](datos/correos.json).

Contiene varios correos sintéticos. Los dominios y URLs han sido preparados para formación y no deben interpretarse como indicadores reales.

## Tarea 1 — Análisis humano inicial

Antes de utilizar IA, revisa cada correo y anota rápidamente:

- remitente visible;
- dominio del remitente;
- asunto;
- URLs o dominios incluidos;
- señales de urgencia o presión;
- solicitudes de credenciales, pagos o acciones inusuales;
- incoherencias entre el texto y los metadatos disponibles.

No intentes todavía emitir una conclusión definitiva.

## Tarea 2 — Análisis con IA

Copia un correo completo en el LLM y utiliza la plantilla de [`prompt-analisis.md`](prompt-analisis.md).

Repite el proceso con los demás mensajes.

## Tarea 3 — Verificación

Para cada respuesta del modelo identifica al menos:

1. una afirmación respaldada directamente por el correo;
2. una inferencia razonable pero no demostrada;
3. cualquier dato inventado o supuesto por el modelo;
4. una evidencia adicional que pedirías para aumentar la confianza.

Ejemplos de evidencias adicionales podrían ser cabeceras completas, reputación histórica del dominio, registros del proxy, telemetría del endpoint o información sobre el usuario afectado.

## Tarea 4 — Clasificación

Asigna a cada correo una de estas categorías:

- **Probablemente legítimo**
- **Sospechoso — requiere verificación**
- **Probable phishing**

Añade un nivel de confianza: bajo, medio o alto.

La clasificación debe estar acompañada por evidencias observables.

## Tarea 5 — Entrega

Completa [`plantilla-entrega.md`](plantilla-entrega.md).

La entrega final debe ser breve. Un analista debería poder leerla y entender:

- qué has observado;
- qué conclusión propones;
- qué no puedes confirmar todavía;
- qué harías a continuación.

## Pregunta de cierre

Compara tu análisis inicial con el del LLM:

> ¿En qué parte de la investigación te ha ahorrado más tiempo la IA y en qué parte ha necesitado más supervisión humana?

Ese equilibrio entre velocidad y verificación será un tema recurrente durante todo el curso.
