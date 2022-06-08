---
stoplight-id: 0c1448ed0e011
---

# Crear sesión

Este endpoint sirve para solicitar la creación de una sesión de pagos.
Retorna el identificador y la URL de procesamiento.
Puedes ver la descripción detallada de cada uno de los elementos de petición y respuesta en
[CreateRequest](../reference/WebCheckout-ES.yaml/paths/~1api~1session/post)

## Localización

Al momento de enviar la petición se puede especificar el `locale` (idioma) que usará la sesión que se creará.

El `locale`, por ejemplo `es_CO`, se compone por el código del lenguaje según el estándar [ISO 631-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes), seguido de un guión bajo `_` y 2 letras que corresponden al país según el estándar [ISO 3166-1 alpha-2](https://es.wikipedia.org/wiki/ISO_3166-1#C%C3%B3digos_ISO_3166-1).

Ejemplos:

|  País               | Idioma      | Locale  |
|:--------------------|:-------------|:--------|
| Colombia (CO)       | Español (es) | `es_CO` |
| Ecuador  (EC)       | Español (es) | `es_EC` |
| Estados Unidos (US) | Inglés  (en) | `en_US` |

El parámetro `locale` es **opcional**, en caso de que no se envíe o no cumpla con los estándares previamente descritos, se tomará por defecto el locale y país del sitio que está creando la sesión.