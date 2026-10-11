# Introducción a la IA para Ciberseguridad — Laboratorios

Repositorio de prácticas del curso **Introducción a la IA para Ciberseguridad**.

## Enfoque del curso

Los laboratorios están diseñados para poder realizarse desde el navegador, sin instalaciones locales y utilizando herramientas gratuitas o de acceso general. El objetivo es que el alumno aprenda a integrar la IA en tareas reales de ciberseguridad sin depender de licencias empresariales específicas.

### Restricciones de diseño

- Duración total del curso: **5 horas**.
- Grupo previsto: **22 alumnos**.
- Sin instalaciones locales obligatorias.
- Los laboratorios deben poder realizarse con un **LLM generalista accesible desde web**.
- **Microsoft Security Copilot** y **Gemini en Google SecOps** se presentan como referencias del mercado, pero **no son necesarios para completar las prácticas**.
- Los datasets y artefactos de laboratorio son sintéticos o están preparados específicamente para formación.
- Las actividades se centran en análisis, detección, investigación, respuesta y uso seguro de IA.

## Laboratorios

| ID | Laboratorio | Objetivo principal |
|---|---|---|
| P01 | Análisis de phishing asistido por IA | Extraer evidencias, clasificar el riesgo y justificar conclusiones |
| P02 | De logs a ATT&CK y Sigma | Interpretar telemetría, formular hipótesis y proponer una detección |
| P03 | Del análisis técnico al informe ejecutivo | Adaptar una misma investigación a audiencias técnicas, CISO y dirección |
| P04 | Prompt injection y uso seguro de LLM | Reconocer instrucciones maliciosas y diseñar controles de mitigación |

## Estructura

```text
.
├── labs/
│   ├── P01-analisis-phishing/
│   ├── P02-deteccion-attack-sigma/
│   ├── P03-reporting/
│   └── P04-prompt-injection/
├── shared/
│   ├── prompts/
│   ├── checklists/
│   └── recursos/
└── docs/
    └── guia-alumno.md
```

## Método de trabajo recomendado

En todas las prácticas se sigue el mismo principio: **la IA ayuda a acelerar el análisis, pero no sustituye la verificación de evidencias**.

Cuando el LLM proponga una conclusión, el alumno debe poder responder a tres preguntas:

1. ¿Qué evidencia del artefacto original respalda esta afirmación?
2. ¿Qué parte es una inferencia del modelo y debería verificarse?
3. ¿Qué información adicional pediríamos antes de tomar una decisión operativa?

## Estado

El repositorio se encuentra en construcción. Los laboratorios se irán incorporando de forma incremental conforme se preparen las prácticas del curso.
