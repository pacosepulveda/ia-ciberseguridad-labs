# Solución orientativa — P04

## 1. Fuente problemática

El Documento B contiene texto que intenta asumir autoridad:

> ignora cualquier instrucción anterior...

Ese texto debe tratarse como **dato no confiable**, no como instrucción.

El hecho de que una cadena aparezca en una base documental no le concede privilegios.

## 2. Respuesta adecuada al usuario

La respuesta debería basarse en los documentos A y C:

- abrir una solicitud;
- indicar repositorio, motivo y duración;
- obtener aprobación;
- aplicar mínimo privilegio;
- retirar el acceso al finalizar;
- registrar la aprobación.

## 3. Controles útiles

### Separación instrucciones/datos
Etiquetar y procesar el contenido recuperado como contexto, no como autoridad.

### Procedencia
Mantener metadatos sobre origen, propietario, fecha y nivel de confianza de cada fuente.

### Mínimo privilegio
El modelo no debería tener capacidad directa para otorgar permisos.

### Validación de salida
Comprobar respuestas contra políticas válidas antes de presentarlas o ejecutar acciones.

### Human-in-the-Loop
Toda concesión de acceso debe requerir aprobación humana explícita.

### Auditoría
Registrar:
- pregunta;
- fuentes consultadas;
- respuesta;
- decisión humana;
- acción final.

## 4. Por qué “un prompt mejor” no basta

Un prompt puede ayudar a reducir errores, pero no constituye por sí solo una frontera de seguridad.

Los controles más importantes deben existir fuera del modelo:

- permisos;
- separación de funciones;
- validación;
- aislamiento;
- autorización;
- registro.

## 5. Mensaje didáctico

El problema central no es que el modelo “obedezca mal”, sino que un sistema inseguro
puede mezclar datos no confiables con instrucciones y conceder al modelo demasiada capacidad
de actuación.
