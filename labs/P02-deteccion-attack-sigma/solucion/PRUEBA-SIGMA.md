# Cómo probar la regla Sigma de P02

La validación de una regla Sigma tiene dos niveles distintos:

1. **Validar que la regla está bien formada y puede convertirse**.
2. **Comprobar que realmente detecta los eventos esperados y no dispara con eventos negativos**.

---

## 1. Validación rápida en navegador

La forma más sencilla para clase es utilizar el conversor oficial de SigmaHQ en:

`https://sigmahq.io/docs/digging-deeper/convert.html`

Pega el contenido de:

`regla-sigma-orientativa.yml`

Si la regla puede procesarse y convertirse a un backend, hemos comprobado que su estructura y sintaxis son utilizables por pySigma.

También puede utilizarse:

`https://sigconverter.io/`

para convertirla a lenguajes como Splunk SPL, Kusto/KQL, Elasticsearch/OpenSearch, etc.

> Convertir una regla correctamente **no demuestra todavía que detecte los eventos correctos**.

---

## 2. Prueba funcional con eventos positivos y negativos

En `../datos/eventos-prueba-sigma.jsonl` se incluyen tres eventos sintéticos:

| Caso | ParentImage | Image | Resultado esperado |
|---|---|---|---|
| `positive_office_powershell` | WINWORD.EXE | powershell.exe | MATCH |
| `negative_explorer_powershell` | explorer.exe | powershell.exe | NO MATCH |
| `negative_word_cmd` | WINWORD.EXE | cmd.exe | NO MATCH |

La lógica de la regla exige simultáneamente:

```text
ParentImage termina en WINWORD.EXE / EXCEL.EXE / POWERPNT.EXE

Y

Image termina en powershell.exe / pwsh.exe
```

Por tanto, solo el primer evento debe coincidir.

---

## 3. Prueba real en un SIEM

El flujo correcto en producción sería:

```text
Regla Sigma
    ↓
Conversión al backend
    ↓
Pipeline/mapeo de campos
    ↓
Consulta SIEM
    ↓
Eventos conocidos positivos y negativos
    ↓
Validación de resultados
```

Ejemplos:

- Sigma → Splunk SPL → eventos Sysmon/Windows;
- Sigma → Sentinel KQL → tabla de procesos normalizada;
- Sigma → Elasticsearch/OpenSearch → campos ECS/Winlogbeat.

El mapeo de campos es crítico. Una regla puede convertir correctamente y no detectar nada si los campos reales no coinciden con `Image` y `ParentImage`.

---

## 4. Importante sobre los datos de esta práctica

El archivo principal `../datos/eventos.jsonl` utiliza nombres didácticos simplificados como:

```text
process
parent
command_line
```

La regla Sigma orientativa utiliza la taxonomía habitual de process creation:

```text
Image
ParentImage
CommandLine
```

Por ello, `eventos.jsonl` **no debe usarse directamente para probar la regla sin un mapeo previo**.

El archivo `eventos-prueba-sigma.jsonl` ya está normalizado para mostrar claramente qué casos deberían disparar la detección.

---

## 5. Qué valida cada prueba

| Prueba | Qué demuestra |
|---|---|
| Parseo/conversión | La regla está bien formada |
| Evento positivo | La lógica detecta el patrón buscado |
| Eventos negativos | La regla no es trivialmente demasiado amplia |
| SIEM real | La regla funciona con el esquema y telemetría del entorno |
| Revisión de falsos positivos | La detección es operativamente utilizable |

El objetivo no es únicamente que la regla “compile”, sino demostrar que existe una relación verificable entre **telemetría → lógica de detección → alerta**.
