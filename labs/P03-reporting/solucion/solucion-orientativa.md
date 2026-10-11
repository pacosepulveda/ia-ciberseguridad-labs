# Solución orientativa — P03

## A. Nota técnica SOC

En `WS-FIN-23` se observó una cadena de procesos inusual iniciada tras la apertura de
`factura_octubre.docm`: `WINWORD.EXE → powershell.exe`, seguida de `whoami /all`,
`ipconfig /all` y una conexión TCP saliente desde PowerShell.

La relación entre el documento y la actividad es una hipótesis razonable, pero todavía
no se ha confirmado ejecución de malware ni exfiltración. El equipo ha sido aislado de
forma preventiva. No se han observado por ahora otros endpoints con la misma secuencia.

Siguientes pasos: analizar el documento, ampliar telemetría EDR y de red, buscar el patrón
en otros equipos y determinar el origen del archivo.

## B. Resumen CISO

Se ha aislado preventivamente un equipo de Finanzas tras detectar una secuencia de procesos
inusual asociada temporalmente a la apertura de un documento. El alcance conocido está limitado
actualmente a un endpoint. No existe evidencia confirmada de exfiltración ni robo de credenciales.

La investigación continúa para determinar si el documento originó la actividad y si es necesario
ampliar la búsqueda a otros equipos. El riesgo se considera relevante, pero el impacto todavía
no está confirmado.

## C. Dirección

Se ha detectado actividad inusual en un equipo de Finanzas y se ha aislado preventivamente.
Por el momento no se ha confirmado pérdida de información ni afectación a otros equipos.
El equipo de seguridad está analizando el origen del incidente y revisando si es necesario
ampliar las medidas de protección.

## Punto didáctico

La versión ejecutiva debe ser más corta, no más categórica.
