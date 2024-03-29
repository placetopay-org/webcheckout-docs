---
tags: [Crear sesión]
internal: true
---

## Pago

Un pago hace referencia al proceso que se ejecuta luego de que el usuario ingresa la información solicitada
en WebCheckout Placetopay y éste solicita a la red realizar el cobro.

## Pago mixto

El pago mixto permite utilizar varios medios de pago (habilitados para la clave API) al momento de pagar para una misma sesión.

Para hacer uso de esta funcionalidad, en la estructura payment del Pago es necesario enviar el atributo `allowPartial` como: `TRUE`.

Ejemplo:

```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
  },

   "payment": {
        "reference": "3210",
        "description": "Pago mixto de prueba",
        "amount": {
            "currency": "COP",
            "total": "10000"
        },
        "allowPartial": true //Definimos que la operación permitirá pagos mixtos
    },

    "expiration": "2021-04-30T00:00:00-05:00",
    "returnUrl": "https://mysite.com/response/3210",
    "ipAddress": "127.0.0.1",
    "userAgent": "PlacetoPay Sandbox"
}
```

Estados adicionales de una sesión de pago mixto

Al obtener el resultado de la operación, debe tener muy presente los siguiente dos estados:

- **APPROVED_PARTIAL:** Indica que se realiza al menos un pago aprobado pero no se realizado el pago total de la sesión.
- **PARTIAL_EXPIRED:** Indica que se realiza al menos un pago aprobado pero no se completó el pago total de la sesión y ésta expiró.

Es importante identificar según la regla de negocio del sitio al obtener alguno de estos dos estados.

<!-- theme: danger -->

> ### Importante
>
> _No se permiten pagos parciales cuando se envían impuestos, estos no se pueden dividir._

## Pago Recurrente

Es un cobro periódico realizado por PlacetoPay para un mismo valor con un intervalo (diario, mensual, anual) según la indicación dada en la petición.

Para hacer uso de esta funcionalidad, en la estructura payment del Pago recurrente es necesario enviar en el objeto `recurring` los datos obligatorios para esta estructura.

```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
    },
    "payment": {
        "reference": "3210",
        "description": "Pago recurrente de prueba",
        "amount": {
            "currency": "COP",
            "total": "10000"
        },
        "recurring": { //Definimos las características que tendrá la recurrencia.
            "periodicity": "M",
            "interval": "1",
            "nextPayment": "2019-04-04",
            "maxPeriods": "12"
        }
    },
    "expiration": "2019-03-05T00:00:00-05:00",
    "returnUrl": "https://mysite.com/response/3210",
    "ipAddress": "127.0.0.1",
    "userAgent": "PlacetoPay Sandbox"
}
```

| Atributo            | Tipo     | Descripción                                                                   | ¿Requerido? |
| ------------------- | -------- | ----------------------------------------------------------------------------- | ----------- |
| **periodicity**     | `string` | Periodicidad de la factura [D=Día, M=Mes, Y=Año]                              | Requerido   |
| **interval**        | `int`    | Intervalo asociado a la periodicidad.                                         | Requerido   |
| **nextPayment**     | `date`   | Fecha del próximo pago.                                                       | Opcional    |
| **maxPeriods**      | `int`    | Número máximo de periodo (-1 en caso de que no haya restricción.)             | Requerido   |
| **dueDate**         | `date`   | Fecha para finalizar el pago.                                                 | Opcional    |
| **notificationUrl** | `string` | URL en el que el servicio notificará cada vez que se haga un pago recurrente. | Opcional    |

<!-- theme: warning -->

> ### Importante
>
> - _El atributo `nextPayment` no es obligatorio, en caso de que no se envié, se calcula dependiendo del atributo `interval` y `periodicity`, en caso de que se declare debe ser una fecha futura a la fecha actual._
> - _En el caso de fallar un cobro recurrente, éste seguirá reintentado una vez cada día durante 3 días, si luego de esto no se obtiene una transacción aprobada, la recurrencia se le cancela al tarjetahabiente._
> - _La recurrencia se deja de reintentar si la primera respuesta no tiene sentido reintentar (Tarjeta invalida, robada, etc), es decir se reintenta sólo si es por saldo._
> - _Las recurrencias sólo pueden ser canceladas en la consola administrativa de PlacetoPay._

