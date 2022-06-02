# Crear sesión

Este endpoint sirve para solicitar la creación de una sesión de pagos.
Retorna el identificador y la URL de procesamiento.
Puedes ver la descripción detallada de cada uno de los elementos de petición y respuesta en
[CreateRequest](/docs/webcheckout-docs/5e87083a4109d-crear-sesion-create-request)

## Localización
Al momento de enviar la petición se puede especificar el `locale` con el cuál se manejará el idioma de la
sesión que se creará. Se compone por el código del lenguaje según el estándar ISO 631-1 + guión bajo ( _ ) + 2 letras
del país según el estándar ISO 3166-1 alpha-2.

Ejemplos:

| País                | Idioma       | Locale  |
|---------------------|--------------|---------|
| Colombia (CO)       | Español (es) | `es_CO` |
| Ecuador  (EC)       | Español (es) | `es_EC` |
| Estados Unidos (US) | Inglés  (en) | `en_US` |

El parámetro `locale` es opcional, en caso de que no se envíe o cumpla con los estándares previamente descritos,
se tomará por defecto el locale y país del sitio asociado a las credenciales enviadas en la
[Autenticación](/docs/webcheckout-docs/9d6ee5d256b71-autenticacion)