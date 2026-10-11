# Prompt de reporting — P03

Copia el siguiente prompt y añade debajo el contenido de `datos/incidente.json`.

```text
Actúa como analista de ciberseguridad que debe comunicar una investigación en curso a varias audiencias.

Trabaja únicamente con los datos proporcionados. No inventes malware, impacto, exfiltración, credenciales comprometidas, responsables, alcance adicional ni acciones que no aparezcan en el incidente.

Distingue siempre entre:
- HECHOS CONFIRMADOS;
- INFERENCIAS;
- DATOS NO DISPONIBLES.

Genera tres versiones:

A) Nota de traspaso para SOC
- 250 a 400 palabras.
- Mantén detalles técnicos útiles para continuar la investigación.
- Incluye evidencias, hipótesis, acciones realizadas, incertidumbres y próximos pasos.

B) Resumen para CISO
- 150 a 220 palabras.
- Explica situación, riesgo potencial, medidas tomadas, incertidumbres y decisiones pendientes.
- No presentes una sospecha como compromiso confirmado.

C) Actualización para dirección
- Máximo 120 palabras.
- Lenguaje no técnico.
- Indica impacto confirmado, exposición potencial, estado y próximo hito.
- Si el impacto no está confirmado, dilo explícitamente.

Al final añade una sección titulada "Control de calidad" con:
1. tres afirmaciones que hayas mantenido deliberadamente con lenguaje de incertidumbre;
2. dos datos que hayas omitido de la versión ejecutiva por ser demasiado técnicos;
3. cualquier información que no hayas podido incluir porque no está disponible.
```

## Revisión posterior

Después de generar las tres versiones, utiliza:

```text
Compara tus tres textos con el incidente original. Señala cualquier dato que hayas añadido sin evidencia, cualquier cambio injustificado en el nivel de certeza y cualquier información crítica que se haya perdido al resumir. Corrige los textos si es necesario.
```
