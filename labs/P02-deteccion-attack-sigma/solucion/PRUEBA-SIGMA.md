# Cómo probar la regla Sigma de P02

Esta guía permite probar la regla Sigma de la práctica **sin instalar un SIEM ni utilizar línea de comandos**.

La prueba se realiza con **Enclave Rule Tester**, una herramienta web que ejecuta el análisis localmente en el navegador:

<https://tools.winterstetter.io/rule-tester>

La validación tiene dos objetivos distintos:

1. comprobar que la lógica de la regla detecta el comportamiento que buscamos;
2. comprobar que no dispara ante algunos eventos negativos sencillos.

> El objetivo de esta práctica no es certificar una regla para producción, sino mostrar de forma verificable la relación **telemetría → lógica Sigma → detección**.

---

## 1. Archivos utilizados

Para esta prueba se utilizan:

- `regla-sigma-orientativa.yml` — regla Sigma que queremos evaluar;
- `../datos/eventos-prueba-sigma.jsonl` — conjunto pequeño de eventos diseñados específicamente para probar la regla.

En el laboratorio existen además:

- `../datos/eventos.jsonl` — telemetría completa del escenario de investigación;
- `../datos/eventos.txt` — exactamente el mismo contenido que `eventos.jsonl`, pero con extensión `.txt` para poder utilizarlo en herramientas que no permiten adjuntar archivos `.jsonl`, como las cuentas de Copilot previstas para el curso.

### ¿Por qué existen `eventos.jsonl` y `eventos-prueba-sigma.jsonl`?

Porque tienen **objetivos diferentes**.

`eventos.jsonl` contiene la historia completa que debe investigar el alumno:

```text
Explorer
  ↓
Word abre factura_octubre.docm
  ↓
PowerShell
  ├── whoami
  ├── ipconfig
  ├── conexión TCP
  └── cmd
```

Sus campos son deliberadamente sencillos y orientados a lectura y análisis:

```text
process
parent
command_line
```

Por ejemplo:

```json
{
  "event_type": "process_create",
  "process": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
  "parent": "C:\\Program Files\\Microsoft Office\\root\\Office16\\WINWORD.EXE",
  "command_line": "powershell.exe -NoProfile -Command ..."
}
```

Este archivo sirve para **investigar el incidente**.

En cambio, `eventos-prueba-sigma.jsonl` no intenta representar toda la investigación. Contiene solamente tres casos controlados y utiliza los mismos nombres de campo que espera la regla Sigma:

```text
Image
ParentImage
CommandLine
```

Este archivo sirve para **probar la detección**.

Por tanto:

```text
eventos.jsonl / eventos.txt
        ↓
Investigación con el LLM


eventos-prueba-sigma.jsonl
        ↓
Prueba controlada de la regla Sigma
```

No hay duplicación funcional: uno es un conjunto de evidencias para investigar y el otro es un pequeño conjunto de pruebas de detección.

---

## 2. ¿Qué significa `Image` y `ParentImage`?

En telemetría de creación de procesos:

- `Image` identifica el ejecutable que se ha iniciado;
- `ParentImage` identifica el proceso que lo ha iniciado.

Por ejemplo:

```text
WINWORD.EXE
    ↓ inicia
powershell.exe
```

se representa de forma simplificada como:

```text
ParentImage = ...\\WINWORD.EXE
Image       = ...\\powershell.exe
```

Nuestra regla busca precisamente este tipo de relación.

---

## 3. Qué detecta la regla

La parte principal de la regla es:

```yaml
detection:
  selection_parent:
    ParentImage|endswith:
      - '\\WINWORD.EXE'
      - '\\EXCEL.EXE'
      - '\\POWERPNT.EXE'
  selection_child:
    Image|endswith:
      - '\\powershell.exe'
      - '\\pwsh.exe'
  condition: selection_parent and selection_child
```

La condición significa:

```text
El proceso padre es Word, Excel o PowerPoint

Y AL MISMO TIEMPO

el nuevo proceso es PowerShell
```

Por tanto, la regla intenta detectar:

```text
Office → PowerShell
```

No intenta detectar cualquier ejecución de PowerShell.

---

## 4. Abrir Enclave Rule Tester

Abre en Chrome, Edge o Firefox:

<https://tools.winterstetter.io/rule-tester>

Selecciona:

**Sigma**

Enclave permite pegar una regla Sigma y eventos de log en JSON o JSON Lines y mostrar qué selecciones y condiciones han coincidido.

El procesamiento se realiza en el navegador; no es necesario instalar software ni desplegar un SIEM.

---

## 5. Pegar la regla Sigma

Abre:

```text
regla-sigma-orientativa.yml
```

Copia todo su contenido y pégalo en el panel de reglas Sigma de Enclave.

No modifiques inicialmente la regla.

---

## 6. Pegar los eventos de prueba

Abre:

```text
../datos/eventos-prueba-sigma.jsonl
```

El archivo contiene tres eventos, uno por línea.

Copia todo el contenido y pégalo en el área de logs/eventos de Enclave.

Los tres casos son:

