# API Version Policy

En Placetopay contamos con una única versión del api disponible hasta la fecha. Tal que si te vas a conectar o ya estas conectado con nuestro api, estás usando la única versión disponible y la más actual.

Al tratarse de una única versión de API, todas las funcionalidades nuevas y ajustes se hacen en la misma versión del API y pretenden ser **retro-compatibles**.

## Cambios Retro-compatibles

En Placetopay consideramos los siguientes cambios retro-compatibles:

### Agregar nuevos recursos y endpoints.

Cuando se agrega una nueva funcionalidad, es muy probable que venga acompañada de un nuevo endpoint y/o recurso.

**Ejemplo:** Si se hiciera el lanzamiento de un nuevo API para obtener usuarios, la funcionalidad llevaría a un nuevo recurso `User` y nuevo endpoint `api.com/users`.   

### Agregar nuevos parámetros opcionales a las solicitudes de API existentes

Debido a la evolución de algunas funcionalidades, es probable que agreguemos nuevos parámetros **opcionales** en las solicitudes que pueden hacer los clientes integradores.

**Ejemplo:** En el api de `Crear Sesión` se podría agrega un parámetro **opcional** `notificationUrl` para aquellos clientes integradores que quieren definir la url de notificación de esa sesión.

```json
// CreateRequest body

{
  ...
  "payment": { ... }
  "notificationUrl": "http://example.com" // new optional parameter
  ...
}
```

Este nuevo parámetro será **opcional** y no afectará las integraciones existentes.

### Agregar nuevas propiedades en respuestas de API existentes

Debido a la evolución de algunas funcionalidades, es probable que algunas respuestas del api incluyan nuevas propiedades.

**Ejemplo:** En el api `GetRequestInformation` la respuesta puede ser modificada para incluir una nueva propidad `cancelled` dentro de la propiedad `subscription`

```json
// GetRequestInformation Response
{
  ...
  "subscription": {
    ...
    "cancelled": true, // new property
    ...
  }
  ...
}
```

Esta nueva propiedad será incluida y no afectará las integraciones existentes.

### Cambiar el orden de propiedades en respuestas de API existentes

Debido a la evolución de algunas funcionalidades, es probable que algunas respuestas del api cambien el orden de sus propiedades.

**Ejemplo:** En el api `GetRequestInformation` la respuesta puede ser modificada para que el orden de las propiedades sea diferente.

```json
// current
{
  "requestId": "123",
  "status": { ... },
  ...
}

// changes to
{
  "status": { ... }, // changed order
  "requestId": "123",
  ...
}
```

Este cambio no afectará las integraciones existentes.

