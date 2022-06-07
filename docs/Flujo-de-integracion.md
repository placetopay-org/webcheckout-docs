# Flujo de integración

1. Para redireccionar tu usuario al sistema de Webcheckout, debes consumir el método **`createRequest`**.
   **Si no deseas redireccionarlo puedes usar la opción de lightbox.**
   Si la solicitud es procesada correctamente, el servicio crea una sesión y retorna en la respuesta: Identificador `requestID` y URL de procesamiento `processUrl`.
2. Crea un registro en tu sistema, relaciona ese registro al `requestID` y déjalo en estado pendiente.
3. Redirecciona al usuario al `processUrl`.
4. En la interfaz de Web Checkout el usuario realizará el proceso de pago o suscripción donde debe ingresar la información para procesar el pago.
5. Posteriormente el usuario debe seleccionar el medio de pago con el que va a realizar la compra ingresando los datos del medio de pago.
6. Una vez el usuario realiza el proceso y hace clic en *“Regresar al comercio”*, éste es enviado a la URL de retorno returnUrl (Atributo especificado al crear la operación).
7. Al llegar a tu sitio, con el `requestID` del registro debes consultar a PlacetoPay el estado de la sesión usando el método **`getRequestInformation`**.
8. Ejecuta tu regla de negocio según el estado obtenido para actualizar el estado de la misma en tu base de datos.
9. De manera asincrónica, PlacetoPay realiza una notificación, del estado final de una sesión, a tu sitio.
10. Recomendamos implementar un proceso sonda para resolver aquellas transacciones que no se resolvieron en los numerales 7 y 9.