## Pago con dispersión

El pago con dispersión permite dividir el pago principal a diferentes convenios registrados en una misma sesión, además permite que cada parte de la transacción sea procesada por diferentes proveedores.
**[Más información](https://docs-gateway.placetopay.com/docs/api-services-docs/ZG9jOjExNjAxOTc1)**

Para hacer uso de esta funcionalidad es importante tener el `ID` del convenio a donde va dirigido el pago, por defecto si no se agrega ningún valor este tomará por defecto el medio de pago configurado en el sitio de la sesión,
también es necesario indicar el tipo de convenio, en este caso `MERCHANT` o `AIRLINE`. **[Más información sobre códigos de aerolíneas](https://docs-gateway.placetopay.com/docs/api-services-docs/ZG9jOjIxNzUzMzYw-codigos-de-aerolineas)**

En la estructura payment del pago es necesario enviar el esquema de dispersión

Ejemplo:

```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
    },
    "payment": {
        "reference": "3210",
        "description": "Pago con dispersión de prueba",
        "amount": {
            "currency": "COP",
            "total": 100000
        },
        "dispersion": [ //Estructura de dispersión
            {
                "agreement": 1, //ID del convenio
                "agreementType": "AIRLINE", //Tipo de convenio
                "amount": {
                    "currency": "COP",
                    "total": 50000
                }
            },
            {
                "agreement": "",
                "agreementType": "MERCHANT",
                "amount": {
                    "currency": "COP",
                    "total": 50000
                }
            }
        ]
    },
    "expiration": "2021-12-31T00:00:00-05:00",
    "returnUrl": "https://mysite.com/response/3210",
    "ipAddress": "127.0.0.1",
    "userAgent": "PlacetoPay Sandbox"
}
```

<!-- theme: warning -->

> ### Importante
>
> - _No se permiten pagos mixtos con valores de dispersión_
> - _No se permiten pagos de preautorización con valores de dispersión._
> - _La suma total de las dispersiones deben ser igual al total del pago._
> - _Todas las monedas de las dispersiones deben ser igual a la moneda del pago._

Para el envió de impuestos, es importante que se encuentre en la estructura de cada una de las dispersiones

Ejemplo:

```json
{
    "dispersion": [ //Estructura de dispersión
        {
            "agreement": 1, //ID del convenio
            "agreementType": "AIRLINE", //Tipo de convenio
            "amount": {
                "currency": "COP",
                "total": 50000
            },
            "taxes": [
                {
                    "kind": "airportTax",
                    "amount": 16.13
                }
            ],
            "details": [
                {
                    "kind": "tip",
                    "amount": 11
                }
            ]
        },
        {
            "agreement": "",
            "agreementType": "MERCHANT",
            "amount": {
                "currency": "COP",
                "total": 50000
            },
            "taxes": [
                {
                    "kind": "municipalTax",
                    "amount": 16.13
                }
            ],
            "details": [
                {
                    "kind": "tip",
                    "amount": 11
                }
            ]
        }
    ]
}
```

## Pago con subscripción

Un pago se puede convertir en pago y subscripción al mismo tiempo, para realizar este flujo es importante agregar en el objeto `payment` el atributo  `subscribe` en `true` de la siguiente manera

```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
    },
    "payment": {
        "reference": "3210",
        "description": "Pago con subscripcion de prueba",
        "amount": {
            "currency": "COP",
            "total": 100000
        },
        "subscribe" : true //Definimos subscribe en true
    },
    "expiration": "2021-12-31T00:00:00-05:00",
    "returnUrl": "https://mysite.com/response/3210",
    "ipAddress": "127.0.0.1",
    "userAgent": "PlacetoPay Sandbox"
}
```

<!-- theme: warning -->

> ### Importante
>
> - _El atributo `subscribe` es un valor de tipo `bool` por defecto en `false`. Se declara `true` cuando se quiere guardar la información para realizar subscripciones_
> - _Solamente permite guardar información de subscripciones cuando se realiza con el flujo de `Wallet` de caso contrario solamente efectuará el pago y no guardará la subscripción_
