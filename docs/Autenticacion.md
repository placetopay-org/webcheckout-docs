---
internal: true
---

# Autenticación

La API de Webcheckout Placetopay utiliza _Web Services Security
UsernameToken Profile 1.1_ para autenticar todas las solicitudes.

La autenticación al servicio debe ser enviada sobre el objeto `auth`, el cual debe contener los siguientes atributos:

Valores como `login` y `secretKey` son suministrados por Placetopay.
El `nonce` es un valor aleatorio por cada solicitud

| Valor       | Descripción                                                                                                                                                                |
| ----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **login**   | Identificador del sitio.                                                                                                                                                   |
| **tranKey** | Valor formado por la siguiente operación: `Base64(SHA-1(nonce + seed + secretKey))`. (El nonce dentro de la operación es el original, es decir, el que no está en Base64.) |
| **nonce**   | Valor aleatorio para cada solicitud codificado en Base64.                                                                                                                  |
| **seed**    | Fecha actual, la cual se genera en formato ISO 8601.                                                                                                                       |

```json
AVISO IMPORTANTE:

Sus claves de API tienen muchos privilegios, asegúrese de mantenerlas seguras. No comparta sus claves secretas de API en áreas de acceso público como GitHub, código del lado del cliente, etc.
```

## Posibles errores

| Código | Causa                                                                                  |
| ------ | -------------------------------------------------------------------------------------- |
| 100    | UsernameToken no proporcionado (Encabezado de la autorización mal formado).            |
| 101    | Identificador de sitio no existe ( Login incorrecto o no se encuentra en el ambiente). |
| 102    | El hash de TranKey no coincide (Trankey incorrecto o mal formado).                     |
| 103    | Fecha de la semilla mayor de 5 minutos.                                                |
| 104    | Sitio inactivo.                                                                        |
| 105    | Sitio expirado.                                                                        |
| 106    | Credenciales expiradas.                                                                |
| 107    | Mala definición del UsernameToken (No cumple con el encabezado WSSE).                  |
| 200    | Saltar el encabezado de autenticación SOAP.                                            |
| 10001  | Contacte a Soporte.                                                                    |

## Errores frecuentes

- #### **Mensaje de error “Autenticación mal formada”**

Se presenta cuando el sistema no detecta que se esté enviando login, tranKey, seed o nonce en la estructura auth enviada, también puede presentarse si se envían estos datos pero de manera incorrecta, es decir sin el parámetro content-type “application/json” de manera que el servidor interpreta la petición como texto en lugar de un arreglo de datos. Puedes validar esto haciendo la petición a la URL <https://dnetix.co/p2p/client> y capturando la respuesta, es una especie de espejo de la petición que te permitirá comprobar los parámetros y el _body_ del mensaje.

- #### **Error conectando al servicio con el mensaje ERROR: javax.net.ssl.SSLHandshakeException: Remote host closed connection during handshake**

Tus servidores requieren TLSv1.2 para recibir la solicitud, debido a la norma PCI. Por favor, revisa el cifrado y el protocolo utilizado para conectar al servidor. Si usas Java, ten presente que solo las versiones después de la 8 tienen soporte completo.

- #### **SoapFault responde con el mensaje "Authentication Failed 103"**

En el proceso de autenticación, Placetopay revisamos el campo Created, este campo debe estar en el tiempo GMT o el tiempo local usando el tiempo de zona. Si obtienes esta respuesta, se debe a que tu tiempo no es preciso con el tiempo real. Nosotros solo permitimos 5 minutos de diferencia entre los tiempos. Puedes usar NTP para mantener la precisión del reloj.

- #### **Dando los mismos valores EXACTOS que en los ejemplos anteriores a la BASE64(SHA1($Nonce + $Created . $secretKey)) estoy obteniendo un password digest diferente.**

Mantén en mente que BASE64 debería ser para el raw output de la SHA1 y de acuerdo con todos los lenguajes de programación este puede ser requerido para configurar esta opción, por ejemplo. En PHP base64\_encode(sha1( … , true)) este parámetro retornaría el raw output para el sHA1 algorithm
