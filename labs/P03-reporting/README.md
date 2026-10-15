# P03 — Del análisis técnico al informe ejecutivo

## Objetivo

Transformar una misma investigación sintética en comunicaciones adaptadas a distintas audiencias
sin perder precisión, incertidumbre ni trazabilidad.

La práctica trabaja una competencia muy importante en ciberseguridad: comunicar correctamente
lo que sabemos, lo que inferimos y lo que todavía no sabemos.

---

## Escenario

El SOC ha investigado una actividad inusual en una estación de trabajo de Finanzas.

Debes preparar tres salidas a partir del mismo conjunto de hechos:

1. nota técnica para otro analista;
2. resumen para CISO;
3. actualización breve para dirección.

La dificultad consiste en simplificar sin deformar.

---

## Material proporcionado

- `datos/resumen-incidente.md` — hechos e incertidumbres del caso.
- `prompt-reporting.md` — prompt estructurado.
- `plantilla-entrega.md` — plantilla del alumno.
- `solucion/solucion-orientativa.md` — referencia del instructor.

---

## Parte 1 — Identifica el núcleo del mensaje

Antes de utilizar IA, separa:

- hechos confirmados;
- inferencias;
- impacto potencial;
- impacto confirmado;
- acciones realizadas;
- decisiones pendientes.

---

## Parte 2 — Tres audiencias

Genera:

### Analista SOC
Puede incluir detalle técnico, procesos, hipótesis y datos faltantes.

### CISO
Debe centrarse en riesgo, confianza, alcance, controles y decisión pendiente.

### Dirección
Debe explicar impacto de negocio, estado actual y siguiente decisión sin jerga innecesaria.

---

## Parte 3 — Control de exageración

Comprueba que ninguna versión:

- convierta una hipótesis en un hecho;
- afirme un impacto no observado;
- invente usuarios afectados;
- invente exfiltración;
- atribuya actor o campaña;
- oculte incertidumbre importante.

---

## Criterios de evaluación

Se valorará:

- fidelidad al caso original;
- adecuación a la audiencia;
- concisión;
- claridad;
- conservación de incertidumbre;
- ausencia de exageración;
- trazabilidad de conclusiones.
