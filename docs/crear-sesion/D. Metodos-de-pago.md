---
tags: [Crear sesión]
---

# Métodos de pago

Al momento de crear una sesión puedes limitar los medios de pagos, de esa forma obligas a tu usuario a pagarte esa sesión con métodos de pago en específicos. Puedes enviar el listado de métodos de pago en el atributo `paymentMethod` 

**Posibles valores:**

Valor | Descripción 
---------|----------
 `visa` | Tarjetas  VISA  
 `master` | Tarjetas  MASTERCARD
 `amex` | Tarjetas  AMERICAN EXPRESS
 `diners` | Tarjetas  DINERS
 `discover` | Tarjetas  DISCOVER
 `visa_electron` | Tarjetas debito VISA ELECTRON
 `ATHMV` | ATH Movil (Solo aplica para Puerto Rico)
  `EBATH` | ATH débito (Solo aplica para Puerto Rico)
 `pse` | PSE (Solo aplica para Colombia) | 
  

```json
    "payment": {
        "reference": "TEST_20210503_170757",
        "description": "Ipsam eum qui quae animi ut expedita amet.",
        "amount": {
            "currency": "COP",
            "total": 193000
        }
    },
    "expiration": "2021-05-04T17:07:57-05:00",
    "ipAddress": "181.53.226.56",
    "returnUrl": "https://dnetix.co/p2p/client",
    "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36",
    "paymentMethod": "visa, master, amex"// Se define los metodos de pago a usar.

```




