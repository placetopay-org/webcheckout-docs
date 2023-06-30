---
tags: [Crear sesión]
stoplight-id: u39gg1c6qvyjx
---

# Reversos

El proceso de reverso consiste en realizar un reembolso de una transacción aprobada por medio de la referencia interna.

## **Reverso Total**
Un reverso total permite el reembolso de una transacción por el monto total del pago.

**Ejemplo:**

API | URL
---------|----------
 `POST` | /api/reverse |

```json
{
  "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
  },
  "internalReference": 1, //código de referencia interna
}
```

## **Reverso Parcial**

Un reverso parcial permite el reembolso de una transacción estableciendo un monto a reembolsar.

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
  "action": "reverse",
  "payment": {
        "amount": {
            "currency": "COP"
            "total": 10000
        }
    }
}
```

<!-- theme: warning -->
> ### Importante
>
>- *Los procesos de reembolso no crean una sesión de pago, sino que se comunica con el core transaccional para efectuar el reembolso.*


