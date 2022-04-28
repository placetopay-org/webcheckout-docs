---
tags: [Crear sesión]
---


# Tipos de documento

Al momento de solicitar crear una sesión, si usa alguna de las estructuras `payer`, `buyer` o `shipping` deberá enviar en el atributo **`DocumentType`** alguno de los siguientes códigos  dependiendo del país:

```json
AVISO IMPORTANTE:

Según  del tipo de documento enviado el sistema realizará la validación basado en  expresiones regulares
```


### Global


Código| Tipo de documento | Regla de validación
---------|----------|----------
 PPN	 | Pasaporte | `'/^[a-zA-Z0-9_]{4,16}$/'`
 TAX | TAX | `'/^[a-zA-Z0-9_]{4,16}$/'`
 LIC | Labeler Identification Code | `'/^[a-zA-Z0-9_]{4,16}$/'`

### Puerto Rico (PR)

Para integraciones en este país no se realiza el envío de `DocumentType` ni del `Document`

### Colombia (CO)

Código| Tipo de documento | Regla de validación
---------|---------- |----------
 CC | Cédula de ciudadanía  | `'/^[1-9][0-9]{3,9}$/'`
 CE | Cédula de extranjería | `'/^([a-zA-Z]{1,5})?[1-9][0-9]{3,7}$/'`
 TI | Tarjeta de identidad| `'/^[1-9][0-9]{4,11}$/'`
 NIT | Número de Identificación Tributaria|` '/^[1-9]\d{6,9}$/'`
 RUT | Registro único tributario| `'/^[1-9]\d{6,9}$/'`

### Ecuador (EC)
Código| Tipo de documento | Regla de validación
---------|----------|---------
 CI | Cédula de identidad|`'/^\d{10}$/'`
 RUC | Registro Único de Contribuyentes|`'/^\d{13}$/'`


### Costa Rica (CR)

Código| Tipo de documento | Regla de validación
---------|----------|------------
 CRCPF | Cédula personal física |`'/^[1-9][0-9]{8}$/'`
 CPJ | Cédula personal juridica |`'/^[1-9][0-9]{9}$/'`
 DIMEX | DIMEX- Docuemnto de identificación de Migración y Extranjería|`'/^[1-9][0-9]{10,11}$/'`
  DIDI | DIDI - Docuemnto de identificación de diplomáticos|`'/^[1-9][0-9]{10,11}$/'`

### Chile (CL)

Código| Tipo de documento | Regla de validación
---------|----------|------------
 CLRUT | Cédula personal física |`'/^(\d{1,2}(?:\.?\d{1,3}){2}-[\dkK])$/'`


### Panamá (PA)

Código| Tipo de documento| Regla de validación
---------|----------|------------
 CIP | Cédula de identidad personal| `/^(N,E,PE\d+)?\d{2,6}\d{2,6}$/`

### Brasil (BR)

 Código| Tipo de documento| Regla de validación
---------|----------|------------
 CPF | Cadastro de Pessoas Físicas|`'/^\d{10,11}$/'`


### Perú (PE)

  Código| Tipo de documento| Regla de validación
---------|----------|------------
 DNI | DNI|`'/^\d{8}$/'`
  PERUC | Registro Único de Contribuyentes|`'/^(10,15,16,17,20)[0-9]{9}$/'`

### Honduras (HN)

 Código| Tipo de documento| Regla de validación
---------|----------|------------
 HNDNI | Documento nacional de identificación|`'/^[a-zA-Z0-9]{1,15}$/'`
  HNDR | Documento de residencia|`'/^[a-zA-Z0-9]{1,15}$/'`

### Belize (BZ)

 Código| Tipo de documento| Regla de validación
---------|----------|------------
 BZSSN | Identificación de Seguridad Social|`'/^[0-9]{9}$/'`
