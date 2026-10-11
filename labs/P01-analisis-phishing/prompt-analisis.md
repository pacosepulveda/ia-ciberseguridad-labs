# Prompt de análisis

Copia el siguiente prompt y, debajo, añade el contenido completo de uno de los correos del dataset.

```text
Actúa como analista de ciberseguridad realizando un triage inicial de un correo sospechoso.

Analiza únicamente la información proporcionada. No inventes cabeceras, reputación de dominios, resultados de sandbox, información WHOIS ni telemetría que no aparezca en el artefacto.

Devuelve la respuesta con esta estructura:

1. Hechos observables
   - Lista solo elementos presentes en el correo.

2. Señales de riesgo
   - Explica por qué cada señal puede ser relevante.

3. Elementos que reducen el riesgo o generan duda
   - Señala cualquier evidencia que impida afirmar con certeza que se trata de phishing.

4. Hipótesis
   - Indica la hipótesis principal y, si procede, una alternativa.

5. Clasificación provisional
   - Probablemente legítimo / Sospechoso — requiere verificación / Probable phishing.
   - Nivel de confianza: bajo / medio / alto.

6. Información adicional necesaria
   - Indica qué datos pedirías para confirmar o descartar la hipótesis.

7. Resumen para un analista
   - Máximo 5 líneas.

Distingue claramente entre HECHOS, INFERENCIAS y DATOS NO DISPONIBLES.
```

## Variante de comprobación

Después del primer análisis, puedes preguntar:

```text
Revisa tu respuesta anterior. Identifica cualquier afirmación que no esté respaldada directamente por el correo y corrígela o rebaja su nivel de certeza.
```

El objetivo de esta segunda interacción es comprobar si el modelo es capaz de autocorregir afirmaciones demasiado seguras.
