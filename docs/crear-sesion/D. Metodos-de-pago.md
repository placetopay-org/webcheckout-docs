---
tags: [Crear sesión]
---

# Métodos de pago

Al momento de crear una sesión puedes limitar los medios de pagos, de esa forma obligas a tu usuario a pagarte esa sesión con métodos de pago en específicos. Puedes enviar el listado de métodos de pago en el atributo `paymentMethod`

**Posibles valores:**

Valor | Descripción
---------|----------
visa | Tarjetas  VISA
master | Tarjetas  MASTERCARD
amex | Tarjetas  AMERICAN EXPRESS
diners | Tarjetas  DINERS
discover | Tarjetas  DISCOVER
visa_electron | Tarjetas débito VISA ELECTRON
_ATH_ | Corresponsales bancarios Grupo Aval
_PPD_ | Débito pre-autorizado (PPD)
_PSE_ | Débito a cuentas corrientes y ahorros (PSE
AC_WU | Western Union
ATHMV | ATH Móvil
AV_AV | Banco AV Villas Recaudos
AV_BB | Banco de Bogota Recaudos
AV_BO | Banco de Occidente Recaudos
BBVAC | BBVA Colombia Oficinas y corresponsales
BTNBC | Bancolombia
CAFAM | Cafam
CDNSA | Codensa
CMFDI | Comfandi
DBTAC | Registro cuentas débito
DVVND | Davivienda Oficinas y corresponsales
EBATH | Tarjeta ATH
EFCTY | Efecty
GNOFC | Gana Recaudo en Oficina
GNPIN | GanaPIN
PYPAL | PayPal
SFPAY | Safety Pay
SOMOS | Somos Grupo EPM
SPGRS | Supergiros
T1_BC | Bancolombia Recaudos
TYDAK | Tarjeta Alkosto
TYDEX | Tarjeta Éxito

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
