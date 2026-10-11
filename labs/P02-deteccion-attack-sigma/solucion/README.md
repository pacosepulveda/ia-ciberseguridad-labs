# Solución orientativa — P02

## 1. Reconstrucción de la secuencia

La actividad relevante comienza a las `10:16:11Z` cuando `WINWORD.EXE` abre `Informe-Q4.docx`. Veintiocho segundos después, Word crea un proceso `powershell.exe` con el argumento `-EncodedCommand`. Ese PowerShell realiza después una consulta DNS y una conexión HTTPS a `cdn-updates.example`, ejecuta `whoami.exe /all` y crea un fichero temporal.

El evento de `notepad.exe` de las `10:18:03Z` no presenta, por sí solo, una relación clara con la secuencia anterior y sirve como ejemplo de ruido legítimo dentro de la telemetría.

## 2. Hechos observables

- El host es `WS-023` y el usuario es `EMPRESA\\ana.garcia`.
- Word abre un documento descargado desde la carpeta `Downloads`.
- `WINWORD.EXE` aparece como proceso padre de `powershell.exe`.
- PowerShell utiliza `-NoProfile` y `-EncodedCommand`.
- El mismo PID de PowerShell realiza una resolución DNS y una conexión TCP/443.
- PowerShell crea posteriormente `whoami.exe /all` como proceso hijo.
- Se crea un fichero de texto en el directorio temporal del usuario.

## 3. Hipótesis prudente

La secuencia es **compatible con la ejecución de PowerShell iniciada desde un documento de Office y seguida de actividad de red y descubrimiento local**. Es razonable considerarla sospechosa y priorizar su investigación.

Con estos datos no puede afirmarse todavía que exista malware, persistencia, exfiltración o control remoto. Tampoco puede demostrarse que el dominio contactado sea malicioso: es un dominio sintético del laboratorio.

## 4. MITRE ATT&CK

### T1059.001 — Command and Scripting Interpreter: PowerShell

Es el mapeo más sólido porque existe un evento explícito de creación de `powershell.exe`.

**Evidencia:** evento de las `10:16:39Z`.

### T1087 — Account Discovery

Puede considerarse un mapeo razonable por la ejecución de `whoami.exe /all`, que obtiene información sobre la identidad y pertenencia a grupos del contexto actual.

**Evidencia:** evento de las `10:17:08Z`.

### Mapeos que no deberían darse por demostrados

Una conexión HTTPS no basta por sí sola para afirmar `T1071.001 Web Protocols` como canal de mando y control. Para ello haría falta más contexto sobre la finalidad de la conexión. Del mismo modo, no existe evidencia suficiente para afirmar descarga de herramientas, persistencia o exfiltración.

## 5. Regla Sigma orientativa

Una detección sencilla y defendible consiste en buscar PowerShell con `-EncodedCommand` cuando el proceso padre sea Microsoft Word.

```yaml
title: PowerShell Encoded Command Spawned by Microsoft Word
id: 2fcba9f6-68c5-4f37-a1bf-ia-course-p02
status: experimental
description: Detecta PowerShell con EncodedCommand iniciado desde Microsoft Word en la telemetría sintética del laboratorio P02.
logsource:
  category: process_creation
  product: windows
detection:
  selection_parent:
    parent_image|endswith: '\\WINWORD.EXE'
  selection_child:
    image|endswith: '\\powershell.exe'
    command_line|contains: '-EncodedCommand'
  condition: selection_parent and selection_child
falsepositives:
  - Automatizaciones administrativas o documentos corporativos que invoquen PowerShell de forma controlada.
level: high
```

## 6. Revisión de la regla

La regla deliberadamente prioriza **precisión contextual** frente a cobertura. Una regla que buscase cualquier PowerShell con `-EncodedCommand` tendría más cobertura, pero también podría generar más falsos positivos administrativos.

En un entorno real habría que adaptar los nombres de campos al backend concreto y comprobar si la telemetría disponible conserva proceso padre y línea de comandos.

## 7. Datos adicionales que pediríamos

- contenido o procedencia validada de `Informe-Q4.docx`;
- línea de comandos completa o contenido decodificado del argumento, si la política y las herramientas del entorno lo permiten;
- telemetría EDR del proceso PowerShell;
- detalles HTTP/TLS o proxy asociados a la conexión;
- reputación y contexto interno del destino;
- actividad posterior del host y del usuario;
- eventos de creación, modificación o ejecución relacionados con el fichero temporal.

## 8. Qué debería aprender el alumno sobre el LLM

El modelo suele ser útil para ordenar la línea temporal y proponer una primera regla, pero requiere especial revisión en dos áreas:

1. **ATT&CK:** puede asignar demasiadas técnicas a partir de una señal débil.
2. **Sigma:** puede utilizar nombres de campo que no existen o producir una regla sintácticamente plausible pero semánticamente incorrecta.

La evaluación debe premiar que el alumno elimine sobreinferencias y pueda señalar la evidencia concreta que sustenta cada conclusión.
