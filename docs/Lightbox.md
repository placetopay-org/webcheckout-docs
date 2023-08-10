---
internal: true
---

# Lightbox SDK

Con el Lightbox SDK, puedes ofrecer una experiencia de usuario mejorada al evitar redireccionamientos. La ventana Lightbox se despliega sobre la página actual, ocupando toda la pantalla con un fondo transparente. En el centro de esta ventana, se muestra de manera dinámica la página de Webcheckout Placetopay, ajustando su tamaño automáticamente en un recuadro. Esta solución te permite mantener a tus usuarios en tu sitio web o aplicación, brindándoles comodidad y facilitando el proceso de pago.

## Integración del Lightbox SDK

### Pasos esenciales

1. Para importar el SDK Lightbox en tu página, puedes utilizar la etiqueta `<script>` de HTML de la siguiente manera:

   ```html
   <script src="<URL_BASE>/lightbox.min.js"></script>
   ```

   **Nota:** La `<URL_BASE>` depende del país donde se encuentre tu cuenta PlacetoPay, obtén la URL base de tu país en la siguiente tabla:

   | País | URL Base                           |
   | :--: | :--------------------------------- |
   |  CO  | <https://checkout.placetopay.com>  |
   |  CL  | <https://checkout.getnet.cl>       |
   |  EC  | <https://checkout.placetopay.ec>   |
   |  CR  | <https://checkout.davivienda.cr>   |
   |  HN  | <https://pagoenlinea.bancatlan.hn> |

2. Crea la sesión de checkout y obtén el `processURL` de la respuesta PlacetoPay. **Ejemplo**:
   ```json
   {
   	"status": {
   		"status": "OK",
   		"reason": "PC",
   		"message": "La petición se ha procesado correctamente",
   		"date": "2023-01-01T00:00:00-05:00"
   	},
   	"requestId": 123456,
   	"processUrl": "https://secure.placetopay.com/redirection/session/123456/1234567890abc1234567890abc12345"
   }
   ```

3. Inicializa la URL en el Lightbox SDK utilizando la variable processUrl obtenida al crear la sesión de checkout. **Ejemplo:**

   ```javascript
   // Obtén la variable processUrl de la respuesta de PlacetoPay
   var processUrl = "https://secure.placetopay.com/redirection/session/123456/1234567890abc1234567890abc12345";

   // Inicializa la URL en el Lightbox SDK
   P.init(processUrl);
   ```

   **Nota:** Si deseas ajustar la transparencia del fondo del iframe, puedes enviarla como parámetro al inicializarlo. El valor de transparencia debe ser un número entre 0 y 1, donde 1 indica que el fondo no es transparente y 0 indica que es completamente transparente. **Ejemplo:**

   ```javascript
   P.init(processUrl, { opacity: 0.4 });
   ```

   En este ejemplo, se establece un nivel de transparencia del 40% al inicializar el iframe mediante el método P.init(). Recuerda que puedes ajustar el valor de opacity según tus necesidades, utilizando un valor entre 0 y 1.

> **AVISO IMPORTANTE**
> Ten en cuenta que si el lightbox no encuentra un ambiente propicio para su funcionamiento (Poco soporte de JS, Versión anterior o antigua de navegador) ejecutará una redirección a la URL de procesamiento.

### Profundizando en la integración

#### Métodos

El Lightbox SDK permite ejecutar los siguientes métodos:

- `init` : Inicializa el Lightbox SDK. **Ejemplo:**

  ```javascript
  P.init(processUrl, options);
  ```

  Puede recibir un segundo parámetro de tipo objeto con las siguientes opciones:

  | Opción    | Tipo     | Descripción                                                                                                                                                                            | Valor por defecto |
  | --------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
  | `opacity` | `number` | Establece la transparencia del fondo del iframe. El valor debe ser un número entre 0 y 1, donde 1 indica que el fondo no es transparente y 0 indica que es completamente transparente. | `0.7`             |

- `on` : Suscribe un evento al Lightbox SDK. **Ejemplo:**

  ```javascript
  P.on('close', function () {
  	// Tu código...
  });
  ```

#### Eventos

El Lightbox SDK permite suscribirse a los siguientes eventos:

- `response` : Se ejecuta cuando se recibe una respuesta de PlacetoPay. **Ejemplo:**

  ```javascript
  P.on('response', function (response) {
  	console.log(response);
  });
  ```

- `close` : Se ejecuta cuando el usuario cierra el Lightbox o cuando se cierra automáticamente al finalizar el proceso y este haber sido creado con un `skipResult: true`. **Ejemplo:**

  ```javascript
  P.on('close', function () {
  	console.log('El usuario cerró el Lightbox');
  });
  ```

> **Nota:** Es posible agregar mas de un evento a la vez y multiples listener al mismo evento, por ejemplo:
>
> ```javascript
> P.on('response', function (response) {
> 	// Tu código...
> });
> // Otro código...
> P.on('response', function (response) {
> 	// Tu otro código...
> });
> P.on('close', function () {
> 	// Tu código...
>     // EJ: window.location.href = myAppResultUrl;
> });
> ```

##### Listado de eventos

| Evento     | Descripción                                                                                                                                                    | Parámetros                                                                                                                                 |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `response` | Se ejecuta cuando se recibe una respuesta de PlacetoPay.                                                                                                       | `{  reference: string; requestId: number; signature: string; status: { date: string; message: string; reason: string; status: string; } }` |
| `close`    | Se ejecuta cuando el usuario cierra el Lightbox o cuando se cierra automáticamente al finalizar el proceso y este haber sido creado con un `skipResult: true`. | N/A                                                                                                                                        |

### Ejemplo de integración

```html
<!DOCTYPE html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<title>Lightbox SDK</title>
	<script src="https://secure.placetopay.com/redirection/lightbox.min.js"></script>
</head>
<body>
	<h1>Lightbox SDK</h1>
	<button id="open">Abrir Lightbox</button>
	<script>
		// Suscribe el evento close
		P.on('close', function () {
			alert('El usuario cerró el Lightbox');
		});

		// Suscribe el evento response
		P.on('response', function (response) {
			console.log(response);
		});

		// Abre el Lightbox al hacer click en el botón
		document.getElementById('open').addEventListener('click', function () {
			// Obtén la variable processUrl de la respuesta de PlacetoPay
			var processUrl = "https://secure.placetopay.com/redirection/session/123456/1234567890abc1234567890abc12345";

			// Inicializa la URL en el Lightbox SDK
			P.init(processUrl);
		});
	</script>
</body>
</html>
```
