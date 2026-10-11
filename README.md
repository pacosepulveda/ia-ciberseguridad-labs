# Introducción a la IA para Ciberseguridad — Laboratorios

Repositorio de prácticas del curso **Introducción a la IA para Ciberseguridad**.

## Enfoque del curso

Los laboratorios están diseñados para poder realizarse desde el navegador, sin instalaciones locales y utilizando herramientas gratuitas o de acceso general. El objetivo es que el alumno aprenda a integrar la IA en tareas reales de ciberseguridad sin depender de licencias empresariales específicas.

### Restricciones de diseño

- Sin instalaciones locales obligatorias.
- Los laboratorios deben poder realizarse con un **LLM generalista accesible desde web**.
- **Microsoft Security Copilot** y **Gemini en Google SecOps** se presentan como referencias del mercado, pero **no son necesarios para completar las prácticas**.
- Los datasets y artefactos de laboratorio son sintéticos o están preparados específicamente para formación.
- Las actividades se centran en análisis, detección, investigación, respuesta y uso seguro de IA.

## Laboratorios

| ID | Laboratorio | Objetivo principal |
|---|---|---|
| [P01](labs/P01-analisis-phishing/) | Análisis de phishing asistido por IA | Extraer evidencias, clasificar el riesgo y justificar conclusiones |
| [P02](labs/P02-deteccion-attack-sigma/) | De logs a ATT&CK y Sigma | Interpretar telemetría, formular hipótesis y proponer una detección |
| [P03](labs/P03-reporting/) | Del análisis técnico al informe ejecutivo | Adaptar una misma investigación a audiencias técnicas, CISO y dirección |
| [P04](labs/P04-prompt-injection/) | Prompt injection y uso seguro de LLM | Reconocer instrucciones no confiables y diseñar controles de mitigación |

Cada práctica incluye enunciado paso a paso, artefactos sintéticos, prompt de trabajo, plantilla de entrega y una solución orientativa.

## Alineación con el curso

Consulta [`docs/mapa-modulos-practicas.md`](docs/mapa-modulos-practicas.md) para ver cómo encajan las prácticas con M01–M05.

Resumen:

- **M01 — Fundamentos de IA y ciberseguridad:** introducción práctica con P01.
- **M02 — Uso profesional de LLM en Ciberseguridad:** P01 como práctica principal y P03 como extensión de comunicación.
- **M03 — IA para Detección, Investigación y Respuesta:** P02.
- **M04 — Seguridad de IA Generativa y Agentes:** P04.
- **M05 — Gobernanza, Uso Responsable y Adopción Segura de IA:** revisión transversal de P01–P04 desde riesgo, controles, trazabilidad y Human-in-the-Loop.

## Estructura

```text
.
├── labs/
│   ├── P01-analisis-phishing/
│   │   ├── README.md
│   │   ├── datos/
│   │   ├── prompt-analisis.md
│   │   ├── plantilla-entrega.md
│   │   └── solucion/
│   ├── P02-deteccion-attack-sigma/
│   │   ├── README.md
│   │   ├── datos/
│   │   ├── prompt-investigacion.md
│   │   ├── plantilla-entrega.md
│   │   └── solucion/
│   ├── P03-reporting/
│   │   ├── README.md
│   │   ├── datos/
│   │   ├── prompt-reporting.md
│   │   ├── plantilla-entrega.md
│   │   └── solucion/
│   └── P04-prompt-injection/
│       ├── README.md
│       ├── datos/
│       ├── prompt-prueba.md
│       ├── plantilla-entrega.md
│       └── solucion/
├── shared/
│   ├── prompts/
│   ├── checklists/
│   └── recursos/
└── docs/
    ├── guia-alumno.md
    └── mapa-modulos-practicas.md
```

## Método de trabajo recomendado

En todas las prácticas se sigue el mismo principio: **la IA ayuda a acelerar el análisis, pero no sustituye la verificación de evidencias**.

Cuando el LLM proponga una conclusión, el alumno debe poder responder a tres preguntas:

1. ¿Qué evidencia del artefacto original respalda esta afirmación?
2. ¿Qué parte es una inferencia del modelo y debería verificarse?
3. ¿Qué información adicional pediríamos antes de tomar una decisión operativa?

## Uso responsable

Los escenarios, dominios, usuarios, hashes y eventos del repositorio son sintéticos y están creados para formación. No deben introducirse en servicios públicos de IA credenciales, información confidencial, datos personales reales, secretos empresariales ni artefactos procedentes de incidentes reales sin autorización expresa de la organización.

## Estado

La **primera versión funcional de P01–P04 está completa**. El siguiente paso es revisar cada práctica contra el tiempo real disponible en clase y ajustar extensión, dificultad y material de apoyo si fuese necesario.
