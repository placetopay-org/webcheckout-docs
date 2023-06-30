---
tags: [Crear sesión]
---

# Preautorización

Este flujo de trabajo es usado con el fin de reservar **(CHECKIN)** un monto de dinero en el tarjetahabiente para posteriormente hacer el débito del mismo, en este caso **(CHECKOUT)**.
Este monto en el transcurso del tiempo puede cambiar **(REAUTHORIZATION)** según las necesidades del comercio o cambios en los servicios elegidos por el tarjetahabiente.
Por último, el reverso **(REVERSE)** es un tipo de transacción, el cual permite reversar un pago aprobado o debitado con el código de referencia interna.

## **CHECKIN**
La  transacción tipo **CHECKIN** es  utilizada  para  obtener  una  autorización por  parte  del  banco. Realiza un débito a una tarjeta de crédito/débito el cual se utiliza como depósito de garantía por la utilización de un bien o servicio.

**Ejemplo:**

```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
  },
   "type": "checkin", //Definimos como tipo reserva
   "payment": {
        "reference": "3210",
        "description": "Pago de reserva prueba",
        "amount": {
            "currency": "USD",
            "total": "100"
        },
        "allowPartial": false
    },

    "expiration": "2021-04-30T00:00:00-05:00",
    "returnUrl": "https://mysite.com/response/3210",
    "ipAddress": "127.0.0.1",
    "userAgent": "PlacetoPay Sandbox"
}
```

<!-- theme: warning -->
> ### Importante
>
>- *No se permiten pagos de preautorización cuando se quiere hacer un pago mixto.*
>- *No se permiten pagos de preautorización con valores de dispersión.*

## **REAUTHORIZATION**
La transacción tipo **REAUTHORIZATION** es utilizada para modificar el monto definido como depósito de garantía separado previamente, con una transacción tipo CHECKIN. Esto realiza una nueva autorización  por parte del banco.

**Ejemplo:**

API | URL
---------|----------
 `POST` | /api/transaction |

 ```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
  },
  "internalReference": 1, //código de referencia interna
  "amount": {
    "currency": "USD",
    "total": 100
  },
  "action": "reauthorization"
}
```

## **CHECKOUT**
La transacción tipo **CHECKOUT** es utilizada para confirmar el monto del depósito de garantía separado previamente, con una transacción tipo **CHECKIN/REAUTHORIZATION**. Esto formaliza la transacción de compra con el banco.

**Ejemplo:**

API | URL
---------|----------
 `POST` | /api/transaction |

 ```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
  },
  "internalReference": 1, //código de referencia interna
  "amount": {
    "currency": "USD",
    "total": 100
  },
  "action": "checkout"
}
```
## **REVERSE**
La transacción tipo **REVERSE** es utilizada para reversar un pago de tipo CHECKOUT o un pago debitado común y corriente.

**Ejemplo:**

API | URL
---------|----------
 `POST` | /api/transaction |

```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
  },
  "internalReference": 1, //código de referencia interna
  "action": "reverse"
}

```
