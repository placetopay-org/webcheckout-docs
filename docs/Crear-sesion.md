# Crear sesión

Para realizar la creación de una sesión se debe contar con las
credenciales (login y trankey) válidas correspondientes a un sitio
habilitado.

Al momento de enviar la petición (véase [CreateRequest](https://docs-gateway.placetopay.com/docs/webcheckout-docs/5e87083a4109d-crear-sesion-create-request))
se puede especificar el `locale` con el cuál se manejará el idioma de la
sesión que se creará. En caso de que no se especifique, se tomará por
defecto el locale del sitio asociado a las credenciales enviadas basado
en su código ISO 631-1 y ISO 3166-1 alpha-2.