| Caso | ParentImage | Image | Resultado esperado |
|---|---|---|---|
| `positive_office_powershell` | WINWORD.EXE | powershell.exe | MATCH |
| `negative_explorer_powershell` | explorer.exe | powershell.exe | NO MATCH |
| `negative_word_cmd` | WINWORD.EXE | cmd.exe | NO MATCH |

---

## 7. Ejecutar la prueba

Ejecuta el análisis en Enclave.

El resultado esperado es **un único evento detectado**:

```text
positive_office_powershell
```

porque cumple simultáneamente:

```text
ParentImage termina en WINWORD.EXE

AND

Image termina en powershell.exe
```

Los otros dos eventos no deben disparar la regla.

---

## 8. Entender los casos negativos

### Caso positivo

```text
WINWORD.EXE
    ↓
powershell.exe
```

Resultado:

```text
MATCH
```

porque se cumplen las dos selecciones.

### Caso negativo 1

```text
explorer.exe
    ↓
powershell.exe
```

PowerShell se ejecuta, pero el padre no es una aplicación Office.

Resultado:

```text
NO MATCH
```

### Caso negativo 2

```text
WINWORD.EXE
    ↓
cmd.exe
```

El padre sí es Word, pero el proceso hijo no es PowerShell.

Resultado:

```text
NO MATCH
```

Esto permite comprobar que la detección depende de la **relación entre ambos procesos**, no solo de la aparición de una palabra o ejecutable aislado.

---

## 9. Prueba interactiva recomendada en clase

Después de probar los tres eventos juntos, puede hacerse una demostración sencilla modificando un evento manualmente.

Partimos del positivo:

```json
{
  "Image": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
  "ParentImage": "C:\\Program Files\\Microsoft Office\\root\\Office16\\WINWORD.EXE"
}
```

Debe producir:

```text
MATCH
```

Cambia únicamente:

```text
ParentImage = C:\\Windows\\explorer.exe
```

Debe dejar de coincidir.

Después restaura `WINWORD.EXE` y cambia:

```text
Image = C:\\Windows\\System32\\cmd.exe
```

Tampoco debe coincidir.

Esta prueba muestra visualmente cómo funciona una condición Sigma:

```text
selection_parent
       AND
selection_child
       ↓
     MATCH
```

---

## 10. ¿Por qué no probamos directamente `eventos.jsonl` o `eventos.txt`?

El archivo de investigación usa:

```text
process
parent
command_line
```

La regla Sigma usa:

```text
Image
ParentImage
CommandLine
```

Aunque describen conceptos equivalentes, **los nombres de los campos no son los mismos**.

En un entorno real existiría normalmente una capa de normalización o un pipeline que traduciría los campos del producto de seguridad al esquema utilizado por la detección.

Para no introducir esa complejidad en una práctica introductoria, `eventos-prueba-sigma.jsonl` contiene eventos ya normalizados con los campos que necesita la regla.

Esto permite aislar exactamente lo que queremos enseñar:

```text
¿La lógica de detección funciona?
```

sin mezclarlo todavía con:

```text
¿Está correctamente configurado el pipeline del SIEM?
```

---

## 11. ¿Y para qué se utiliza `eventos.txt`?

`eventos.txt` contiene exactamente los mismos eventos y el mismo formato interno que `eventos.jsonl`.

La única diferencia es la extensión del archivo.

Se incluye porque algunas interfaces de LLM utilizadas durante el curso permiten adjuntar archivos `.txt` pero bloquean archivos `.jsonl`.

Por tanto:

```text
eventos.jsonl
    → versión canónica de la telemetría


eventos.txt
    → copia compatible para adjuntarla al LLM
```

No deben analizarse ambos: contienen la misma información.

---

## 12. Qué hemos demostrado y qué no

Con esta prueba hemos demostrado que:

- la lógica de la regla reconoce el caso positivo;
- no dispara con dos casos negativos sencillos;
- las selecciones `ParentImage` e `Image` funcionan como esperamos;
- podemos relacionar una regla Sigma con telemetría concreta.

Todavía **no** hemos demostrado que la regla esté preparada para producción.

Una validación real requeriría también:

- telemetría del producto real;
- mapeo de campos;
- conversión al backend del SIEM/XDR;
- pruebas con un conjunto mucho mayor de positivos y negativos;
- análisis de falsos positivos;
- ajuste de la regla al entorno de la organización.

El flujo de producción sería aproximadamente:

```text
Telemetría Windows / EDR
        ↓
Normalización de campos
        ↓
Regla Sigma
        ↓
Conversión al backend
        ↓
SIEM / XDR
        ↓
Alertas
        ↓
Validación y tuning
```

---

## Resultado esperado de la práctica

El alumno debe poder explicar al terminar:

1. qué comportamiento intenta detectar la regla;
2. qué significan `Image` y `ParentImage`;
3. por qué el caso positivo dispara;
4. por qué los dos negativos no disparan;
5. por qué `eventos.jsonl`/`eventos.txt` y `eventos-prueba-sigma.jsonl` tienen propósitos diferentes;
6. por qué probar una regla con tres eventos no equivale a certificarla para producción.
