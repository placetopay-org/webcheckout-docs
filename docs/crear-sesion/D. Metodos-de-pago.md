---
tags: [Crear sesión]
---

# Métodos de pago

Webcheckout Placetopay contiene diversos medios de pago para brindar soluciones a las necesidades de los clientes, los cuales están divididos por proveedores de servicios, funcionando en distintos países.

Por lo tanto, la configuración de los medios de pago se brinda según el país del comercio.

## COLOMBIA

 ### ACCOUNT

 Código | Nombre
---------|----------
 DBTAC | Registro cuentas débito 

### ACH

 Código | Nombre
---------|----------
 PSEAV | Débito Bancario PSE

 ### BANCOLOMBIA

  Código | Nombre
---------|----------
 BTNBC | Botón Bancolombia 

### CODENSA

  Código | Nombre
---------|----------
 CDNSA | Tarjeta CODENSA


 ### COMFANDI

 Código | Nombre
---------|----------
 CMFDI | Comfandi 

 ### CREDIBANCO

Código | Nombre 
---------|----------
 CR_VS | Tarjeta Visa 
 CR_MC | Tarjeta Mastercard 
 CR_DN | Tarjeta Diners Club  
 CR_AM | Tarjeta American Express 
 CR_VE | Tarjeta débito Visa Electron

 ### EQUITY

  Código | Nombre
---------|----------
 CAFAM | Tarjeta CAFAM


### FLAMINGO

 Código | Nombre
---------|----------
 MEFIA | Tarjeta Mefia

 ### GANAPIN

 Código | Nombre
---------|----------
 GNPIN | Gana PIN

 ### PAGOEFECTIVO

  Código | Nombre
---------|----------
 PGEFT | Pago Efectivo 

 ### PROCESA

  Código | Nombre
---------|----------
 PRCSA | Billetera compensar 

### REDEBAN

 Código | Nombre 
---------|----------
 RM_VS | Tarjeta Visa 
 RM_MC | Tarjeta Mastercard 
 RM_DN | Tarjeta Diners Club    
 RM_AM | Tarjeta American Express 
 SOMOS | Somos Grupo EPM

 ### SAFETYPAY

  Código | Nombre
---------|----------
 SFPAY | Safety Pay

 ###  SOAP

 Código | Nombre
---------|----------
 ´_ATH_´ | Corresponsales bancarios Grupo Aval 
 ´_PSE_´ | Débito a cuentas corrientes y ahorros (PSE)
 AC_WU | Western Union
 AV_AV | Banco AV Villas Recaudos
 AV_BB | Banco de Bogota Recaudos
 AV_BO | Banco de Occidente Recaudos
 BBVAC | BBVA Colombia Oficinas y corresponsales
 DVVND | Davivienda Oficinas y corresponsales
 EFCTY | Efecty
 GNOFC | Gana Recaudo en Oficina
 SPGRS | Supergiros
 T1_BC | Bancolombia Recaudos 

 ### TUYA-DIRECT

  Código | Nombre
---------|----------
 TYDEX | Tarjeta Éxito 
 TYDAK | Tarjeta Alkosto 

## CHILE / URUGUAY

### PAYSTUDIO

 Código | Nombre
---------|----------
 PS_VS | Tarjeta Visa 
 PS_MC | Tarjeta Mastercard 
 PS_DN | Tarjeta Diners Club 
 PS_AM | Tarjeta American Express 
 PS_MS | Tarjeta Maestro 


## ECUADOR

### AUSTRO

 Código | Nombre
---------|----------
 AT_VS | Tarjeta Visa 
 AT_MC | Tarjeta Mastercard 
 AT_DN | Tarjeta Diners Club 
 AT_AM | Tarjeta American Express

### DATAFAST

 Código | Nombre
---------|----------
 DF_VS | Tarjeta Visa 
 DF_MC | Tarjeta Mastercard 
 DF_DN | Tarjeta Diners Club 
 DF_DS | Tarjeta Discover   
 DF_AM | Tarjeta American Express

### INTERDIN

 Código | Nombre
---------|----------
 ID_VS | Tarjeta Visa 
 ID_MC | Tarjeta Mastercard 
 ID_DN | Tarjeta Diners Club 
 ID_DS | Tarjeta Discover   
 ID_AM | Tarjeta American Express 

 ### MEDIANET

 Código | Nombre
---------|----------
 MD_VS | Tarjeta Visa 
 MD_MC | Tarjeta Mastercard 
 MD_DN | Tarjeta Diners Club 
 MD_AM | Tarjeta American Express 
  

## PANAMÁ / COSTA RICA / BELICE / HONDURAS

### TECNICARD

 Código | Nombre
---------|----------
 TC_VS | Tarjeta Visa 
 TC_MC | Tarjeta Mastercard 
 TC_DN | Tarjeta Diners Club 
 TC_DS | Tarjeta Discover   
 TC_AM | Tarjeta American Express  

### TELERED

  Código | Nombre
---------|----------
 TR_TC | Tarjeta Clave

### TRANSERVER

 Código | Nombre
---------|----------
 TS_VS | Tarjeta Visa 
 TS_MC | Tarjeta Mastercard 
 TS_DN | Tarjeta Diners Club 
 TS_AM | Tarjeta American Express 
 TSPVS | Tarjeta Puntos Visa 
 TSPMC | Tarjeta Puntos Mastercard 
 TSIVS | Tarjeta Internacional Visa 
 TSIMC | Tarjeta Internacional Mastercard 
 TSIDN | Tarjeta Internacional Diners Club 
 TSIAM | Tarjeta Internacional American Express 


## PUERTO RICO

### ATH-MOVIL

 Código | Nombre
---------|----------
 ATHMV | ATH Móvil 

 ### EBUS

 Código | Nombre
---------|----------
 EB_VS | Tarjeta Visa 
 EB_MC | Tarjeta Mastercard 
 EB_AM | Tarjeta American Express 
 EBATH | Tarjeta ATH 
 EBATV | Tarjeta ATH Visa 
 EBATM | Tarjeta ATH Mastercard 
 EBACH | ACH 

Al momento de crear una sesión puedes limitar los medios de pagos, de esa forma obligas a tu usuario a pagarte esa sesión con métodos de pago en específicos. Puedes enviar el listado de métodos de pago en el atributo `paymentMethod`

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
    "paymentMethod": "PS_VS, PS_MS, PS_AM"// Se define los metodos de pago a usar.

```
