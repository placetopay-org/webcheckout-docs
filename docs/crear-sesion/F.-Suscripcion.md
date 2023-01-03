---
tags: [Crear sesión]
---

# Suscripción

La suscripción permite almacenar de forma segura (tokenizando) el medio de pago de un usuario, para que luego pueda efectuar cobros relacionados a éste.

### **Solicitar suscripción:**

Para hacer uso de esta funcionalidad es necesario enviar en el `RedirectRequest` la estructura `subscription`.

**Ejemplo:**
```json
{
   "auth": {
    "login": "usuarioPrueba",
    "tranKey": "jsHJzM3+XG754wXh+aBvi70D9/4=",
    "nonce": "TTJSa05UVmtNR000TlRrM1pqQTRNV1EREprWkRVMU9EZz0=",
    "seed": "2019-04-25T18:17:23-04:00"
    },
    "subscription": { //En este punto definimos que el tipo de operación es una suscripción
        "reference": "3110",
        "description": "Una suscripción de prueba"
    },
    "expiration": "2021-04-30T00:00:00-05:00",
    "returnUrl": "https://mysite.com/response/3210",
    "ipAddress": "127.0.0.1",
    "userAgent": "PlacetoPay Sandbox"
}
```


### **Cobrar usando un token**
La estructura de la respuesta contiene toda la información de la petición original y una estructura de suscripción (`subscription`) con un instrumento (`instrument`) representado en forma de token.

 <!-- theme: warning -->
> ### Importante
>
>- *Se recomienda realizar un cobro por un valor mínimo para identificar que la tarjeta se encuentra activa.*
>- *La información del token debe ser almacenada en su sitio y relacionada al usuario y/o producto. Luego de tener el token, puede generar cobros al medio de pago tokenizado usando el servicio collect.*
