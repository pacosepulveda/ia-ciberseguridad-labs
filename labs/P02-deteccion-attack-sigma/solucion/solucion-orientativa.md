# Solución orientativa — P02

## Conclusión

La secuencia presenta un patrón que merece investigación:

`WINWORD.EXE → powershell.exe → whoami.exe / ipconfig.exe / cmd.exe`

El hecho más relevante no es la existencia de PowerShell por sí sola, sino que una
aplicación Office lo inicia y a continuación aparecen comandos de descubrimiento.

## Hechos observables

- Word abrió un archivo `.docm`.
- Word inició PowerShell.
- PowerShell ejecutó `whoami /all` e `ipconfig /all`.
- PowerShell originó una conexión TCP hacia una IP sintética.
- PowerShell inició `cmd.exe`.
- No se dispone del contenido del documento ni de la causa que originó el proceso.

## Hipótesis

Una hipótesis defensiva razonable es que el documento desencadenó una secuencia no habitual.
Sin embargo, no puede afirmarse que exista malware únicamente con estos datos.

También sería posible, aunque menos probable según el contexto, que se trate de una automatización
legítima o una prueba interna.

## ATT&CK razonable

- **T1059.001 — PowerShell**: respaldado por la ejecución observada de `powershell.exe`.
- **T1033 — System Owner/User Discovery**: respaldado por la ejecución de `whoami /all`.
- **T1016 — System Network Configuration Discovery**: respaldado por `ipconfig /all`.

El mapeo ATT&CK debe apoyarse en comportamiento observable y contexto. El hecho de que un comando
pueda asociarse a una técnica no demuestra por sí mismo intención maliciosa.

## Sigma

La regla orientativa incluida detecta Office generando PowerShell. Es deliberadamente simple,
generalizable y defensiva.

Antes de desplegarla deberían evaluarse falsos positivos y adaptarla al esquema real del SIEM.

Para una prueba rápida, consulta `PRUEBA-SIGMA.md` y los eventos de
`../datos/eventos-prueba-sigma.jsonl`.

## Datos adicionales

- contenido y origen del documento;
- firma o procedencia;
- árbol completo de procesos;
- eventos de red enriquecidos;
- telemetría EDR;
- prevalencia del patrón en otros equipos;
- actividad posterior del usuario.

## Error típico del LLM

Un modelo podría afirmar automáticamente que el documento es malicioso o identificar una campaña.
Eso no está demostrado con la evidencia disponible.
