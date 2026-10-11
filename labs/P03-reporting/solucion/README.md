# Solución orientativa — P03

## 1. Qué no debe cambiar entre audiencias

Aunque el nivel de detalle sea distinto, las tres versiones deben conservar estos principios:

- la investigación sigue abierta;
- el endpoint fue aislado preventivamente;
- existe una secuencia sospechosa Word → PowerShell;
- hubo una conexión HTTPS asociada al mismo proceso;
- no se ha confirmado exfiltración, persistencia ni impacto sobre datos o credenciales;
- la finalidad de la conexión aún no está determinada.

La adaptación a la audiencia nunca debe transformar una hipótesis en un hecho confirmado.

---

## 2. Ejemplo de nota de traspaso para SOC

**INC-2026-0142 — Investigación en curso**

El host `WS-023`, asociado al usuario `EMPRESA\\ana.garcia`, presentó una secuencia de ejecución que requiere investigación prioritaria. Tras abrirse un documento de Office descargado, `WINWORD.EXE` inició `powershell.exe` con el argumento `-EncodedCommand`. El proceso PowerShell realizó posteriormente una conexión HTTPS a `cdn-updates.example` y ejecutó `whoami.exe /all`.

El comportamiento es compatible con ejecución de código iniciada desde un documento, pero todavía no se ha determinado el contenido del argumento codificado ni la finalidad de la conexión. No existe evidencia confirmada de exfiltración, persistencia, descarga de contenido adicional o compromiso de credenciales.

Como medida preventiva, el endpoint fue aislado de la red corporativa a las 10:28Z. Se ha preservado la telemetría disponible y la búsqueda inicial no ha identificado actividad equivalente en otros endpoints.

Pendiente: revisar la telemetría EDR del proceso PowerShell, analizar el documento de origen en un entorno controlado, determinar el contexto de la conexión y revisar actividad posterior del usuario y del host. La evaluación de impacto deberá actualizarse cuando exista nueva evidencia.

---

## 3. Ejemplo de resumen para CISO

Se investiga actividad sospechosa detectada en una estación de trabajo corporativa. La secuencia observada incluye la apertura de un documento de Office seguida de la ejecución de PowerShell y una conexión de red asociada. El comportamiento justifica una investigación prioritaria, pero todavía no permite confirmar un compromiso completo del equipo.

Como medida preventiva, el endpoint afectado ha sido aislado y se ha preservado la telemetría disponible. La revisión inicial no ha identificado el mismo patrón en otros equipos.

En este momento **no se ha confirmado impacto sobre datos, credenciales o servicios**, ni existen evidencias confirmadas de exfiltración o persistencia. Quedan pendientes el análisis del documento, la revisión detallada de la actividad de PowerShell y la determinación de la finalidad de la conexión observada.

La siguiente actualización debería producirse cuando se disponga de esas evidencias y pueda revisarse el alcance e impacto con mayor confianza.

---

## 4. Ejemplo de actualización para dirección

Se está investigando una actividad inusual detectada en un equipo corporativo. El equipo ha sido aislado preventivamente y, por el momento, no se ha identificado el mismo comportamiento en otros dispositivos.

Aún **no se ha confirmado impacto sobre datos, credenciales ni servicios**. El análisis continúa para determinar qué ejecutó el equipo y si la conexión de red observada tuvo alguna consecuencia adicional.

La próxima actualización se realizará cuando finalice la revisión técnica inicial y pueda evaluarse con mayor precisión el alcance del incidente.

---

## 5. Errores que deberían penalizarse

- afirmar que hubo malware confirmado;
- afirmar que existió exfiltración;
- decir que las credenciales del usuario fueron robadas;
- convertir `prioridad: media` en una crisis crítica sin nueva evidencia;
- inventar un atacante, una campaña o un grupo de amenaza;
- decir que el dominio era malicioso basándose solo en el dataset;
- omitir en la versión ejecutiva que el impacto sigue sin confirmarse.

## 6. Criterio de corrección

La mejor entrega no es necesariamente la más extensa. Debe mantener consistencia factual, adaptar correctamente el nivel de detalle y conservar las incertidumbres que sean relevantes para la toma de decisiones.
