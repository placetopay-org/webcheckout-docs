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