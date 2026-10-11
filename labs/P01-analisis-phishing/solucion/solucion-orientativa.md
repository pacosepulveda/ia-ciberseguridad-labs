# Solución orientativa — P01

> Documento para revisión del instructor. No pretende ser la única respuesta válida.

## 1. Conclusión razonable

La clasificación más defendible con los datos disponibles es:

**Probable phishing / riesgo alto / confianza media-alta**

La confianza no debería considerarse absoluta porque faltan datos como cabeceras completas,
telemetría del gateway, reputación externa verificada o información DNS.

---

## 2. Evidencias relevantes

### Dominio del remitente no reconocido

El remitente utiliza:

`notificaciones@proveedores-ejemplo.net`

Ese dominio no aparece entre los dominios habituales proporcionados por el contexto.

Esto es un indicador de riesgo, pero por sí solo no demuestra fraude.

### URL con estructura engañosa

El enlace es:

`https://proveedores-ejemplo.net.validacion-segura.example/login`

Aunque visualmente comienza por `proveedores-ejemplo.net`, el dominio efectivo es
`validacion-segura.example`.

Esta discrepancia es una evidencia muy relevante porque el texto puede inducir a una lectura
incorrecta del destino real.

### Solicitud de credenciales

El correo pide iniciar sesión con una cuenta corporativa.

Esto incrementa el impacto potencial de una interacción con un sitio no verificado.

### Presión temporal

La frase:

`antes de las 12:00 de hoy`

introduce urgencia y reduce el tiempo percibido para validar la solicitud.

La urgencia es una señal frecuente en fraudes, pero tampoco es concluyente de forma aislada.

### Inconsistencia con el portal habitual

El portal legítimo proporcionado en el contexto es:

`https://proveedores.contoso-lab.example`

El enlace del mensaje no coincide.

---

## 3. Inferencias aceptables

Con las evidencias anteriores es razonable inferir que:

- el mensaje podría intentar dirigir al usuario a un portal no autorizado;
- existe riesgo de captura de credenciales;
- el dominio visible puede estar diseñado para parecer familiar.

No sería correcto afirmar sin más evidencia que:

- el sitio aloja malware;
- el dominio está registrado por un actor concreto;
- existe una campaña activa;
- las credenciales ya han sido comprometidas;
- el mensaje ha superado controles SPF, DKIM o DMARC.

---

## 4. Datos adicionales útiles

Antes de una conclusión operativa definitiva sería útil revisar:

- cabeceras completas del mensaje;
- resultados SPF, DKIM y DMARC;
- logs del gateway de correo;
- telemetría de navegación;
- resolución DNS del dominio;
- reputación externa de la URL y del dominio;
- comunicaciones internas sobre cambios del portal.

---

## 5. Acción recomendada

Una respuesta prudente sería:

1. no utilizar el enlace del correo;
2. acceder al portal habitual mediante un marcador o URL conocida;
3. verificar con el área responsable si existe una campaña legítima de actualización;
4. escalar el mensaje al equipo de seguridad para validación técnica.

Si existiese evidencia de que un usuario ya introdujo credenciales, el flujo de respuesta
debería ampliarse conforme al procedimiento de la organización.

---

## 6. Punto didáctico

El ejercicio está diseñado para mostrar que el modelo puede ayudar a:

- estructurar señales;
- resumir evidencias;
- identificar preguntas pendientes;
- proponer una evaluación provisional.

Pero también puede generar falsa seguridad si transforma una inferencia en un hecho.

La competencia principal no es obtener una respuesta del LLM, sino **evaluar críticamente
qué parte de esa respuesta está respaldada por evidencia**.
