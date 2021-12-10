---
tags: [Crear sesión]
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
    "login": "usuarioprueba",
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

> Nota: No se permiten pagos parciales cuando se envían impuestos, estos no se pueden dividir


## Pago Recurrente

Es un cobro periódico realizado por PlacetoPay para un mismo valor con un intervalo (diario, mensual, anual) según la indicación dada en la petición.

Para hacer uso de esta funcionalidad, en la estructura payment del Pago recurrente es necesario enviar en el objeto `recurring` los datos obligatorios para esta estructura.

```json
{
  "auth": {
    "login": "usuarioprueba",
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
        "recurring": { //Definimos las caracteristicas que tendrá la recurrencia.
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


Atributo | Tipo | Descripción | ¿Requerido?
---------|----------|--------- |---------
 **periodicity**  | `string` | Periodicidad de la factura [D=Día, M=Mes, Y=Año]| Requerido |
 **interval**   | `int` | Intervalo asociado a la periodicidad.| Requerido |
 **nextPayment**   | `date` |Fecha del próximo pago.| Requerido |
 **maxPeriods**   | `int` | Número máximo de periodo (-1 en caso de que no haya restricción.)| Requerido |
 **dueDate**   | `date` | Fecha para finalizar el pago.| Opcional |
 **notificationUrl**   | `string` |URL en el que el servicio notificará cada vez que se haga un pago recurrente.| Opcional |


Los cobros recurrentes sólo se realizarán en el caso que la transacción inicial sea aprobada.

En el caso de fallar un cobro recurrente, éste seguirá reintentado una vez cada día durante 3 días, si luego de esto no se obtiene una transacción aprobada, la recurrencia se le cancela al tarjetahabiente.
 
La recurrencia se deja de reintentar si la primera respuesta no tiene sentido reintentar (Tarjeta invalida, robada, etc), es decir se reintenta sólo si es por saldo.

Las recurrencias sólo pueden ser canceladas en la consola administrativa de PlacetoPay.

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
    "login": "usuarioprueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
    },
    "payment": {
        "reference": "3210",
        "description": "Pago con dispersion de prueba",
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
> Validaciones
- No se permiten pagos mixtos con valores de dispersión
- No se permiten pagos de preautorización con valores de dispersión
- La suma total de las dispersiones deben ser igual al total del pago
- Todas las monedas de las dispersiones deben ser igual a la moneda del pago

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





