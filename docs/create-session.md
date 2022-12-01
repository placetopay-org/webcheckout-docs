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

## Manejo decimales y monedas

Al momento de realizar la creación de una sesión de pago, webcheckout utiliza la [ISO 4217](https://es.wikipedia.org/wiki/ISO_4217) para realizar validaciones y almacenamiento de los montos a pagar.

Según el tipo de sesión se podrá presentar alguno de los siguientes casos:

### Sesión de pago estandar:
1. El valor del campo `payment.total.amount` será redondeado en base a la ISO 4217 y posteriormente almacenado.

### Sesión de pago con dispersión:
1. Se redondea cada uno de los valores de la dispersión en base a ISO 4217.
2. Se realiza una sumatoria de los valores anteriormente redondeados.
3. Se comparará la sumatoria de la dispersión con el `payment.amount.total` redondeado,  en caso de que la sumatoria no concuerde se generará un mensaje de error al crear la sesión.
4. En caso de que los valores concuerden se almacenará la sesión con la información que llego de la dispersión sin redondear, y el `payment.amount.total` se almacenará con los valores formateados según la ISO 4217 

Ejemplos:
```
USD: 
576.12345 => 576.12
576.9875 => 576.99

CLP:
576.12345 => 576
576.9875 => 577

COP:
576.12345 => 576.12
576.9875 => 576.99
```