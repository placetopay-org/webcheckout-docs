---
stoplight-id: 14206cdfa4c0f
---

# Webcheckout PlacetoPay

WebCheckout es una página web prediseñada, optimizada y alojada en Placetopay que le permite aceptar pagos en línea de forma rápida y segura desde dispositivos móviles y de escritorio. Puedes aceptar pagos únicos, pagos recurrentes, pagos mixtos y suscribir medios de pago.

Webcheckout te permite:

* **Diseño personalizado:** Puedes personalizar los nombres, logos y colores de tu empresa.
* **Diferentes idiomas y monedas:** Aceptar pagos en multiples idiomas y monedas.
* **Adaptado a diferentes resoluciones:** Diseño receptivo para diferentes dispositivos.
* **Wallet PlacetoPay:** WebCheckout cuenta con su propia billetera que le permite a usuarios guardar medios de pago frecuentes brindando mayor seguridad y facilidad en el proceso de pago.
* **Seguridad de la información:** Lineamientos PCI que garantizan seguridad en la captura y procesamiento de la información sensible de tarjetas.
* **Pagos avanzados:** Pagos con Impuestos, pagos mixtos, suscripciones, cobros recurrentes, promociones y más...

# Flujo de integración

**1.** Para aceptar un pago por WebCheckout es necesario tener una *Sesión* de pago que se puede crear usando el método [API - Crear sesión (CreateRequest)](../reference/WebCheckout-ES.yaml/paths/~1api~1session/post), en la respuesta de este servicio se obtendrá el `processURL` y el `requestId`.

Ver más en: [Crear Sesión](create-session.md)

**2.** En su sistema, crear un registro que relacione el pago en proceso con el `requestID` entregado, el proceso se encuentra en estado **pendiente**.

**3.** El usuario debe ser redireccionado al `processUrl` entregado.

**4.** En la interfaz de WebCheckout el usuario realizará el proceso de pago o suscripción, WebCheckout se encargará de recaudar todos los datos requeridos.

**6.** Una vez completado el proceso, el usuario puede ser redireccionado de vuelta a la *URL* de retorno indicada como `returnUrl` (Atributo enviado en `CreateRequest`).

**7.** Al llegar al sitio del comercio, se debe consultar el estado de la *Sesión*. 

Consumir él método [API - Consultar sesión (getRequestInformation)](../reference/WebCheckout-ES.yaml/paths/~1api~1session~1{requestId}/post)

**8.** Segun sea el estado final del pago, se debe ejecutar las regla de negocio y actualizar la información correspondiente al pago.

**9.** De manera asincrónica, PlacetoPay realiza una notificación, del estado final de una sesión, a tu sitio.

**10.** Recomendamos implementar un proceso sonda para resolver aquellas transacciones que no se resolvieron en los numerales 7 y 9.

