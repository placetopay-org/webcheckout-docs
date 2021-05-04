# Lightbox

Evita redireccionar a tu usuario usando la ventana Lightbox, que toma toda la pantalla con un fondo transparente para indicar y en el centro dentro de un recuadro que ajusta su tamaño dinámicamente se muestra la página de Webcheckout Placetopay.

Pasos para usar el lightbox:

1.	Usa la URL de tu país.

**Nota:** La URL del pais está formada por `URL_Base`/lightbox.min.js

**Ejemplo:**

- **Colombia, Puerto Rico, Costa Rica, Panamá:** https://secure.placetopay.com/redirection/lightbox.min.js

- **Ecuador:** https://secure.placetopay.ec/redirection/lightbox.min.js
	
2.	Carga la etiqueta JavaScript en tu página usando el origen de tu país en el atributo src
`<script src="REEMPLAZA_CON_URL_DE_TU_PAIS"></script>`
3.	Configura el callback de la respuesta para que realice la acción que requieras, en este caso solo mostramos la información en el campo inferior
```json
	P.on('response', function(data) {
	    $("#lightbox-response").html(JSON.stringify(data, null, 2));
	});
```
4.	Obtén el `processURL` PlacetoPay.
5.	Inicializa la URL en el lightbox, para este ejemplo se carga en la variable `processUrl`
```json
P.init(processUrl);
```
** Nota: ** Si deseas cambiar la transparencia del fondo del *iframe* puedes enviarla como parámetro al inicializar, de la siguiente manera, ésta debe ser un valor entre 0 y 1 donde 1 es nada transparente y 0 es completamente transparente
```json
P.init(processUrl, { opacity: 0.4 });
```
**AVISO IMPORTANTE ** 

Ten en cuenta que si el lightbox no encuentra un ambiente propicio para su funcionamiento (Poco soporte de JS, Versión anterior o antigua de navegador) ejecutará una redirección a la URL de procesamiento.

