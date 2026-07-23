[Atrás ←](/kubox/wiki/Timbre4.0)

## Timbrar
El timbrado permite enviar la datos del emisor y del receptor, responde  un objeto JSON con la información del timbre, siempre debe llevar el token en las cabeceras de la petición.

### Catalogos CFDI 4.0
[catCFDI_V_4_05052023.xls](http://omawww.sat.gob.mx/tramitesyservicios/Paginas/documentos/catCFDI_V_4_05052023.xls)

### El token en las peticiones
Para realizar cualquier petición es necesario enviar el token en las cabeceras, así que se tiene que agregar el token:

```php

-H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg3NzM2MTAsImV4cCI6MTUwODc5NTIxMCwibmJmIjoxNTA4NzczNjEwLCJqdGkiOiJIcUZPbDlWSWZSYk53N3ZqIiwic3ViIjo4NX0.GEqizwFutuibe_RYUXh3i0sOmK-PDRKK88tJBSTyJr4' \

```

---

### Timbrado CFDI Ingreso
El timbrado requiere que se envíen los datos del emisor, el receptor y los productos relacionado a la factura.
### Petición

    https://development.kubox.mx/v2/timbre/factura40

| Propiedad            | Descripción                                                                                                                                                                                                                                                             |
| ----------           | --------------------------------------                                                                                                                                                                                                                                  |
| `emisor`             | __*Object*__ ([ver Obj Emisor](#markdown-header-obj-emisor))                                                                                                                                                                                                            |
| `receptor`           | __*Object*__ ([ver Obj Receptor](#markdown-header-obj-receptor))                                                                                                                                                                                                        |
| `serie`              | __*String*__ Es el número de serie que utiliza el contribuyente para control interno de su información. Este campo acepta de 1 hasta 25 caracteres alfanuméricos.                                                                                                       |
| `folio`              | __*Number*__ Es el folio de control interno que asigna el contribuyente al comprobante, puede conformarse desde 1 hasta 40 caracteres alfanuméricos.                                                                                                                    |
| `fecha`              | __*datetime*__ Es la fecha y hora de expedición del comprobante fiscal. Se expresa en la forma AAAA-MM-DDThh:mm:ss y debe corresponder con la hora local donde se expide el comprobante                                                                                 |
| `formaDePago`        | __*number*__ Clave forma de pago(cat. c_FormaPago)                                                                                                                                                                                                                      |
| `condicionesDePago`  | __*String*__ contado, crédito *obsoleto*                                                                                                                                                                                                                                |
| `moneda`             | __*String*__ Clave moneda (c_Moneda)                                                                                                                                                                                                                                    |
| `tipoCambio`         | __*Number*__ Este campo es requerido cuando la clave de moneda es distinta de "MXN"                                                                                                                                                                                     |
| `tipoDeComprobante`  | __*String*__ "I" por ser de CFDI de ingreso                                                                                                                                                                                                                             |
| `metodoDePago`       | __*String*__ Clave de método (c_MetodoPago)                                                                                                                                                                                                                             |
| `confirmacion`       | __*String*__ Se debe registrar la clave de confirmación única e irrepetible que entrega el proveedor de certificación de CFDI o el SAT a los emisores (usuarios) para expedir el comprobante con importes o tipo de cambio fuera del rango establecido o en ambos casos |
| `usoCfdi`            | __*String*__ Contraseña de usuario                                                                                                                                                                                                                                      |
| `noCertificado`      | __*String*__ Es el número que identifica al certificado de sello digital del emisor, el cual lo incluye en el comprobante fiscal el sistema que utiliza el contribuyente para la emisión                                                                                |
| `totalImporte`       | __*Number*__ Total antes de impuestos                                                                                                                                                                                                                                   |
| `descuento`          | __*Number*__ Descuento aplicado                                                                                                                                                                                                                                         |
| `trasladosImporte`   | __*Object*__ ([ver Obj trasladosImporte](#markdown-header-obj-trasladosimporte))                                                                                                                                                                                        |
| `retencionesImporte` | __*Object*__ ([ver Obj retencionesImporte](#markdown-header-obj-retencionesimporte))                                                                                                                                                                                    |
| `total`              | __*Number*__ Es la suma del subtotal, menos los descuentos aplicables, más las contribuciones recibidas menos los impuestos retenidos federales o locales. No se permiten valores negativos                                                                             |
| `exportacion`        | __*String*__ Clave que indica si la factura es exportación ([ver lista exportacion](#markdown-header-lista-exportacion))                                                                                                                                                |
| `productos`          | __*Object*__ ([ver Obj productos](#markdown-header-obj-productos))                                                                                                                                                                                                      |
| `informacionGlobal`  | __*Object*__ Se especifica cuando son ventas a publico en general ([ver Obj informacionGlobal](#markdown-header-obj-informacionglobal))                                                                                                                                                                                      |

---


### **Obj emisor**

| Propiedad         | Descripción                             |
| ----------        |--------------------------------------   |
| `nombreFiscal`    | __*String*__ Se puede registrar el nombre, denominación o razón social del emisor del comprobante                     |
| `rfc`             | __*String*__  Clave del Registro Federal de Contribuyentes                                                |
| `regimenFiscal`   | __*String*__ clave del régimen fiscal del contribuyente (c_RegimenFiscal)                                              |
| `calle`           | __*String*__ Calle                      |
| `noExterior`      | __*String*__ No Exterior                |
| `noInterior`      | __*String*__ No Interior                |
| `colonia`         | __*String*__ Colonia                    |
| `localidad`       | __*String*__ Localidad                  |
| `municipio`       | __*String*__ Municipio                  |
| `estado`          | __*String*__ Estado                     |
| `pais`            | __*String*__ Pais                       |
| `cp`              | __*String*__ Código Postal              |
| `cer`             | __*String*__ Certificado .pem en base64 |
| `key`             | __*String*__ Key .pem en base64         |

---

### **Obj receptor**

| Propiedad     | Descripción                             |
| ----------    |--------------------------------------   |
| `nombreFiscal`| __*String*__ Se puede registrar el nombre, denominación o razón social del emisor del comprobante                   |
| `rfc`         | __*String*__ Clave del Registro Federal de Contribuyentes                                            |
| `regimenFiscal`   | __*String*__ clave del régimen fiscal del contribuyente (c_RegimenFiscal)                                              |
| `calle`       | __*String*__ Calle                      |
| `noExterior`  | __*String*__ No Exterior                |
| `noInterior`  | __*String*__ No Interior                |
| `colonia`     | __*String*__ Colonia                    |
| `localidad`   | __*String*__ Localidad                  |
| `municipio`   | __*String*__ Municipio                  |
| `estado`      | __*String*__ Estado                     |
| `pais`        | __*String*__ Pais                       |
| `cp`          | __*String*__ Código Postal              |

---


### **Obj trasladosImporte**

| Propiedad | Descripción                             |
| ----------|--------------------------------------   |
| `ieps`    | __*Number*__ Cantidad de IEPS           |
| `iva`     | __*Number*__ Cantidad de IVA            |

---


### **Obj productos**

| Propiedad                 | Descripción                             |
| ------------------------  |--------------------------------------   |
| `claveProdServ`           | __*String*__ Clave Producto (c_ClaveProdServ)|
| `claveUnidad`             | __*String*__ Clave Unidad (c_ClaveUnidad)|
| `cantidad`                | __*Number*__ Cantidad del bien o servicio|
| `concepto`                | __*String*__ Descripción del producto/serv.|
| `cuentaPredial`           | __*String*__ En este nodo se puede expresar el número de cuenta predial con el que fue registrado el inmueble en el sistema catastral de la entidad federativa de que trate                          |
| `descuentoProd`           | __*String*__ Se puede registrar el importe de los descuentos aplicables a cada concepto, debe tener hasta la cantidad de decimales que tenga registrado en el atributo importe del concepto y debe ser menor o igual al campo Importe. No se permiten valores negativos         |
| `descuentoProdPorcent`    | __*Number*__ Valor porcentual del descuento|
| `importe`                 | __*Number*__ Se debe registrar el importe total de los bienes o servicios de cada concepto. Debe ser equivalente al resultado de multiplicar la cantidad por el valor unitario expresado en el concepto, el cual debe ser calculado por el sistema que genera el comprobante y considerará los redondeos que tenga registrado este campo en el estándar tecnico del Anexo 20. No se permiten valores negativos                                     |
| `noIdentificacion`        | __*String*__ En este campo se puede registrar el número de parte, identificador del producto o del servicio, la clave de producto o servicio, SKU (número de referencia) o equivalente            |
| `retencionCedular`        | __*String*__ Retención cedular del producto|
| `retencionCedularPorcent` | __*String*__ Valor Porcentual de la retención cedular|
| `retencionIsr`            | __*String*__ Retención Isr del producto    |
| `retencionIsrPorcent`     | __*String*__ Valor Porcentual de la retención Isr                                                                      |
| `retencionIva`            | __*String*__ Retención Iva del producto    |
| `retencionIvaPorcent`     | __*String*__ Valor Porcentual de la retención Iva                                                                      |
| `retencionIvc`            | __*String*__ Retención Ivc del producto    |
| `retencionIvcPorcent`     | __*String*__ Valor Porcentual de la retención Ivc                                                                      |
| `trasladoCedular`         | __*String*__ Importe del traslado para impuesto Cedular                                                                  |
| `trasladoCedularPorcent`  | __*String*__ Valor porcentual del impuesto Cedular                                                                  |
| `trasladoIeps`            | __*String*__ Importe del  traslado Ieps    |
| `trasladoIepsPorcent`     | __*String*__ Valor porcentual de Ieps      |
| `trasladoIsh`             | __*String*__ Importe del traslado Ish      |
| `trasladoIshPorcent`      | __*String*__ Valor porcentual de Ish       |
| `trasladoIva`             | __*String*__ Importe del traslado Iva      |
| `trasladoIvaPorcent`      | __*String*__ Valor porcentual de Iva       |
| `valorUnitario`           | __*String*__ En este campo se debe registrar el valor o precio unitario del bien o servicio por cada concepto, el cual puede contener de cero hasta seis decimales                                    |
| `objetoImp`          | __*String*__ Clave para indicar el tipo de impuestos ([ver lista objetoImp](#markdown-header-lista-objetoimp)) |

### Ejemplo de petición

```php
  curl https://development.kubox.mx/v2/timbre/factura40 \
     -H "Content-type: application/json" \
     -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg3NzM2MTAsImV4cCI6MTUwODc5NTIxMCwibmJmIjoxNTA4NzczNjEwLCJqdGkiOiJIcUZPbDlWSWZSYk53N3ZqIiwic3ViIjo4NX0.GEqizwFutuibe_RYUXh3i0sOmK-PDRKK88tJBSTyJr4' \
     -X POST -d '{
    "emisor": {
      "nombreFiscal"  : "ESCUELA KEMPER URGATE SA DE CV",
      "rfc"           : "EKU9003173C9",
      "regimenFiscal" : "601",
      "calle"         : "Calle 1",
      "noExterior"    : "23",
      "noInterior"    : "",
      "colonia"       : "Colonia",
      "localidad"     : "",
      "municipio"     : "VILLA",
      "estado"        : "COLIMA",
      "pais"          : "MEXICO",
      "cp"            : "28984",
      "cer"           : "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQklqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUFqZEtYaXFZSHppKytZbUViOVg2cQp2cUZXTEN6MVZFZnhvbTJKaGluUFNKeHhjdVpXQmVqazJJNXlDTDVwRG5VYUcyeHBRbE1Ua1YvN1M3SmZHR3ZZCkp1bUtPNFI1emcwUVNBN3FkeGlFaGN3Zi9la2ZTdnpNMkVEbkxIRENLQVF3RVdzbkp5Nzh1eFpUTHp1LzY1VloKN0VnRWNXVVR2Q3MvR1pKTEk5czZYbUtZMlNNbXY5K3ZmcUJxa0pOWEUwWkI2T2ZTYnllRTMyNVA5NGlNbitCLwp5SjR2WndYdlhHRnFOREp5cUcrd3c3Zjc3SFl1YlFQSmpMUVBlZHkycVRjZ21TQXdrVUVKVkJqWUE2bVBmL0JlClpsTDFZSkhITTdDSUJuYjMvYnpFRDBuOTQ0d29pbys0K3JuTVpkZmhjQ1ZwbTc0RFpvbWxFZjlLdUp0cTV1L0oKUlFJREFRQUIKLS0tLS1FTkQgUFVCTElDIEtFWS0tLS0tCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQpNSUlGdXpDQ0E2T2dBd0lCQWdJVU16QXdNREV3TURBd01EQTBNREF3TURJME16UXdEUVlKS29aSWh2Y05BUUVMCkJRQXdnZ0VyTVE4d0RRWURWUVFEREFaQlF5QlZRVlF4TGpBc0JnTlZCQW9NSlZORlVsWkpRMGxQSUVSRklFRkUKVFVsT1NWTlVVa0ZEU1U5T0lGUlNTVUpWVkVGU1NVRXhHakFZQmdOVkJBc01FVk5CVkMxSlJWTWdRWFYwYUc5eQphWFI1TVNnd0pnWUpLb1pJaHZjTkFRa0JGaGx2YzJOaGNpNXRZWEowYVc1bGVrQnpZWFF1WjI5aUxtMTRNUjB3Ckd3WURWUVFKREJRemNtRWdZMlZ5Y21Ga1lTQmtaU0JqWVdScGVqRU9NQXdHQTFVRUVRd0ZNRFl6TnpBeEN6QUoKQmdOVkJBWVRBazFZTVJrd0Z3WURWUVFJREJCRFNWVkVRVVFnUkVVZ1RVVllTVU5QTVJFd0R3WURWUVFIREFoRApUMWxQUVVOQlRqRVJNQThHQTFVRUxSTUlNaTQxTGpRdU5EVXhKVEFqQmdrcWhraUc5dzBCQ1FJVEZuSmxjM0J2CmJuTmhZbXhsT2lCQlEwUk5RUzFUUVZRd0hoY05NVGt3TmpFM01UazBOREUwV2hjTk1qTXdOakUzTVRrME5ERTAKV2pDQjRqRW5NQ1VHQTFVRUF4TWVSVk5EVlVWTVFTQkxSVTFRUlZJZ1ZWSkhRVlJGSUZOQklFUkZJRU5XTVNjdwpKUVlEVlFRcEV4NUZVME5WUlV4QklFdEZUVkJGVWlCVlVrZEJWRVVnVTBFZ1JFVWdRMVl4SnpBbEJnTlZCQW9UCkhrVlRRMVZGVEVFZ1MwVk5VRVZTSUZWU1IwRlVSU0JUUVNCRVJTQkRWakVsTUNNR0ExVUVMUk1jUlV0Vk9UQXcKTXpFM00wTTVJQzhnV0VsUlFqZzVNVEV4TmxGRk5ERWVNQndHQTFVRUJSTVZJQzhnV0VsUlFqZzVNVEV4TmsxSApVazFhVWpBMU1SNHdIQVlEVlFRTEV4VkZjMk4xWld4aElFdGxiWEJsY2lCVmNtZGhkR1V3Z2dFaU1BMEdDU3FHClNJYjNEUUVCQVFVQUE0SUJEd0F3Z2dFS0FvSUJBUUNOMHBlS3BnZk9MNzVpWVJ2MWZxcStvVllzTFBWVVIvR2kKYlltR0tjOUluSEZ5NWxZRjZPVFlqbklJdm1rT2RSb2JiR2xDVXhPUlgvdExzbDhZYTlnbTZZbzdoSG5PRFJCSQpEdXAzR0lTRnpCLzk2UjlLL016WVFPY3NjTUlvQkRBUmF5Y25Mdnk3RmxNdk83L3JsVm5zU0FSeFpSTzhLejhaCmtrc2oyenBlWXBqWkl5YS8zNjkrb0dxUWsxY1RSa0hvNTlKdko0VGZiay8zaUl5ZjRIL0luaTluQmU5Y1lXbzAKTW5Lb2I3RER0L3ZzZGk1dEE4bU10QTk1M0xhcE55Q1pJRENSUVFsVUdOZ0RxWTkvOEY1bVV2VmdrY2N6c0lnRwpkdmY5dk1RUFNmM2pqQ2lLajdqNnVjeGwxK0Z3SldtYnZnTm1pYVVSLzBxNG0ycm03OGxGQWdNQkFBR2pIVEFiCk1Bd0dBMVVkRXdFQi93UUNNQUF3Q3dZRFZSMFBCQVFEQWdiQU1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQ0FRQmMKcGoxVGpUNGppaW5JdWpJZEFsRnpFNmtSd1lKQ25ERzA4elNwNGtTblNoanhBREdFWEgyY2hlaEtNVjBGWTdjNApuakE1ZURHZEEvRzJPQ1RQdkY1cnBlQ1pQNUR3NTA0UlprWURsMnN1Unord2Exc05CVnBibkJKRUswZlFjTjNJCmZ0QndzZ05GZEZoVXRDeXczbHVzMVNTSmJQeGpMSFM2RmNaWjUxWVNlSWZjTlhPQXVUcWRpbXVzYVhxMTVHclMKckNPa002bjJqZmoyc01KWU0ySFhhWEo2ckdURWdZbWhZZHd4V3RpbDZSZlpCK2ZHUS9IOUk5V0xubDRLVFpVUwo2QzkrTkxIaDRGUERoU2sxOWZwUzJTLzU2YXFnRm9HQWtYQVl0OUZ5NUVDYVBjVUxJZkoxREVic1hLeVJkQ3YzCkpZODkrME1Oa09kYURuc2VtUzJvNUdsMDh6STRpWXR0M0w0MGdBWjYwTlBoMzFrVkxuWU5zbXZmTnhZeUtwK0EKZUp0REh5Vzl3N2Z0TTBIb2krQnVSbWNBUVNLRlYzcGs4ajUxbGEranJSQnJBVXY4YmxiUmNRNUJpWlV3SnpIRgpFS0l3VHNSR29SeUV4OTZzTm5CMDNuNkdUd2pJR3o5MlNtTGRObDk1cjlya3ZwKzJtNFM2cTFsUHVYYUZnN0RHCkJyWFdDOGl5cWVXRTJpb2Jkd0lJdVhQVE1WcVFiMTJtMWRBa0pWUk81TmRIblAvTXBxT3ZPZ0xxb1pCTkhHeUIKZzRHcW00c0NKSEN4QTFjOEVsZmEyUlFUQ2swdEF6bGxMNHZPbkkxR0hrR0puNjV4b2tHc2FVNEI0RDM2eGg3ZQpXcmZqNC9wZ1dIbXRvREFZYTh3elN3bzJHVkNaT3MrbXRFZ09RQjkxL2c9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==",
      "key"           : "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpQcm9jLVR5cGU6IDQsRU5DUllQVEVECkRFSy1JbmZvOiBERVMtRURFMy1DQkMsOEY5QzYxOUQyNkM1M0M0QwoKOE5GRVlSSU9ZT0l3aXVOSDNTVUlkeW93WGtxQmVlWDhydGpCYVlXZWJmcHY4dzdEcFJvZnVaVHRzcEtqTXhQSwp5K1NQUHdkVUF1cVlmc3c2UVk3ZWZ2WVRGZ0pFVUlXb2lJRmhlblQyYmtvektPMExoeVVHNXVuZUJWczVObzhkCjZIdDUzdkpXeEkwK2NzYU5nQTNpR0ZUQTVaT2FyQlR1alg4aTVqMFVBR0haMVNURksvQ1BJUHhPVE45bWV4WDcKblFXMzhERzkva1RBd2d4Z3NGaG9EbFdCeWluWndpeXRYcGNEa1Y5UDEwZDF2RUJkeVhFa0FxV25nK0dNa2ZpOApxanI3d29iTDl0Zm9iOW9pb0ZxbVJjQy9lYmlIa3lTZjFuZUlQNEU1RFhHaGJwcFBkWTNhbkdQbjRLaE12TFF6CjZPZ3BOaVkwKzlja3BIclppMlFpMGNwdFBFRjBUWi9IK2dTK1doamtGQWhta2ppSG5CNEZUSy8zVVdmeVhjazUKWXlSWDU2MDV1Q2ZaZ3Jtd3dOMURwQ3dKR2dLcW1EMStZUmZXWDB3TVZSTVMxWDBOVTBIMzZmZGhheFI5OGpPNQp3eHZMVGVlYTF2NUpUTjk1TjZ0R3YxL1BKYVVUQnU5SnlBQmsyRzc5bnl3R0lMdFloLzYzN3ROeUxPaFA3N2FGCmlTL0JWdkFZR1lZZVN5QW9Ra0dQL1poUjFoNFZ4UmFnL21paHpOOE02aHBEN3Nwa2U5MmJ4d0RhZjlLTVhiUVUKZkRCd2tBeis0SjV4TGh6OEgweUpNQjJQUVNQNkJ1M1dhMm5XcnM4THcyTGMxTFhrN1VpZjNSbkd3cDg1WjdregplcEhuQTlUVnRDR3BIME15Y2Z2Mm5FbTk0S2FRVi9lZjVCb3NyWUl4aUl6WkZFZlZ0Q3dXQ2xueHpEWkt1a3ErCkZMZHVrQlpET1k1ekZpM3h4YStKRS9LbjFlcHdxYk9oMDlkVk1UL1ZzUXk4SHZYc3pIcDl3TnhHTEFmV3RrTlAKS0lhTHYyVWxoTkZHekVWbW03U09YU0FRTmM2WFNsT0NzeThhcU5aOE9uS1ppeDVWVSt3Wngxa0Ryd1NObWZ1bQp4Uk9BZjJwdnNTc2hDL045Y2ljTjhmTFpyS2JBbzJoMERCMDJReWt1bW5obnNPVXVEQ2VUUmdlU1pKNTF3M0VwCnBJdHB1WWwvRThITnRpb3hxRG9wL1pOdHhnd05XNm9XaVU4T29sSEFjbzRxd0xMN2hXQThJTDlROGszcy9kQ1QKSWpNUTJKLzhZSkRlM3dRN2xwbXRvZlNSRUNRTGZvYWpEbkdHOXhkaFJkVUdBRnNwM01PcVBpajF6Y3dXYWVJUwpUckRHUnNGMWI1dG85TXRHWHhUV2p1SVVxT3VETVpVcXJkbjQ3THBxZVljLytvNmw5NldvTkpVaW5zN3ZFN21RCldPcjd2QTFPYndnR1IzM1Y1Rkp2a1N2UUkvNUZVeUNSeXFkUHBJSStZOHFIS1J0cDFtdzVQNlhEakhwa3ByUWoKdEZEeW1FWDV5VWNZSkFMRWs4Wk5uR1lISnc3VHo2SU5rMnl2cVpXdlpBTG5qNDhPSFJEaE9ieGdJeFZITHZIdwpzVjFoQ2lnM1FNOVF0L3p4RGo4ejNKVzlsbElzSXBld2ZIaFRyay9XN1NySVozWThHOXI1dnYxeWFmRFFQdnViCnN0ZUZvYWhQQlNmUFdWenJ6aDNtdnBraW1KMzhrRUNEd3JYR0xROGxsenZOdTV1b0JjNkdQRy80cGJwYVJGSGMKTi9jMUVUZVk5MjZyYWNVWWJyR1FLbDJZUE5FWVNjL1ExT0xzaG4za0VjeFhVWjhHTDRGczFhQVdTYVpIbVBEawpKSDdKRWYxM0dyWlc5WW5ua0hvWUl1WFQ1UngzemhBQ0R3MEV3bVRHNGYrTVprbldNbVQ3WDh0Zml5aTFWOUhvCld6QVJnYzhpTDNqZkJ4TDYvTnFoRHFJOUx3dmdzSEZKbnFONjV1Q0xkdHQzek82RXhFSml3akhiVE42NnhocjAKMFB4MXBUb2diakxhYzRoVXNsVklYQUZ1QkJxYlJlZFlDZS8wSnA2YkpSTGtMWngxWmI5YTFBPT0KLS0tLS1FTkQgUlNBIFBSSVZBVEUgS0VZLS0tLS0K"
    },
    "receptor": {
      "nombreFiscal"  : "CESAR OSBALDO CRUZ SOLORZANO",
      "rfc"           : "CUSC850516316",
      "calle"         : "Calle del norte",
      "noExterior"    : "33",
      "noInterior"    : "",
      "colonia"       : "",
      "localidad"     : "",
      "municipio"     : "",
      "estado"        : "Aguascalientes",
      "pais"          : "México",
      "cp"            : "45638",
      "regimenFiscal" : "612"
    },
    "serie"             : "F",
    "folio"             : 12,
    "fecha"             : "2022-05-18T09:18:19",
    "formaDePago"       : "03",
    "condicionesDePago" : "CONTADO",
    "moneda"            : "MXN",
    "tipoCambio"        : "1",
    "tipoDeComprobante" : "I",
    "metodoDePago"      : "PUE",
    "confirmacion"      : "",
    "usoCfdi"           : "I04",
    "exportacion"       : "01",
    "noCertificado"     : "30001000000400002434",
    "totalImporte" : "2231.00",
    "descuento"    : "50",
    "total": "2529.96",
    "trasladosImporte": {
        "ieps": "0",
        "iva": "348.96"
    },
   "productos": [
        {
            "claveProdServ": "81111500",
            "claveUnidad": "H87",
            "cantidad": "1",
            "concepto": "Producto 1",
            "cuentaPredial": "152122",
            "descuentoProd": "0",
            "descuentoProdPorcent": "0",
            "importe": "1231.00",
            "noIdentificacion": "123",
            "retencionCedular": "0",
            "retencionCedularPorcent": "0",
            "retencionIsr": "0",
            "retencionIsrPorcent": "0",
            "retencionIva": "0",
            "retencionIvaPorcent": "0",
            "retencionIvc": "0",
            "retencionIvcPorcent": "0",
            "trasladoCedular": "0",
            "trasladoCedularPorcent": "0",
            "trasladoIeps": "0",
            "trasladoIepsPorcent": "0",
            "trasladoIsh": "0",
            "trasladoIshPorcent": "0",
            "trasladoIva": "196.96",
            "trasladoIvaPorcent": "16",
            "valorUnitario": "1231.00",
            "objetoImp": "02"
        },
        {
            "claveProdServ": "81111500",
            "claveUnidad": "H87",
            "cantidad": "1",
            "concepto": "Producto 2",
            "descuentoProd": "50",
            "descuentoProdPorcent": "5",
            "importe": "1000",
            "noIdentificacion": "312",
            "retencionCedular": "0",
            "retencionCedularPorcent": "0",
            "retencionIsr": "0",
            "retencionIsrPorcent": "0",
            "retencionIva": "0",
            "retencionIvaPorcent": "0",
            "retencionIvc": "0",
            "retencionIvcPorcent": "0",
            "trasladoCedular": "0",
            "trasladoCedularPorcent": "0",
            "trasladoIeps": "0",
            "trasladoIepsPorcent": "0",
            "trasladoIsh": "0",
            "trasladoIshPorcent": "0",
            "trasladoIva": "152",
            "trasladoIvaPorcent": "16",
            "valorUnitario": "1000.00",
            "objetoImp": "02"
        }
    ]

}'
```

## Otros Impuestos

Si necesitas agregar más impuestos, puedes agregar los siguientes objetos a la petición (al igual que el objeto trasladosImporte)

### **Obj retencionesImporte**

| Propiedad   | Descripción                             |
| ----------  |--------------------------------------   |
| `isr`       | __*Number*__ Cantidad de retención ISR  |
| `iva`       | __*Number*__ Cantidad de retención IVA  |

---

### **Obj trasladosLocalImporte**

| Propiedad   | Descripción                             |
| ----------  |--------------------------------------   |
| `cedular`   | __*Number*__ Cantidad de cedular        |
| `ish`       | __*Number*__ Cantidad de ish            |

---

### **Obj retencionesLocalImporte**

| Propiedad   | Descripción                             |
| ----------  |--------------------------------------   |
| `cedular`   | __*Number*__ Cantidad de retención cedular      |
| `deductivas`| __*Number*__ Cantidad de retención deductivas   |
| `ivc`       | __*Number*__ Cantidad de retención ivc          |

---

### **Obj informacionGlobal**

| Propiedad      | Descripción                                                                                                                                         |
| ----------     | ------------                                                                                                                                        |
| `periodicidad` | __*String*__ Frecuencia con que se genera las ventas a publico en general ([ver Lista informacionGlobal](#markdown-header-lista-informacionglobal)) |
| `meses`        | __*String*__ Mes en el que corresponde la venta a publico en general ([ver Lista informacionGlobal](#markdown-header-lista-informacionglobal))      |
| `anio`         | __*Number*__ Año que corresponde la venta a publico en general                                                                                      |

---

### **Lista informacionGlobal**

| Clave        | Descripción         |
| ----------   | ------------        |
| Periodicidad                       |
| ----------   | ------------        |
| `01`         | Diario              |
| `02`         | Semanal             |
| `03`         | Quincenal           |
| `04`         | Mensual             |
| `05`         | Bimestral           |
| ----------   | ------------        |
| Meses                              |
| ----------   | ------------        |
| `01`         | Enero               |
| `02`         | Febrero             |
| `03`         | Marzo               |
| `04`         | Abril               |
| `05`         | Mayo                |
| `06`         | Junio               |
| `07`         | Julio               |
| `08`         | Agosto              |
| `09`         | Septiembre          |
| `10`         | Octubre             |
| `11`         | Noviembre           |
| `12`         | Diciembre           |
| `13`         | Enero-Febrero       |
| `14`         | Marzo-Abril         |
| `15`         | Mayo-Junio          |
| `16`         | Julio-Agosto        |
| `17`         | Septiembre-Octubre  |
| `18`         | Noviembre-Diciembre |

---


### **Lista exportacion**

| Clave      | Descripción  |
| ---------- | ------------ |
| `01`       | No aplica    |
| `02`       | Definitiva   |
| `03`       | Temporal     |

---


### **Lista objetoImp**

| Clave      | Descripción                                      |
| ---------- | ------------                                     |
| `01`       | No objeto de impuesto                            |
| `02`       | Si objeto de impuesto                            |
| `03`       | Si objeto del impuesto y no obligado al desglose |

---


##Complementos

También puedes agragar los complementos INE, Notario.

```json
{
    "ine": {
      "tipoProceso": "Ordinario",
      "tipoComite": "Ejecutivo Estatal",
      "idContabilidad": "",
      "entidad": [
        {
          "claveEntidad": "COL",
          "ambito": "",
          "contabilidad": {
            "idContabilidad": [
              "2323"
            ]
          }
        }
      ]
    },

    "notario": {
      "curp": "MESG880710HCMNLM02",
      "numNotaria": "22",
      "entFederal": "01",
      "adscripcion": "Ddas das das d",
      "operacion": {
        "numNotarial": "01",
        "fechaNotarial": "2017-07-10",
        "subtotal": "100000",
        "iva": "16000",
        "total": "116000"
      },
      "inmueble": [
        {
          "tipo": "01",
          "calle": "Calle 21",
          "noExterior": "32",
          "noInterior": "",
          "colonia": "",
          "localidad": "",
          "referencia": "",
          "municipio": "villa",
          "estado": "06",
          "pais": "MEX",
          "cp": "28984"
        }
      ],
      "enajenanteCoproSoc": "Si",
      "enajenante": [
        {
          "nombre": "Gamaliel",
          "apePaterno": "mendoza",
          "apeMaterno": "solis",
          "rfc": "MESG880710EC6",
          "curp": "",
          "porcentaje": "50"
        },
        {
          "nombre": "Patricia",
          "apePaterno": "garcia",
          "apeMaterno": "lopez",
          "rfc": "MAR980114GQA",
          "curp": "",
          "porcentaje": "50"
        }
      ],
      "adquirienteCoproSoc": "No",
      "adquiriente": [
        {
          "nombre": "Pepe",
          "apePaterno": "del campo",
          "apeMaterno": "carra",
          "rfc": "VAAM130719H60",
          "curp": "",
          "porcentaje": "100"
        }
      ]
    },

    "instEducativas": {
        "nombreAlumno": "Juan Carlos Mendoza Garcia",
        "curp": "CASS930122MCMSLS03",
        "nivelEducativo": "Primaria",
        "autRVOE": "06PPR0050D",
        "rfcPago": "MESG880710EC6"
    }
}

```

---

### Timbrado CFDI Egreso

El timbrado requiere que se envíen los datos del emisor, el receptor y los productos relacionado a la factura, sin embargo, es necesario que se envíen los datos del CFDI relacionado.


### Petición

    https://development.kubox.mx/v2/timbre/factura40

```php
  curl https://development.kubox.mx/v2/timbre/factura40 \
     -H "Content-type: application/json" \
     -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg4NzE1NTcsImV4cCI6MTUwODg5MzE1NywibmJmIjoxNTA4ODcxNTU3LCJqdGkiOiJVUks0bFFBZzNwbTlaYzRiIiwic3ViIjo4NX0.SRERzevo_MZ1PVmguj0i3joiWtY0IpfRsn5JVgjPmc4' \
    -X POST -d '{
        "emisor": {
          "nombreFiscal"  : "ALLIANCE EMPEÑOS S DE RL DE CV",
          "rfc"           : "ACO560518KW7",
          "regimenFiscal" : "601",
          "calle"         : "Calle 1",
          "noExterior"    : "23",
          "noInterior"    : "",
          "colonia"       : "Colonia",
          "localidad"     : "",
          "municipio"     : "VILLA",
          "estado"        : "COLIMA",
          "pais"          : "MEXICO",
          "cp"            : "28984",
          "cer"           : "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0NCk1JSUJJakFOQmdrcWhraUc5dzBCQVFFRkFBT0NBUThBTUlJQkNnS0NBUUVBdWtZZmQyOTd2UUwrSHRsbFBNZHYNCktkbzBUWEtraTlwWEtVQWNQdmVTQVg5RUhVSjk4dVJvY2RwdjBZV01CRHFIZllGRXV4RWRoUC9rWG11Y3RHQ0wNCmEzTGoyTkxWcktwZHFIeEVkdUpibHdWc1lnOS9zSTEyNXFBVW5aZ3ZpLzl2MlRwZDV2RnBPb2k4VVNNMDhBd0INCnNrR2JxZHk4RlR3dGM1bGxsUlRQbmVrM3hsdUJYM3ZMSDBkMXhVV2JyQ1VLVHV5UlEyVk13clA3aGFaVllMYTkNClM5ckdLcm9hY0YrSG4xQjZRUlQyQVNKRjZWQ1RGOTErWFFDY21wQkNDWThQSmk5MytiOGxKSG9CeDU0QUR0TXINCld4MnNpZVhnUUtXMGEreW1FVUdXNGtncDlsRTdRZlIrWVVsamVlWWdjSndxZUxENEE5RDgzRTh4UUxNbS9odUwNCmZRSURBUUFCDQotLS0tLUVORCBQVUJMSUMgS0VZLS0tLS0NCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQ0KTUlJRjZ6Q0NBOU9nQXdJQkFnSVVNakF3TURFd01EQXdNREF6TURBd01EVTJPVEl3RFFZSktvWklodmNOQVFFTA0KQlFBd2dnRm1NU0F3SGdZRFZRUUREQmRCTGtNdUlESWdaR1VnY0hKMVpXSmhjeWcwTURrMktURXZNQzBHQTFVRQ0KQ2d3bVUyVnlkbWxqYVc4Z1pHVWdRV1J0YVc1cGMzUnlZV05wdzdOdUlGUnlhV0oxZEdGeWFXRXhPREEyQmdOVg0KQkFzTUwwRmtiV2x1YVhOMGNtRmphY096YmlCa1pTQlRaV2QxY21sa1lXUWdaR1VnYkdFZ1NXNW1iM0p0WVdOcA0KdzdOdU1Ta3dKd1lKS29aSWh2Y05BUWtCRmhwaGMybHpibVYwUUhCeWRXVmlZWE11YzJGMExtZHZZaTV0ZURFbQ0KTUNRR0ExVUVDUXdkUVhZdUlFaHBaR0ZzWjI4Z056Y3NJRU52YkM0Z1IzVmxjbkpsY204eERqQU1CZ05WQkJFTQ0KQlRBMk16QXdNUXN3Q1FZRFZRUUdFd0pOV0RFWk1CY0dBMVVFQ0F3UVJHbHpkSEpwZEc4Z1JtVmtaWEpoYkRFUw0KTUJBR0ExVUVCd3dKUTI5NWIyRmp3NkZ1TVJVd0V3WURWUVF0RXd4VFFWUTVOekEzTURGT1RqTXhJVEFmQmdrcQ0KaGtpRzl3MEJDUUlNRWxKbGMzQnZibk5oWW14bE9pQkJRMFJOUVRBZUZ3MHhOREV4TWpVd01ETTNNamxhRncweA0KT0RFeE1qVXdNRE0zTWpsYU1JSFhNU2N3SlFZRFZRUURGQjVCVEV4SlFVNURSU0JGVFZCRjBVOVRJRk1nUkVVZw0KVWt3Z1JFVWdRMVl4SnpBbEJnTlZCQ2tVSGtGTVRFbEJUa05GSUVWTlVFWFJUMU1nVXlCRVJTQlNUQ0JFUlNCRA0KVmpFbk1DVUdBMVVFQ2hRZVFVeE1TVUZPUTBVZ1JVMVFSZEZQVXlCVElFUkZJRkpNSUVSRklFTldNU1V3SXdZRA0KVlFRdEV4eEJRMDgxTmpBMU1UaExWemNnTHlCSVJVZFVOell4TURBek5GTXlNUjR3SEFZRFZRUUZFeFVnTHlCSQ0KUlVkVU56WXhNREF6VFVSR1RsTlNNRGd4RXpBUkJnTlZCQXNUQ2xOMVkzVnljMkZzSURFd2dnRWlNQTBHQ1NxRw0KU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLQW9JQkFRQzZSaDkzYjN1OUF2NGUyV1U4eDI4cDJqUk5jcVNMMmxjcA0KUUJ3Kzk1SUJmMFFkUW4zeTVHaHgybS9SaFl3RU9vZDlnVVM3RVIyRS8rUmVhNXkwWUl0cmN1UFkwdFdzcWwybw0KZkVSMjRsdVhCV3hpRDMrd2pYYm1vQlNkbUMrTC8yL1pPbDNtOFdrNmlMeFJJelR3REFHeVFadXAzTHdWUEMxeg0KbVdXVkZNK2Q2VGZHVzRGZmU4c2ZSM1hGUlp1c0pRcE83SkZEWlV6Q3MvdUZwbFZndHIxTDJzWXF1aHB3WDRlZg0KVUhwQkZQWUJJa1hwVUpNWDNYNWRBSnlha0VJSmp3OG1MM2Y1dnlVa2VnSEhuZ0FPMHl0YkhheUo1ZUJBcGJScg0KN0tZUlFaYmlTQ24yVVR0QjlINWhTV041NWlCd25DcDRzUGdEMFB6Y1R6RkFzeWIrRzR0OUFnTUJBQUdqSFRBYg0KTUF3R0ExVWRFd0VCL3dRQ01BQXdDd1lEVlIwUEJBUURBZ2JBTUEwR0NTcUdTSWIzRFFFQkN3VUFBNElDQVFDdQ0KZHFHalZpWm1nWEtZaDNKQjJCU0h5Mi90UG0xTzV4cnFXS2U4SUZ6VElaS2hEU2ZNQmRtYUY1OE14ZklwdDJjYw0KeTNORGNyNDZuNWtzbkE0ZWZrZU5pWmNSNFU5VzlkeTE5VGpmSGRaNGg4VS8xanBrMURSYjlBUU83L0I3V0NRTA0KM1pZNXlpUlNKaitlNEpHMFNxcnRQVWdtTVFJRzZYTlFVZWNBa0R2cVZFZFB1b3Ztdm9RZXRLekZ6SlZ0K0tibw0KYVQzVjVXcG1pNTZvamp1cERuU002RU5xVG1ScldTeml6alZTVElZZExBdTFkNWsyME11ZnhSZDhJSFA4VlpFRA0KNEJGdnFlWEpaa2ZhZXAvZXIwbzdLelpacmNTQ0dDS3RXMXc4bE1yOWRYNGZDRG1jeE5CNE0yMlNxWDBmeDFJTQ0KdkFHdHMyYzZDWEZGR2UyNDV3UjFZcUN2ekFmeVhUdC9kWXdoNWtxV1BqRW0rUFJVV0Qxd294a3JwZ24yUDNJdg0KOUJIWEFsSXZUK085NDN0NkpROVhCRGxwMVUvUk5YRHh2QS91V29tQ09VT3JJa05zZzRvUW54a2MyZ2VSdGp1NQ0KcWtZaHI3TUVnOHR5S1lUTkdxeE5ISittT0M0RDNDMGxDNGxGZXJkbndFSHJLazQrUHEwaDkvZjVBYkZDNzNDcg0KejRWeDdRalB2WDZNalZjR3ZsZmthK292NHpkdEljODMvZFBpajNDU1RVdjlPQ0RybmZuYUhsejh5UWNGOTRkQQ0KT2VXN3lrWXVpbWJaNkhkaTdKc25GTVZIZkRlRHQ5akRnUUJCem9BZGFKVXhvWU9BODA5c0kxZVpKUjRrSEVvbg0KbGFpQ0dGcVY2SHBTNkV0QlZ0ZlhmdDZqNERwTFhRQnF1OGJJZ1lvU1pBPT0NCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0=",
          "key"           : "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQ0KUHJvYy1UeXBlOiA0LEVOQ1JZUFRFRA0KREVLLUluZm86IERFUy1FREUzLUNCQywxNEUyQzA3NjQwQ0YxQUJDDQoNCjgyaDArMEZzaCtPTnVUTk1ZcHJHVEZ4YWNtZkZmdnJMYXhmUXhzK2NqMThFNW1lMVFONUJHc1JxWEIxZHR3eGMNCno4cStZUUEzMENyNUtOMHV2a1p2WFZrdHJHd09MOWI4Rnc0TDdPdmdhTWhucWViYTFVM0Z4cGxsbTgvR2F1MjQNCkRZN2JTci9ER2pRNzFianR2NXRCL1BMUUNZTHJVdlQ5YkZIY3hWc0tnSVNlMDRNMFdwOEQyOXBMQUZnM0VEbWgNCkFWMWpueWlKVnpwbHZ5OWxQS0JEK3NEZjBvMWhhb0FmVjRQY3AxYkc3T2RxbTlrbW5FcDdyTjZXREZiQWw0MW8NCmRjSnQvRStBMC9UdmVvTU56U0JyZUttQWJPYmYyNFdKcVQzTjd4ZGtHRGczN3o1YWoyQWlHeTZYemRnd0VwaFYNCk03dGRTdnJCWXBrNmtQL21tbkpjbm8vdmxXeEt6akNnQ0wyWlZTcXQ0SU1GbkRiVFRtUCtnblNqbXExaU5BcUgNCjk2KzlpMzRhdXFBT0YzTXlrcllsVmIvL0x3d1pZSVkrNkk4cDBCY1UwNmx3R2I1RUVaazNBcjFnbTVTUTVNZE4NCjFpUzJ5M21RY0ZIa2ZhNENpeUhabm9FdnB5VytjZ2grSlJmOVdHR1pKUE5FVjNnRyt4MncrNlU2WEczdzhpcVUNClFvd1ZPb1dUeUx0UHNDWTZNSGpJNWM0YnNhTU1YMXlYQ0prbDl6VmJVZ0VrWkF3VTdtdXpUdGp2Qm5NZ3VpZVENCll3TFNpUTMwb2svZTNrM2l6QytncjJyNEZEOVYrdnVSb01iTnRWUEZFM0VTVWltZDgzNkdVNXphbndVM2NxTisNCmdnMWlOR25mK1JYc1FESXpTcDFzK2RIc2h3OGU2ZmswbURSSXBzMnZFcWdyaDJKVXBoMDdwZTh1aDd1SVdWU1YNClJzRUxZTXRQbXY0UUg4T2VrUzFxMTNoNm5uZXdJT2dzSmEvWjVrb0c2MHFRUEFmc1M5dUJiemNvK21zdVFxemcNCkJzUG1mRkhDMFJwRERVUW9ZTnRPR1FJdnp6N2Z1bHBhWkJ2bXNmVndRUUVTNGRnZUN6UzRTcXduZll4MzlyVzQNCkMzZWpMbk94aFA5d2twUG1yNUJIVUNWelVoRUlxSjljV2NETHgrUFczU3NTZkt1OWN6UXNwQXprZW1DRTJFYUENCis2ajRHRWExZm5rNmt0bHNMQ2JRbENqVWdOSzlXUE03Q200Y1A4K256Ky9KelNxdkhVMmYwRGV1VnBIbFV1SEsNCkFYRWFVVEpDbUZJUFdZaU0rUkFJMHBiL1RqT0Q1akYwYmRVWHhvbE8wdXVybktzSXZoekZVbEIxc25ycCtkdEENCkgwSzk1K0I3WjNpVm5aaGQ1KzZveGF6dFdieVduSkc3Y0ZJczdLTzdSVjRQTmZrTExtU3A2OEl6QXAyR3MzU0ENCjZHYzFGdUdkbUNYR1o1NGJtRGlXVWxhQnBtcU52WWZ4YkNXUHIrS2NNWGdMVEJUNHN0c0c3Q1JETUE5ZU5pWkcNClg5b2QydStvT0d1UElDRWVmL3Bza0Q0NXgvMVVaenQzTFJvc1ZEeWYzcWlxNkxzb3hoVkpSOUlGdW1Oa29sSE0NCjl1N3pmYmU3VzFHKzhoQ3oxRS9pOXpLVjVBOXphRXVUeWlvTE9CTEtWREpKM2pKcm5QNVhKSGUzNzF3T21waEENCmFwVFhRdEx2RjFRQ3dMWTVWKzFVSnNUdHhFdmNTcmtYdGlKNFJqUC84WVpiVkNoYnZwVHk0Lzh5ZGdYM1J3Y3oNCkxDUGs3Tzl3T2FPSFpVSk4zbG9ldnJkUWFLUlJYc3Q1MFp1NllIa0hlb2FrWTQ3cDRpOW9MblgyZ2tzVnhxa3ENCnJKTE9KSFMzcTBrN3QyRGFNWUp1WTd5dVJySmk3Q25LSmwxWjBBdEpxQnpNNk54b0kxOEY0cUJvWHhsaU1lOEENCjVKallZc3I4cHBLZTk3Y1k5NDk0azAwZ1A1dVpxQUQ0Y1BHVWYzYlU0OHFMMUtEcXQzT2hsbTlETm9MOXVaOSsNCnJLY1FSUncyUkVHS0lsNEY2cS81Ly9IYXhEa1hJcFNlRElHNjFBdXpKamlPc2JpLzZvQTlvZz09DQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQ=="
        },
        "receptor": {
          "nombreFiscal": "GAMALIEL MENDOZA SOLIS",
          "rfc"         : "MESG880710EC6",
          "calle"       : "Calle del norte",
          "noExterior"  : "40",
          "noInterior"  : "",
          "colonia"     : "",
          "localidad"   : "",
          "municipio"   : "",
          "estado"      : "Aguascalientes",
          "pais"        : "México",
          "cp"          : ""
        },

        "serie"             : "NC",
        "folio"             : 3,
        "fecha"             : "2017-10-10T14:18:19",
        "formaDePago"       : "03",
        "condicionesDePago" : "CONTADO",
        "moneda"            : "MXN",
        "tipoCambio"        : "1",
        "tipoDeComprobante" : "E",
        "metodoDePago"      : "PUE",
        "confirmacion"      : "",
        "usoCfdi"           : "G02",
        "noCertificado"     : "20001000000300005692",

        "totalImporte" : "25754.05753",
        "descuento"    : "1287.6678765",
        "trasladosImporte": {
            "ieps": "0",
            "iva": "3914.51034"
        },
        "retencionesImporte": {
            "isr": "0",
            "iva": "2609.755115"
        },
        "trasladosLocalImporte": {
            "cedular": "0",
            "ish": "2446.56896"
        },
        "retencionesLocalImporte": {
            "cedular": "0",
            "deductivas": "0",
            "ivc": "0"
        },
        "total": "28217.00",

        "productos": [
            {
                "claveProdServ": "81111500",
                "claveUnidad": "H87",
                "cantidad": "34.0",
                "concepto": "Producto 1",
                "descuentoProd": "1287.6678765",
                "descuentoProdPorcent": "5",
                "importe": "25754.05753",
                "noIdentificacion": "123",
                "retencionCedular": "0",
                "retencionCedularPorcent": "0",
                "retencionIsr": "0",
                "retencionIsrPorcent": "0",
                "retencionIva": "2609.755115",
                "retencionIvaPorcent": "10.667",
                "retencionIvc": "0",
                "retencionIvcPorcent": "0",
                "trasladoCedular": "0",
                "trasladoCedularPorcent": "0",
                "trasladoIeps": "0",
                "trasladoIepsPorcent": "0",
                "trasladoIsh": "2446.56896",
                "trasladoIshPorcent": "10",
                "trasladoIva": "3914.51034",
                "trasladoIvaPorcent": "16",
                "valorUnitario": "774.0741"
            }
        ],

        "cfdiRelacionados": {
          "tipoRelacion": "01",
          "cfdiRelacionado": [
            {
              "uuid": "2783EB87-469D-4510-8B8F-74D516580CBB"
            }
          ]
        }
    }'

```

---

### Timbrado CFDI Pago

El timbrado requiere que se envíen los datos del emisor, el receptor y los productos relacionado a la factura, sin embargo, es necesario que se envíen los datos del CFDI relacionado.


### Petición

    https://development.kubox.mx/v2/timbre/factura40

```php
  curl https://development.kubox.mx/v2/timbre/factura40 \
     -H "Content-type: application/json" \
     -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg5NDQ5OTksImV4cCI6MTUwODk2NjU5OSwibmJmIjoxNTA4OTQ0OTk5LCJqdGkiOiJkOGc2NDk5TFE5UUUyRWxGIiwic3ViIjo4NX0.-uAHoSLXEc50SoGTQKVm8VPtrWn9ThjmrPmA-ZTHC_4' \
    -X POST -d '{
        "emisor": {
          "nombreFiscal"  : "ALLIANCE EMPEÑOS S DE RL DE CV",
          "rfc"           : "ACO560518KW7",
          "regimenFiscal" : "601",
          "calle"         : "fsdlkj",
          "noExterior"    : "23",
          "noInterior"    : "",
          "colonia"       : "sdflkj",
          "localidad"     : "",
          "municipio"     : "VILLA",
          "estado"        : "COLIMA",
          "pais"          : "MEXICO",
          "cp"            : "28984",
          "cer"           : "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0NCk1JSUJJakFOQmdrcWhraUc5dzBCQVFFRkFBT0NBUThBTUlJQkNnS0NBUUVBdWtZZmQyOTd2UUwrSHRsbFBNZHYNCktkbzBUWEtraTlwWEtVQWNQdmVTQVg5RUhVSjk4dVJvY2RwdjBZV01CRHFIZllGRXV4RWRoUC9rWG11Y3RHQ0wNCmEzTGoyTkxWcktwZHFIeEVkdUpibHdWc1lnOS9zSTEyNXFBVW5aZ3ZpLzl2MlRwZDV2RnBPb2k4VVNNMDhBd0INCnNrR2JxZHk4RlR3dGM1bGxsUlRQbmVrM3hsdUJYM3ZMSDBkMXhVV2JyQ1VLVHV5UlEyVk13clA3aGFaVllMYTkNClM5ckdLcm9hY0YrSG4xQjZRUlQyQVNKRjZWQ1RGOTErWFFDY21wQkNDWThQSmk5MytiOGxKSG9CeDU0QUR0TXINCld4MnNpZVhnUUtXMGEreW1FVUdXNGtncDlsRTdRZlIrWVVsamVlWWdjSndxZUxENEE5RDgzRTh4UUxNbS9odUwNCmZRSURBUUFCDQotLS0tLUVORCBQVUJMSUMgS0VZLS0tLS0NCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQ0KTUlJRjZ6Q0NBOU9nQXdJQkFnSVVNakF3TURFd01EQXdNREF6TURBd01EVTJPVEl3RFFZSktvWklodmNOQVFFTA0KQlFBd2dnRm1NU0F3SGdZRFZRUUREQmRCTGtNdUlESWdaR1VnY0hKMVpXSmhjeWcwTURrMktURXZNQzBHQTFVRQ0KQ2d3bVUyVnlkbWxqYVc4Z1pHVWdRV1J0YVc1cGMzUnlZV05wdzdOdUlGUnlhV0oxZEdGeWFXRXhPREEyQmdOVg0KQkFzTUwwRmtiV2x1YVhOMGNtRmphY096YmlCa1pTQlRaV2QxY21sa1lXUWdaR1VnYkdFZ1NXNW1iM0p0WVdOcA0KdzdOdU1Ta3dKd1lKS29aSWh2Y05BUWtCRmhwaGMybHpibVYwUUhCeWRXVmlZWE11YzJGMExtZHZZaTV0ZURFbQ0KTUNRR0ExVUVDUXdkUVhZdUlFaHBaR0ZzWjI4Z056Y3NJRU52YkM0Z1IzVmxjbkpsY204eERqQU1CZ05WQkJFTQ0KQlRBMk16QXdNUXN3Q1FZRFZRUUdFd0pOV0RFWk1CY0dBMVVFQ0F3UVJHbHpkSEpwZEc4Z1JtVmtaWEpoYkRFUw0KTUJBR0ExVUVCd3dKUTI5NWIyRmp3NkZ1TVJVd0V3WURWUVF0RXd4VFFWUTVOekEzTURGT1RqTXhJVEFmQmdrcQ0KaGtpRzl3MEJDUUlNRWxKbGMzQnZibk5oWW14bE9pQkJRMFJOUVRBZUZ3MHhOREV4TWpVd01ETTNNamxhRncweA0KT0RFeE1qVXdNRE0zTWpsYU1JSFhNU2N3SlFZRFZRUURGQjVCVEV4SlFVNURSU0JGVFZCRjBVOVRJRk1nUkVVZw0KVWt3Z1JFVWdRMVl4SnpBbEJnTlZCQ2tVSGtGTVRFbEJUa05GSUVWTlVFWFJUMU1nVXlCRVJTQlNUQ0JFUlNCRA0KVmpFbk1DVUdBMVVFQ2hRZVFVeE1TVUZPUTBVZ1JVMVFSZEZQVXlCVElFUkZJRkpNSUVSRklFTldNU1V3SXdZRA0KVlFRdEV4eEJRMDgxTmpBMU1UaExWemNnTHlCSVJVZFVOell4TURBek5GTXlNUjR3SEFZRFZRUUZFeFVnTHlCSQ0KUlVkVU56WXhNREF6VFVSR1RsTlNNRGd4RXpBUkJnTlZCQXNUQ2xOMVkzVnljMkZzSURFd2dnRWlNQTBHQ1NxRw0KU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLQW9JQkFRQzZSaDkzYjN1OUF2NGUyV1U4eDI4cDJqUk5jcVNMMmxjcA0KUUJ3Kzk1SUJmMFFkUW4zeTVHaHgybS9SaFl3RU9vZDlnVVM3RVIyRS8rUmVhNXkwWUl0cmN1UFkwdFdzcWwybw0KZkVSMjRsdVhCV3hpRDMrd2pYYm1vQlNkbUMrTC8yL1pPbDNtOFdrNmlMeFJJelR3REFHeVFadXAzTHdWUEMxeg0KbVdXVkZNK2Q2VGZHVzRGZmU4c2ZSM1hGUlp1c0pRcE83SkZEWlV6Q3MvdUZwbFZndHIxTDJzWXF1aHB3WDRlZg0KVUhwQkZQWUJJa1hwVUpNWDNYNWRBSnlha0VJSmp3OG1MM2Y1dnlVa2VnSEhuZ0FPMHl0YkhheUo1ZUJBcGJScg0KN0tZUlFaYmlTQ24yVVR0QjlINWhTV041NWlCd25DcDRzUGdEMFB6Y1R6RkFzeWIrRzR0OUFnTUJBQUdqSFRBYg0KTUF3R0ExVWRFd0VCL3dRQ01BQXdDd1lEVlIwUEJBUURBZ2JBTUEwR0NTcUdTSWIzRFFFQkN3VUFBNElDQVFDdQ0KZHFHalZpWm1nWEtZaDNKQjJCU0h5Mi90UG0xTzV4cnFXS2U4SUZ6VElaS2hEU2ZNQmRtYUY1OE14ZklwdDJjYw0KeTNORGNyNDZuNWtzbkE0ZWZrZU5pWmNSNFU5VzlkeTE5VGpmSGRaNGg4VS8xanBrMURSYjlBUU83L0I3V0NRTA0KM1pZNXlpUlNKaitlNEpHMFNxcnRQVWdtTVFJRzZYTlFVZWNBa0R2cVZFZFB1b3Ztdm9RZXRLekZ6SlZ0K0tibw0KYVQzVjVXcG1pNTZvamp1cERuU002RU5xVG1ScldTeml6alZTVElZZExBdTFkNWsyME11ZnhSZDhJSFA4VlpFRA0KNEJGdnFlWEpaa2ZhZXAvZXIwbzdLelpacmNTQ0dDS3RXMXc4bE1yOWRYNGZDRG1jeE5CNE0yMlNxWDBmeDFJTQ0KdkFHdHMyYzZDWEZGR2UyNDV3UjFZcUN2ekFmeVhUdC9kWXdoNWtxV1BqRW0rUFJVV0Qxd294a3JwZ24yUDNJdg0KOUJIWEFsSXZUK085NDN0NkpROVhCRGxwMVUvUk5YRHh2QS91V29tQ09VT3JJa05zZzRvUW54a2MyZ2VSdGp1NQ0KcWtZaHI3TUVnOHR5S1lUTkdxeE5ISittT0M0RDNDMGxDNGxGZXJkbndFSHJLazQrUHEwaDkvZjVBYkZDNzNDcg0KejRWeDdRalB2WDZNalZjR3ZsZmthK292NHpkdEljODMvZFBpajNDU1RVdjlPQ0RybmZuYUhsejh5UWNGOTRkQQ0KT2VXN3lrWXVpbWJaNkhkaTdKc25GTVZIZkRlRHQ5akRnUUJCem9BZGFKVXhvWU9BODA5c0kxZVpKUjRrSEVvbg0KbGFpQ0dGcVY2SHBTNkV0QlZ0ZlhmdDZqNERwTFhRQnF1OGJJZ1lvU1pBPT0NCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0=",
          "key"           : "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQ0KUHJvYy1UeXBlOiA0LEVOQ1JZUFRFRA0KREVLLUluZm86IERFUy1FREUzLUNCQywxNEUyQzA3NjQwQ0YxQUJDDQoNCjgyaDArMEZzaCtPTnVUTk1ZcHJHVEZ4YWNtZkZmdnJMYXhmUXhzK2NqMThFNW1lMVFONUJHc1JxWEIxZHR3eGMNCno4cStZUUEzMENyNUtOMHV2a1p2WFZrdHJHd09MOWI4Rnc0TDdPdmdhTWhucWViYTFVM0Z4cGxsbTgvR2F1MjQNCkRZN2JTci9ER2pRNzFianR2NXRCL1BMUUNZTHJVdlQ5YkZIY3hWc0tnSVNlMDRNMFdwOEQyOXBMQUZnM0VEbWgNCkFWMWpueWlKVnpwbHZ5OWxQS0JEK3NEZjBvMWhhb0FmVjRQY3AxYkc3T2RxbTlrbW5FcDdyTjZXREZiQWw0MW8NCmRjSnQvRStBMC9UdmVvTU56U0JyZUttQWJPYmYyNFdKcVQzTjd4ZGtHRGczN3o1YWoyQWlHeTZYemRnd0VwaFYNCk03dGRTdnJCWXBrNmtQL21tbkpjbm8vdmxXeEt6akNnQ0wyWlZTcXQ0SU1GbkRiVFRtUCtnblNqbXExaU5BcUgNCjk2KzlpMzRhdXFBT0YzTXlrcllsVmIvL0x3d1pZSVkrNkk4cDBCY1UwNmx3R2I1RUVaazNBcjFnbTVTUTVNZE4NCjFpUzJ5M21RY0ZIa2ZhNENpeUhabm9FdnB5VytjZ2grSlJmOVdHR1pKUE5FVjNnRyt4MncrNlU2WEczdzhpcVUNClFvd1ZPb1dUeUx0UHNDWTZNSGpJNWM0YnNhTU1YMXlYQ0prbDl6VmJVZ0VrWkF3VTdtdXpUdGp2Qm5NZ3VpZVENCll3TFNpUTMwb2svZTNrM2l6QytncjJyNEZEOVYrdnVSb01iTnRWUEZFM0VTVWltZDgzNkdVNXphbndVM2NxTisNCmdnMWlOR25mK1JYc1FESXpTcDFzK2RIc2h3OGU2ZmswbURSSXBzMnZFcWdyaDJKVXBoMDdwZTh1aDd1SVdWU1YNClJzRUxZTXRQbXY0UUg4T2VrUzFxMTNoNm5uZXdJT2dzSmEvWjVrb0c2MHFRUEFmc1M5dUJiemNvK21zdVFxemcNCkJzUG1mRkhDMFJwRERVUW9ZTnRPR1FJdnp6N2Z1bHBhWkJ2bXNmVndRUUVTNGRnZUN6UzRTcXduZll4MzlyVzQNCkMzZWpMbk94aFA5d2twUG1yNUJIVUNWelVoRUlxSjljV2NETHgrUFczU3NTZkt1OWN6UXNwQXprZW1DRTJFYUENCis2ajRHRWExZm5rNmt0bHNMQ2JRbENqVWdOSzlXUE03Q200Y1A4K256Ky9KelNxdkhVMmYwRGV1VnBIbFV1SEsNCkFYRWFVVEpDbUZJUFdZaU0rUkFJMHBiL1RqT0Q1akYwYmRVWHhvbE8wdXVybktzSXZoekZVbEIxc25ycCtkdEENCkgwSzk1K0I3WjNpVm5aaGQ1KzZveGF6dFdieVduSkc3Y0ZJczdLTzdSVjRQTmZrTExtU3A2OEl6QXAyR3MzU0ENCjZHYzFGdUdkbUNYR1o1NGJtRGlXVWxhQnBtcU52WWZ4YkNXUHIrS2NNWGdMVEJUNHN0c0c3Q1JETUE5ZU5pWkcNClg5b2QydStvT0d1UElDRWVmL3Bza0Q0NXgvMVVaenQzTFJvc1ZEeWYzcWlxNkxzb3hoVkpSOUlGdW1Oa29sSE0NCjl1N3pmYmU3VzFHKzhoQ3oxRS9pOXpLVjVBOXphRXVUeWlvTE9CTEtWREpKM2pKcm5QNVhKSGUzNzF3T21waEENCmFwVFhRdEx2RjFRQ3dMWTVWKzFVSnNUdHhFdmNTcmtYdGlKNFJqUC84WVpiVkNoYnZwVHk0Lzh5ZGdYM1J3Y3oNCkxDUGs3Tzl3T2FPSFpVSk4zbG9ldnJkUWFLUlJYc3Q1MFp1NllIa0hlb2FrWTQ3cDRpOW9MblgyZ2tzVnhxa3ENCnJKTE9KSFMzcTBrN3QyRGFNWUp1WTd5dVJySmk3Q25LSmwxWjBBdEpxQnpNNk54b0kxOEY0cUJvWHhsaU1lOEENCjVKallZc3I4cHBLZTk3Y1k5NDk0azAwZ1A1dVpxQUQ0Y1BHVWYzYlU0OHFMMUtEcXQzT2hsbTlETm9MOXVaOSsNCnJLY1FSUncyUkVHS0lsNEY2cS81Ly9IYXhEa1hJcFNlRElHNjFBdXpKamlPc2JpLzZvQTlvZz09DQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQ=="
        },
        "emisorSucursal": {
          "nombre"     : "",
          "calle"      : "",
          "noExterior" : "",
          "noInterior" : "",
          "colonia"    : "",
          "localidad"  : "",
          "municipio"  : "",
          "estado"     : "",
          "pais"       : "",
          "cp"         : ""
        },
        "receptor": {
          "nombreFiscal": "GAMALIEL MENDOZA SOLIS",
          "rfc"         : "MESG880710EC6",
          "calle"       : "Calle del norte",
          "noExterior"  : "40",
          "noInterior"  : "",
          "colonia"     : "",
          "localidad"   : "",
          "municipio"   : "",
          "estado"      : "Aguascalientes",
          "pais"        : "México",
          "cp"          : ""
        },

        "serie"             : "P",
        "folio"             : 2,
        "fecha"             : "2017-10-24T12:18:19",
        "formaDePago"       : "03",
        "condicionesDePago" : "CONTADO",
        "moneda"            : "MXN",
        "tipoCambio"        : "1",
        "tipoDeComprobante" : "P",
        "metodoDePago"      : "PUE",
        "confirmacion"      : "",
        "usoCfdi"           : "P01",
        "noCertificado"     : "20001000000300005692",

        "totalImporte" : "0",
        "descuento"    : "0",
        "subTotal"     : "0",
        "trasladosImporte": {
            "ieps": "0",
            "iva": "0"
        },
        "retencionesImporte": {
            "isr": "0",
            "iva": "0"
        },
        "trasladosLocalImporte": {
            "cedular": "0",
            "ish": "0"
        },
        "retencionesLocalImporte": {
            "cedular": "0",
            "deductivas": "0",
            "ivc": "0"
        },
        "total": "0",

        "productos": [
            {
                "cantidad": "1",
                "claveProdServ": "84111506",
                "claveUnidad": "ACT",
                "concepto": "Pago",
                "descuentoProd": "0",
                "descuentoProdPorcent": "0",
                "importe": "0",
                "noIdentificacion": "",
                "retencionCedular": "0",
                "retencionCedularPorcent": "0",
                "retencionIsr": "0",
                "retencionIsrPorcent": "0",
                "retencionIva": "0",
                "retencionIvaPorcent": "0",
                "retencionIvc": "0",
                "retencionIvcPorcent": "0",
                "subtotal": "0",
                "trasladoCedular": "0",
                "trasladoCedularPorcent": "0",
                "trasladoIeps": "0",
                "trasladoIepsPorcent": "0",
                "trasladoIsh": "0",
                "trasladoIshPorcent": "0",
                "trasladoIva": "0",
                "trasladoIvaPorcent": "0",
                "valorUnitario": "0"
            }
        ],
        "pagos": [
          {
              "cadenaPago": "",
              "certificadoPago": "",
              "cuentaBen": "5345345345345",
              "cuentaOrd": "123456789123456789",
              "fechaPago": "2017-07-19T00:18:19",
              "formaDePago": "03",
              "moneda": "MXN",
              "monto": "1523.62",
              "nombreBancoOrdExt": "",
              "numOperacion": "BB14999013003",
              "rfcEmisorCtaBen": "BMN930209927",
              "rfcEmisorCtaOrd": "BBA940707IE1",
              "selloPago": "",
              "tipoCadPago": "",
              "tipoCambio": "1",
              "doctoRelacionado": [
                  {
                      "idDocumento": "A88C5532-8A6C-43E1-8E8C-E94CD7C85A9F",
                      "serie": "",
                      "folio": "18",
                      "moneda": "MXN",
                      "tipoCambio": "1",
                      "metodoDePago": "PPD",
                      "numParcialidad": "1",
                      "saldoAnterior": "1523.62",
                      "importePagado": "1523.62",
                      "saldoInsoluto": "0"
                  }
              ]
          }
        ]
    }'
```

### Ejemplo de Respuesta correcta

Retorna un objeto con la información de la cadena original, el sello, certificado, xml, UUID y un mensaje.

```json

{
    "errors": false,
    "data": {
        "cadenaOriginal": "||4.0|F|10|2017-10-23T14:18:19|03|20001000000300005692|CONTADO|2231.00|50.00|MXN|1|2529.96|I|PUE|28984|ACO560518KW7|ALLIANCE EMPEÑOS S DE RL DE CV|601|AAA010101AAA|ALAN SINUE PASTOR PIÑA|I04|81111500|123|1|H87|Producto 1|1231.00|1231.00|1231.00|002|Tasa|0.160000|196.96|152122|81111500|312|1|H87|Producto 2|1000.00|1000.00|50.00|950.00|002|Tasa|0.160000|152.00|002|Tasa|0.160000|348.96|348.96||",
        "sello": "rx1a0tekPWCFRpVf0soo6hhSQjJ1wu/lIICxIYlOF3mAjJiDXMbyznnQKtZ63NlenqYYGvR0cg7zyjCM/jXActKMdSC8uqaNmuyhhN8d4zXYQVnE99ZhM5wTQzRQdgYwQpCcq04AcLhxBnD7KIQTq2Avw5+y+aaIXC68W9dB/luymaXtKTPhkjauVtymFToid/MO51wfyVcjif7l+8LJeCPyZbNGKH+mWrg7QQyUA73pcuaOHG4ruFfGwFDrnpK+qkbW7t+VyFxMiVgz8mGwXEoZX3xV7yqTwlyADnV9EFlNVKXAki0evEtZ+C1oJTB3kIQFKO2fWTcx79P+GvV8BQ==",
        "certificado": "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",
        "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?>\n<cfdi:Comprobante xmlns:cfdi=\"http://www.sat.gob.mx/cfd/3\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:schemaLocation=\"http://www.sat.gob.mx/cfd/3 http://www.sat.gob.mx/sitio_internet/cfd/3/cfdv40.xsd\" Version=\"4.0\" Serie=\"F\" Folio=\"10\" Fecha=\"2017-10-23T14:18:19\" Sello=\"rx1a0tekPWCFRpVf0soo6hhSQjJ1wu/lIICxIYlOF3mAjJiDXMbyznnQKtZ63NlenqYYGvR0cg7zyjCM/jXActKMdSC8uqaNmuyhhN8d4zXYQVnE99ZhM5wTQzRQdgYwQpCcq04AcLhxBnD7KIQTq2Avw5+y+aaIXC68W9dB/luymaXtKTPhkjauVtymFToid/MO51wfyVcjif7l+8LJeCPyZbNGKH+mWrg7QQyUA73pcuaOHG4ruFfGwFDrnpK+qkbW7t+VyFxMiVgz8mGwXEoZX3xV7yqTwlyADnV9EFlNVKXAki0evEtZ+C1oJTB3kIQFKO2fWTcx79P+GvV8BQ==\" FormaPago=\"03\" NoCertificado=\"20001000000300005692\" Certificado=\"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\" CondicionesDePago=\"CONTADO\" SubTotal=\"2231.00\" Descuento=\"50.00\" Moneda=\"MXN\" TipoCambio=\"1\" Total=\"2529.96\" TipoDeComprobante=\"I\" MetodoPago=\"PUE\" LugarExpedicion=\"28984\"><cfdi:Emisor Rfc=\"ACO560518KW7\" Nombre=\"ALLIANCE EMPEÑOS S DE RL DE CV\" RegimenFiscal=\"601\"/><cfdi:Receptor Rfc=\"AAA010101AAA\" Nombre=\"ALAN SINUE PASTOR PIÑA\" UsoCFDI=\"I04\"/><cfdi:Conceptos><cfdi:Concepto ClaveProdServ=\"81111500\" NoIdentificacion=\"123\" Cantidad=\"1\" ClaveUnidad=\"H87\" Descripcion=\"Producto 1\" ValorUnitario=\"1231.00\" Importe=\"1231.00\"><cfdi:Impuestos><cfdi:Traslados><cfdi:Traslado Base=\"1231.00\" Impuesto=\"002\" TipoFactor=\"Tasa\" TasaOCuota=\"0.160000\" Importe=\"196.96\"/></cfdi:Traslados></cfdi:Impuestos><cfdi:CuentaPredial Numero=\"152122\"/></cfdi:Concepto><cfdi:Concepto ClaveProdServ=\"81111500\" NoIdentificacion=\"312\" Cantidad=\"1\" ClaveUnidad=\"H87\" Descripcion=\"Producto 2\" ValorUnitario=\"1000.00\" Importe=\"1000.00\" Descuento=\"50.00\"><cfdi:Impuestos><cfdi:Traslados><cfdi:Traslado Base=\"950.00\" Impuesto=\"002\" TipoFactor=\"Tasa\" TasaOCuota=\"0.160000\" Importe=\"152.00\"/></cfdi:Traslados></cfdi:Impuestos></cfdi:Concepto></cfdi:Conceptos><cfdi:Impuestos TotalImpuestosTrasladados=\"348.96\"><cfdi:Traslados><cfdi:Traslado Impuesto=\"002\" TipoFactor=\"Tasa\" TasaOCuota=\"0.160000\" Importe=\"348.96\"/></cfdi:Traslados></cfdi:Impuestos><cfdi:Complemento><tfd:TimbreFiscalDigital xmlns:tfd=\"http://www.sat.gob.mx/TimbreFiscalDigital\" xsi:schemaLocation=\"http://www.sat.gob.mx/TimbreFiscalDigital http://www.sat.gob.mx/sitio_internet/cfd/TimbreFiscalDigital/TimbreFiscalDigitalv11.xsd\" Version=\"1.1\" SelloCFD=\"rx1a0tekPWCFRpVf0soo6hhSQjJ1wu/lIICxIYlOF3mAjJiDXMbyznnQKtZ63NlenqYYGvR0cg7zyjCM/jXActKMdSC8uqaNmuyhhN8d4zXYQVnE99ZhM5wTQzRQdgYwQpCcq04AcLhxBnD7KIQTq2Avw5+y+aaIXC68W9dB/luymaXtKTPhkjauVtymFToid/MO51wfyVcjif7l+8LJeCPyZbNGKH+mWrg7QQyUA73pcuaOHG4ruFfGwFDrnpK+qkbW7t+VyFxMiVgz8mGwXEoZX3xV7yqTwlyADnV9EFlNVKXAki0evEtZ+C1oJTB3kIQFKO2fWTcx79P+GvV8BQ==\" NoCertificadoSAT=\"20001000000300022323\" RfcProvCertif=\"FIN1203015JA\" UUID=\"BD20A82F-91DB-4CFC-85C6-3D1FE4A0ED97\" FechaTimbrado=\"2017-10-24T11:31:30\" SelloSAT=\"bTjx6+Dxhllk9bILuLEHeHRVtJ0oZo5mXlT5gbkZOkgO0HORfSsi2RT8bAflM0jN140l+gZ9B1tmWI5xSt1C4uUxbnIo83EzDAERIBobuYcfS9OhuioCND/DTXOUfL4T8K6vbqVHTDZLSTmx4Dl+QAXvlu4m10kreaeLHge4pTdk7eK+4nq7+LzCnNelUy8RqPQnGB1G1ScKujwgqHJrrP0D+jan44LB+ntKF9KeKgk3+0c6y3Ds4aGbuiPuQt3Y9RJ/z8Mk+pMS7QlPgKnwxjAVY7804dceebmcFjqEsSAO/RWSceUevJXf/8AdpLiWFDOjpvdkFR4VF0DWjGzSKQ==\"/></cfdi:Complemento></cfdi:Comprobante>",
        "uuid": "BD20A82F-91DB-4CFC-85C6-3D1FE4A0ED97",
        "msg": "Comprobante timbrado satisfactoriamente"
    },
    "status_code": 200
}

```

---

### Objeto Error
Kubox responde objetos JSON en caso de error, los errores son muy descriptivos, sin embargo, si tienes una duda puedes contactarnos al correo `soporte@kubox.mx`.

| Propiedad     | Descripción                             |
| ----------    |--------------------------------------   |
| `errors`      | __*Object/String*__ Errores             |
| `status_code` | __*String*__ Código de error HTTP       |

#### Códigos de error

| Error HTTP | Causa                                   |
| ---------- |--------------------------------------   |
| `422`      | Error en la validación de datos         |
| `400`      | Error en formato permitido              |

#### Ejemplo de respuesta con error de validación

```json
{
    "errors": {
        "emisor.rfc": [
            "El campo emisor.rfc no es un valor valido (no cumple con el patrón de validación)."
        ],
        "emisor.regimenFiscal": [
            "El campo emisor.regimen fiscal es obligatorio."
        ]
    },
    "status_code": 422
}
```

#### Ejemplos de respuesta con error de formato

```json
{
    "errors": {
        "timbre": [
            "La clave del campo RegimenFiscal debe corresponder con el tipo de persona (fisica o moral) "
        ]
    },
    "status_code": 400
}

{
    "errors": "La clave del campo RegimenFiscal debe corresponder con el tipo de persona (fisica o moral) ",
    "status_code": 400
}

{
    "errors": {
        "timbre": [
            "El TipoDeComprobante es I,E o N, el importe registrado en el campo no es igual a la suma de los importes de los conceptos registrados."
        ]
    },
    "status_code": 400
}

{
    "errors": "La clave del campo RegimenFiscal debe corresponder con el tipo de persona (fisica o moral) ",
    "status_code": 400
}

```