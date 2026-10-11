# Solución orientativa — P01

Esta solución no pretende sustituir el razonamiento del alumno. Su objetivo es mostrar cómo justificar una clasificación separando hechos, inferencias y datos no disponibles.

## correo-01

**Clasificación orientativa:** Probable phishing  
**Confianza:** Alta

### Hechos observables

- El remitente visible utiliza `microsoft-alerts.example`, no un dominio corporativo de Microsoft.
- El `Reply-To` apunta a un dominio distinto: `account-check.example`.
- El asunto introduce urgencia y amenaza con suspender la cuenta.
- El cuerpo exige actuar en 60 minutos.
- Incluye una URL en `login-security.example`.

### Inferencias razonables

- El mensaje intenta aparentar una comunicación de Microsoft 365.
- La combinación de urgencia, dominios no relacionados y solicitud de validación es coherente con un intento de phishing.

### Datos no disponibles

- Cabeceras completas.
- SPF, DKIM y DMARC.
- Reputación histórica de los dominios.
- Telemetría de proxy, navegador o endpoint.

### Siguiente paso

No usar el enlace. Verificar el estado de la cuenta desde el portal habitual o mediante el canal oficial de soporte.

---

## correo-02

**Clasificación orientativa:** Probablemente legítimo  
**Confianza:** Media

### Hechos observables

- `From` y `Reply-To` coinciden.
- No incluye enlaces externos.
- No solicita credenciales ni datos personales.
- Indica expresamente que se utilice el portal corporativo habitual.
- Recomienda contactar con RR. HH. por canales internos.

### Inferencias razonables

- El contenido es coherente con una comunicación interna de formación.

### Datos no disponibles

- Cabeceras completas.
- Contexto sobre si existe realmente esa formación.
- Información sobre el sistema de correo corporativo.

### Siguiente paso

Si existe duda, verificar la convocatoria desde el portal interno o con RR. HH.

---

## correo-03

**Clasificación orientativa:** Sospechoso — requiere verificación  
**Confianza:** Alta

### Hechos observables

- El mensaje afirma proceder de un proveedor habitual.
- El `Reply-To` cambia de `proveedor.example` a `proveedor-payments.example`.
- Solicita un cambio en la cuenta bancaria de pago.
- Introduce urgencia para procesarlo el mismo día.

### Inferencias razonables

- El patrón es compatible con fraude BEC o manipulación de pagos.
- Con el artefacto disponible no puede demostrarse que la cuenta del proveedor haya sido comprometida ni que el mensaje sea fraudulento.

### Datos no disponibles

- Histórico de comunicaciones con el proveedor.
- Procedimiento autorizado para cambios bancarios.
- Confirmación del proveedor por otro canal.
- Cabeceras completas y autenticación del mensaje.

### Siguiente paso

No modificar datos bancarios basándose únicamente en el correo. Confirmar el cambio mediante un canal previamente conocido e independiente del mensaje recibido.

---

## correo-04

**Clasificación orientativa:** Sospechoso — requiere verificación  
**Confianza:** Baja

### Hechos observables

- Informa de un documento compartido.
- `From` y `Reply-To` coinciden.
- No contiene una URL concreta en el artefacto.
- Recomienda confirmar con la persona remitente si el documento no era esperado.

### Inferencias razonables

- Puede ser una notificación legítima de un servicio de archivos.
- También podría ser un señuelo, pero faltan elementos suficientes para afirmarlo.

### Datos no disponibles

- URL real de acceso.
- Cabeceras completas.
- Confirmación de que Marta G. existe y compartió el documento.
- Contexto del usuario receptor.

### Siguiente paso

Verificar la compartición desde el portal corporativo conocido o confirmar con la persona remitente por un canal independiente.

---

## Qué debería detectar el alumno sobre el LLM

Una buena respuesta del modelo debe:

- separar hechos de inferencias;
- evitar afirmar que un dominio es malicioso sin evidencia externa;
- no inventar SPF, DKIM, DMARC, WHOIS, reputación o resultados de sandbox;
- reconocer cuándo no existe información suficiente para una conclusión definitiva;
- recomendar verificaciones proporcionales al riesgo.

## Criterio de corrección

La nota no depende de que el alumno utilice exactamente las mismas etiquetas, sino de que pueda justificar su decisión con evidencias observables y reconozca correctamente qué información falta.
