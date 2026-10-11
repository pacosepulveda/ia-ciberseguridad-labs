# Resumen sintético de investigación

## Hechos confirmados

- En `WS-FIN-23`, Microsoft Word abrió `factura_octubre.docm`.
- Word inició `powershell.exe`.
- PowerShell ejecutó `whoami /all` e `ipconfig /all`.
- Se observó una conexión TCP saliente desde PowerShell hacia una dirección IP sintética.
- El SOC aisló preventivamente el equipo de la red corporativa.
- No se han observado, con la información disponible, otros equipos con la misma secuencia.

## Inferencias razonables

- La cadena de procesos es inusual para un equipo de usuario.
- El documento puede estar relacionado con el inicio de la actividad.
- Existe riesgo potencial de compromiso del endpoint.

## No confirmado

- No está confirmada la ejecución de malware.
- No está confirmada la exfiltración de información.
- No está confirmado el robo de credenciales.
- No hay atribución a actor o campaña.
- No se conoce todavía si el documento llegó por correo, descarga web u otro canal.

## Estado actual

- Equipo aislado.
- Investigación en curso.
- Pendiente análisis del documento y revisión de telemetría adicional.

## Decisiones pendientes

- Determinar si es necesario ampliar la búsqueda a otros endpoints.
- Determinar si procede restablecer credenciales del usuario.
- Determinar cuándo puede volver el equipo a producción.
