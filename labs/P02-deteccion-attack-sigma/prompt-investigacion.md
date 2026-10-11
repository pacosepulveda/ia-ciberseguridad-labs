# Prompt de investigación — P02

Copia el siguiente prompt y añade debajo el contenido de `datos/eventos.jsonl`.

```text
Actúa como analista SOC revisando una secuencia breve de eventos de seguridad sintéticos.

Trabaja únicamente con la evidencia proporcionada. No inventes eventos, malware, hashes, conexiones, procesos, usuarios, técnicas ATT&CK ni resultados de herramientas que no aparezcan en los datos.

Devuelve la respuesta con esta estructura:

1. Línea temporal
   - Resume los eventos en orden cronológico.

2. Hechos observables
   - Enumera solo hechos presentes en los registros.

3. Eventos más relevantes
   - Indica cuáles merecen investigación y por qué.

4. Hipótesis principal
   - Formula una hipótesis prudente sobre lo que pudo ocurrir.
   - Explica qué evidencia la apoya.

5. Explicaciones alternativas
   - Indica al menos una explicación legítima o menos grave que también sea compatible con los datos.

6. MITRE ATT&CK
   - Propón únicamente técnicas que puedas relacionar con un evento concreto.
   - Para cada técnica, indica el ID, nombre y evento que justificaría el mapeo.
   - Marca el mapeo como "pendiente de validación manual".

7. Detección Sigma
   - Propón una regla Sigma sencilla para el comportamiento más claro.
   - Usa solo campos que aparezcan en los eventos proporcionados.
   - Añade una sección de falsos positivos posibles.

8. Información adicional necesaria
   - Indica qué telemetría pedirías para confirmar o descartar la hipótesis.

9. Nivel de confianza
   - Bajo / medio / alto, con una explicación breve.

Distingue claramente entre HECHOS, INFERENCIAS y DATOS NO DISPONIBLES.
```

## Segunda pasada

Después de recibir la primera respuesta del modelo, utiliza:

```text
Audita tu respuesta anterior. Señala cualquier técnica ATT&CK, afirmación o campo Sigma que no esté respaldado por los eventos proporcionados. Corrige la respuesta y explica cada cambio.
```

El objetivo es comprobar si el modelo detecta sus propias sobreinferencias antes de que un analista las acepte.
