# P04 — Prompt injection y uso seguro de LLM

## Objetivo

Comprender por qué un sistema basado en LLM no debe tratar todo el texto recibido como
instrucciones confiables.

La práctica utiliza un escenario **completamente sintético** de asistente documental.
No se conectan herramientas reales, no se ejecutan acciones externas y no se manejan secretos.

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

> **Importante:** no es necesario que el modelo obedezca la prompt injection para completar la
> práctica. Algunos servicios, incluido Microsoft Copilot, pueden bloquear o rechazar directamente
> una solicitud cuando detectan contenido que parece una prompt injection. Ese rechazo es también
> un resultado válido del laboratorio y debe analizarse.

---

## Material proporcionado

- `datos/instruccion-sistema.md`
- `datos/pregunta-usuario.md`
- `datos/documentos-recuperados.md` — contiene el ejemplo adversarial literal.
- `datos/documentos-recuperados-analisis.md` — versión de contingencia que describe la inyección sin incluirla como instrucción activa.
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

## Parte 4 — Prueba con LLM

### Intento A — Documento adversarial literal

Utiliza `prompt-prueba.md` junto con:

- `datos/instruccion-sistema.md`;
- `datos/pregunta-usuario.md`;
- `datos/documentos-recuperados.md`.

Pueden ocurrir tres resultados:

1. **El modelo intenta obedecer el contenido adversarial.** Analiza qué fuente consiguió influir en la respuesta.
2. **El modelo detecta la inyección y la ignora.** Analiza por qué ese comportamiento es correcto, pero no demuestra por sí solo que toda la arquitectura sea segura.
3. **La plataforma rechaza procesar la solicitud.** Registra el rechazo como una mitigación observada de la plataforma. No asumas qué mecanismo interno concreto se activó si la interfaz no lo indica.

### Intento B — Fallback de análisis seguro

Si el servicio rechaza la solicitud o impide completar el ejercicio, sustituye únicamente
`datos/documentos-recuperados.md` por:

`datos/documentos-recuperados-analisis.md`

Esta versión conserva el escenario, pero describe el intento de inyección en lugar de presentarlo
como una instrucción literal dirigida al modelo.

Vuelve a utilizar `prompt-prueba.md` y evalúa si el LLM:

- clasifica correctamente la confianza de las fuentes;
- identifica el intento de obtener autoridad;
- propone una respuesta basada en los documentos válidos;
- distingue controles de prompting y controles arquitectónicos;
- aplica mínimo privilegio y Human-in-the-Loop.

---

## Parte 5 — Qué hemos aprendido del rechazo

Si Copilot u otro servicio bloquea el primer intento, no consideres la práctica fallida.

El rechazo permite discutir una capa adicional:

```text
Contenido no confiable
        ↓
Protecciones de la plataforma
        ↓
Modelo
        ↓
Controles de la aplicación
        ↓
Autorización / acción
```

Una protección del proveedor puede reducir el riesgo, pero no sustituye a los controles del
sistema que integra el LLM.

---

## Criterios de evaluación

Se valorará:

- comprensión del problema de confianza;
- capacidad de separar datos e instrucciones;
- interpretación correcta de un rechazo o bloqueo de la plataforma;
- diseño de controles por capas;
- aplicación de mínimo privilegio;
- uso de Human-in-the-Loop;
- razonamiento sobre trazabilidad y auditoría.
