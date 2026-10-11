# P04 — Prompt injection y uso seguro de LLM

## Objetivo

Comprender por qué un sistema basado en LLM no debe tratar todo el texto recibido como
instrucciones confiables.

La práctica utiliza un escenario **completamente sintético** de asistente documental.
No se conectan herramientas reales, no se ejecutan acciones externas y no se manejan secretos.

---

## Duración estimada

**30–40 minutos**

---

## Escenario

Una organización utiliza un asistente interno para resumir documentos de su base de conocimiento.

El asistente recibe:

1. una instrucción del sistema;
2. una pregunta del usuario;
3. fragmentos recuperados desde una fuente documental.

Uno de los documentos recuperados contiene texto que intenta comportarse como una instrucción
para el modelo.

El objetivo es identificar por qué ese contenido no debe considerarse confiable y diseñar
controles adecuados.

---

## Material proporcionado

- `datos/instruccion-sistema.md`
- `datos/pregunta-usuario.md`
- `datos/documentos-recuperados.md`
- `prompt-prueba.md`
- `plantilla-entrega.md`
- `solucion/solucion-orientativa.md`

---

## Parte 1 — Clasifica las fuentes

Para cada bloque de texto identifica:

- quién lo controla;
- qué nivel de confianza tiene;
- si debe considerarse instrucción o dato;
- qué daño podría causar si se interpreta de forma incorrecta.

---

## Parte 2 — Detecta la inyección

Localiza el contenido que intenta cambiar el comportamiento del asistente.

Explica:

- por qué es contenido no confiable;
- por qué el hecho de estar dentro de un documento no le da autoridad;
- qué debería hacer el sistema con ese texto.

---

## Parte 3 — Diseña controles

Propón controles en varias capas:

- separación instrucciones/datos;
- procedencia de fuentes;
- mínimo privilegio;
- validación de salida;
- confirmación humana;
- registro y auditoría.

Evita confiar únicamente en “un prompt mejor”.

---

## Parte 4 — Revisión con LLM

Utiliza `prompt-prueba.md` para pedir al modelo que analice el escenario.

Después evalúa si el propio LLM:

- identifica correctamente la inyección;
- sobreestima la eficacia del prompting;
- propone controles arquitectónicos;
- mantiene la separación entre datos e instrucciones.

---

## Criterios de evaluación

Se valorará:

- comprensión del problema de confianza;
- capacidad de separar datos e instrucciones;
- diseño de controles por capas;
- aplicación de mínimo privilegio;
- uso de Human-in-the-Loop;
- razonamiento sobre trazabilidad y auditoría.
