---
tags: [Crear sesión]
stoplight-id: 2d1b9eb6160d6
---

# Taxes (Impuestos)

Los impuestos son los tributos que las personas están obligadas a pagar a alguna organización.

Dependiendo de la actividad sobre la que recaiga, se le aplica un impuesto u otro. Presentan variación en la cuantía que el interesado debe abonar. Esto se basa en la normativa que presente cada sistema tributario.

## Tipos de Impuestos

El valor `kind` representa el tipo de impuesto que está incluido en el pago, los diferentes tipos de impuestos son:


Kind | Traducción | País
---------|----------|---------
 **valueAddedTax** | IVA | Todos
 **exciseDuty** | Impuesto | Todos
 **ice** | ICE | Todos
 **airportTax** | Tasa aeroportuaria | Colombia y Ecuador
 **stateTax** | IVU Estatal | Puerto Rico
 **municipalTax** | IVU Municipal | Puerto Rico
 **reducedStateTax** | IVU Reducido | Puerto Rico

<!-- theme: warning -->
> ### Importante
>
> *Cuando se escribe erroneamente el `kind` o no existe en el listado de tipos de impuestos, el `tax` no se incluye dentro de la sesión de Webcheckout*

## Estructura de los impuestos

los taxes estan dentro de la estructura `amount` siendo el atributo `taxes` un arreglo de objetos

### Ejemplo

```json
{
  "payment": {
    "amount": {
      "currency": "COP",
      "total": 10000,
      "taxes": [
        {
          "kind": "valueAddedTax",
          "amount": 1000,
          "base": 0
        },
        {
          "kind": "ice",
          "amount": 1500,
          "base": 0
        }
      ]
    }
  }
}
```

## Details (Detalles)

Los Details son los detalles que pueden tener una transacción

## Tipos de detalles

El valor `kind` representa el tipo de detalle que está incluido en el pago, los diferentes tipos de detalles son:


Kind | Traducción 
---------|----------
 **discount** | Descuento 
 **additional** | Adicional 
 **vatDevolutionBase** | Base devolución 
 **shipping** | Envío
 **handlingFee** | Cuota manejo 
 **insurance** | Seguro
 **giftWrap** | Regalo
 **subtotal** | Subtotal
 **fee** | Cobro
 **tip** | Propina
 **airline** | Aerolínea
 **interests** | Intereses
 
 <!-- theme: warning -->
> ### Nota Importante
>
> *Cuando se escribe erroneamente el `kind` o no existe en el listado de tipos de detalles, el `detail` no se incluye dentro de la sesión de Webcheckout*

## Estructura de los detalles

los `details` estan dentro de la estructura `amount` siendo el atributo `details` un arreglo de objetos

### Ejemplo

```json
{
  "payment": {
    "amount": {
      "currency": "COP",
      "total": 10000,
      "details": [
        {
          "kind": "tip",
          "amount": 1000
        },
        {
          "kind": "interests",
          "amount": 1500
        }
      ]
    }
  }
}
```

<!-- theme: danger -->
> ### Importante
>
> *No se permite el uso de pagos mixtos cuando se utilizan taxes/details ya que estos no se pueden dividir y genera un error al crear la sesión*


