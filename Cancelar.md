[Atrás ←](/kubox/wiki/Timbre4.0)

## Cancelar Factura
Una vez que se tienen las facturas timbradas, se pueden cancelar.

###El token en las peticiones
Para realizar cualquier petición es necesario enviar el token en las cabeceras, así que se tiene que agregar el token:

```php

-H "authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg4ODA4ODgsImV4cCI6MTUwODkwMjQ4OCwibmJmIjoxNTA4ODgwODg4LCJqdGkiOiJ4Nkt0Rmg3NTR1YkNmUU5nIiwic3ViIjo4NX0.cGnE7e5Ct0PLgpI0k6MX3MHdYXQU0Drn73sPvSNPVl0" \

```

---

### Petición

    https://development.kubox.mx/v2/timbre/cancelar

| Propiedad          | Descripción                                                                                                                                                                              |
| ----------         | --------------------------------------                                                                                                                                                   |
| `rfc`              | __*String*__ Clave del Registro Federal del Contribuyentes |
| `cer`              | __*String*__ Certificado .pem en base64 |
| `key`              | __*String*__ Key .pem en base64 |
| `uuids`            | __*String*__ UUID del CFDI a cancelar |
| `motivo`           | __*String*__ Clave del motivo de la cancelación ([Listado](#markdown-header-listado-motivo)) |
| `folioSustitucion` | __*String*__ Si la clave del motivo es 01, se indica el UUID con el que se sustituye la cancelación |


#### Listado motivo

- 01 - Comprobantes emitidos con errores con relación.
- 02 - Comprobantes emitidos con errores sin relación.
- 03 - No se llevó a cabo la operación.
- 04 - Operación nominativa relacionada en una factura global.


### Ejemplo de petición

```php

curl --location --request POST 'https://development.kubox.mx/v2/timbre/cancelar' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczovL2RldmVsb3BtZW50Lmt1Ym94Lm14L3YyL2F1dGgvbG9naW4iLCJpYXQiOjE2MTg3ODkxOTYsImV4cCI6MTYxODgxMDc5NiwibmJmIjoxNjE4Nzg5MTk2LCJqdGkiOiJ0S0NMdXo4T2lVeTRnZHpoIiwic3ViIjoxMywicHJ2IjoiODdlMGFmMWVmOWZkMTU4MTJmZGVjOTcxNTNhMTRlMGIwNDc1NDZhYSJ9.DC8co4_4N8JR02caEZcDY-ccQEtvIwQL9Zl-pgq_dYA' \
--data-raw '{
    "rfc": "EKU9003173C9",
    "cer": "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQklqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUFqZEtYaXFZSHppKytZbUViOVg2cQp2cUZXTEN6MVZFZnhvbTJKaGluUFNKeHhjdVpXQmVqazJJNXlDTDVwRG5VYUcyeHBRbE1Ua1YvN1M3SmZHR3ZZCkp1bUtPNFI1emcwUVNBN3FkeGlFaGN3Zi9la2ZTdnpNMkVEbkxIRENLQVF3RVdzbkp5Nzh1eFpUTHp1LzY1VloKN0VnRWNXVVR2Q3MvR1pKTEk5czZYbUtZMlNNbXY5K3ZmcUJxa0pOWEUwWkI2T2ZTYnllRTMyNVA5NGlNbitCLwp5SjR2WndYdlhHRnFOREp5cUcrd3c3Zjc3SFl1YlFQSmpMUVBlZHkycVRjZ21TQXdrVUVKVkJqWUE2bVBmL0JlClpsTDFZSkhITTdDSUJuYjMvYnpFRDBuOTQ0d29pbys0K3JuTVpkZmhjQ1ZwbTc0RFpvbWxFZjlLdUp0cTV1L0oKUlFJREFRQUIKLS0tLS1FTkQgUFVCTElDIEtFWS0tLS0tCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQpNSUlGdXpDQ0E2T2dBd0lCQWdJVU16QXdNREV3TURBd01EQTBNREF3TURJME16UXdEUVlKS29aSWh2Y05BUUVMCkJRQXdnZ0VyTVE4d0RRWURWUVFEREFaQlF5QlZRVlF4TGpBc0JnTlZCQW9NSlZORlVsWkpRMGxQSUVSRklFRkUKVFVsT1NWTlVVa0ZEU1U5T0lGUlNTVUpWVkVGU1NVRXhHakFZQmdOVkJBc01FVk5CVkMxSlJWTWdRWFYwYUc5eQphWFI1TVNnd0pnWUpLb1pJaHZjTkFRa0JGaGx2YzJOaGNpNXRZWEowYVc1bGVrQnpZWFF1WjI5aUxtMTRNUjB3Ckd3WURWUVFKREJRemNtRWdZMlZ5Y21Ga1lTQmtaU0JqWVdScGVqRU9NQXdHQTFVRUVRd0ZNRFl6TnpBeEN6QUoKQmdOVkJBWVRBazFZTVJrd0Z3WURWUVFJREJCRFNWVkVRVVFnUkVVZ1RVVllTVU5QTVJFd0R3WURWUVFIREFoRApUMWxQUVVOQlRqRVJNQThHQTFVRUxSTUlNaTQxTGpRdU5EVXhKVEFqQmdrcWhraUc5dzBCQ1FJVEZuSmxjM0J2CmJuTmhZbXhsT2lCQlEwUk5RUzFUUVZRd0hoY05NVGt3TmpFM01UazBOREUwV2hjTk1qTXdOakUzTVRrME5ERTAKV2pDQjRqRW5NQ1VHQTFVRUF4TWVSVk5EVlVWTVFTQkxSVTFRUlZJZ1ZWSkhRVlJGSUZOQklFUkZJRU5XTVNjdwpKUVlEVlFRcEV4NUZVME5WUlV4QklFdEZUVkJGVWlCVlVrZEJWRVVnVTBFZ1JFVWdRMVl4SnpBbEJnTlZCQW9UCkhrVlRRMVZGVEVFZ1MwVk5VRVZTSUZWU1IwRlVSU0JUUVNCRVJTQkRWakVsTUNNR0ExVUVMUk1jUlV0Vk9UQXcKTXpFM00wTTVJQzhnV0VsUlFqZzVNVEV4TmxGRk5ERWVNQndHQTFVRUJSTVZJQzhnV0VsUlFqZzVNVEV4TmsxSApVazFhVWpBMU1SNHdIQVlEVlFRTEV4VkZjMk4xWld4aElFdGxiWEJsY2lCVmNtZGhkR1V3Z2dFaU1BMEdDU3FHClNJYjNEUUVCQVFVQUE0SUJEd0F3Z2dFS0FvSUJBUUNOMHBlS3BnZk9MNzVpWVJ2MWZxcStvVllzTFBWVVIvR2kKYlltR0tjOUluSEZ5NWxZRjZPVFlqbklJdm1rT2RSb2JiR2xDVXhPUlgvdExzbDhZYTlnbTZZbzdoSG5PRFJCSQpEdXAzR0lTRnpCLzk2UjlLL016WVFPY3NjTUlvQkRBUmF5Y25Mdnk3RmxNdk83L3JsVm5zU0FSeFpSTzhLejhaCmtrc2oyenBlWXBqWkl5YS8zNjkrb0dxUWsxY1RSa0hvNTlKdko0VGZiay8zaUl5ZjRIL0luaTluQmU5Y1lXbzAKTW5Lb2I3RER0L3ZzZGk1dEE4bU10QTk1M0xhcE55Q1pJRENSUVFsVUdOZ0RxWTkvOEY1bVV2VmdrY2N6c0lnRwpkdmY5dk1RUFNmM2pqQ2lLajdqNnVjeGwxK0Z3SldtYnZnTm1pYVVSLzBxNG0ycm03OGxGQWdNQkFBR2pIVEFiCk1Bd0dBMVVkRXdFQi93UUNNQUF3Q3dZRFZSMFBCQVFEQWdiQU1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQ0FRQmMKcGoxVGpUNGppaW5JdWpJZEFsRnpFNmtSd1lKQ25ERzA4elNwNGtTblNoanhBREdFWEgyY2hlaEtNVjBGWTdjNApuakE1ZURHZEEvRzJPQ1RQdkY1cnBlQ1pQNUR3NTA0UlprWURsMnN1Unord2Exc05CVnBibkJKRUswZlFjTjNJCmZ0QndzZ05GZEZoVXRDeXczbHVzMVNTSmJQeGpMSFM2RmNaWjUxWVNlSWZjTlhPQXVUcWRpbXVzYVhxMTVHclMKckNPa002bjJqZmoyc01KWU0ySFhhWEo2ckdURWdZbWhZZHd4V3RpbDZSZlpCK2ZHUS9IOUk5V0xubDRLVFpVUwo2QzkrTkxIaDRGUERoU2sxOWZwUzJTLzU2YXFnRm9HQWtYQVl0OUZ5NUVDYVBjVUxJZkoxREVic1hLeVJkQ3YzCkpZODkrME1Oa09kYURuc2VtUzJvNUdsMDh6STRpWXR0M0w0MGdBWjYwTlBoMzFrVkxuWU5zbXZmTnhZeUtwK0EKZUp0REh5Vzl3N2Z0TTBIb2krQnVSbWNBUVNLRlYzcGs4ajUxbGEranJSQnJBVXY4YmxiUmNRNUJpWlV3SnpIRgpFS0l3VHNSR29SeUV4OTZzTm5CMDNuNkdUd2pJR3o5MlNtTGRObDk1cjlya3ZwKzJtNFM2cTFsUHVYYUZnN0RHCkJyWFdDOGl5cWVXRTJpb2Jkd0lJdVhQVE1WcVFiMTJtMWRBa0pWUk81TmRIblAvTXBxT3ZPZ0xxb1pCTkhHeUIKZzRHcW00c0NKSEN4QTFjOEVsZmEyUlFUQ2swdEF6bGxMNHZPbkkxR0hrR0puNjV4b2tHc2FVNEI0RDM2eGg3ZQpXcmZqNC9wZ1dIbXRvREFZYTh3elN3bzJHVkNaT3MrbXRFZ09RQjkxL2c9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==",
    "key": "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpQcm9jLVR5cGU6IDQsRU5DUllQVEVECkRFSy1JbmZvOiBERVMtRURFMy1DQkMsOEY5QzYxOUQyNkM1M0M0QwoKOE5GRVlSSU9ZT0l3aXVOSDNTVUlkeW93WGtxQmVlWDhydGpCYVlXZWJmcHY4dzdEcFJvZnVaVHRzcEtqTXhQSwp5K1NQUHdkVUF1cVlmc3c2UVk3ZWZ2WVRGZ0pFVUlXb2lJRmhlblQyYmtvektPMExoeVVHNXVuZUJWczVObzhkCjZIdDUzdkpXeEkwK2NzYU5nQTNpR0ZUQTVaT2FyQlR1alg4aTVqMFVBR0haMVNURksvQ1BJUHhPVE45bWV4WDcKblFXMzhERzkva1RBd2d4Z3NGaG9EbFdCeWluWndpeXRYcGNEa1Y5UDEwZDF2RUJkeVhFa0FxV25nK0dNa2ZpOApxanI3d29iTDl0Zm9iOW9pb0ZxbVJjQy9lYmlIa3lTZjFuZUlQNEU1RFhHaGJwcFBkWTNhbkdQbjRLaE12TFF6CjZPZ3BOaVkwKzlja3BIclppMlFpMGNwdFBFRjBUWi9IK2dTK1doamtGQWhta2ppSG5CNEZUSy8zVVdmeVhjazUKWXlSWDU2MDV1Q2ZaZ3Jtd3dOMURwQ3dKR2dLcW1EMStZUmZXWDB3TVZSTVMxWDBOVTBIMzZmZGhheFI5OGpPNQp3eHZMVGVlYTF2NUpUTjk1TjZ0R3YxL1BKYVVUQnU5SnlBQmsyRzc5bnl3R0lMdFloLzYzN3ROeUxPaFA3N2FGCmlTL0JWdkFZR1lZZVN5QW9Ra0dQL1poUjFoNFZ4UmFnL21paHpOOE02aHBEN3Nwa2U5MmJ4d0RhZjlLTVhiUVUKZkRCd2tBeis0SjV4TGh6OEgweUpNQjJQUVNQNkJ1M1dhMm5XcnM4THcyTGMxTFhrN1VpZjNSbkd3cDg1WjdregplcEhuQTlUVnRDR3BIME15Y2Z2Mm5FbTk0S2FRVi9lZjVCb3NyWUl4aUl6WkZFZlZ0Q3dXQ2xueHpEWkt1a3ErCkZMZHVrQlpET1k1ekZpM3h4YStKRS9LbjFlcHdxYk9oMDlkVk1UL1ZzUXk4SHZYc3pIcDl3TnhHTEFmV3RrTlAKS0lhTHYyVWxoTkZHekVWbW03U09YU0FRTmM2WFNsT0NzeThhcU5aOE9uS1ppeDVWVSt3Wngxa0Ryd1NObWZ1bQp4Uk9BZjJwdnNTc2hDL045Y2ljTjhmTFpyS2JBbzJoMERCMDJReWt1bW5obnNPVXVEQ2VUUmdlU1pKNTF3M0VwCnBJdHB1WWwvRThITnRpb3hxRG9wL1pOdHhnd05XNm9XaVU4T29sSEFjbzRxd0xMN2hXQThJTDlROGszcy9kQ1QKSWpNUTJKLzhZSkRlM3dRN2xwbXRvZlNSRUNRTGZvYWpEbkdHOXhkaFJkVUdBRnNwM01PcVBpajF6Y3dXYWVJUwpUckRHUnNGMWI1dG85TXRHWHhUV2p1SVVxT3VETVpVcXJkbjQ3THBxZVljLytvNmw5NldvTkpVaW5zN3ZFN21RCldPcjd2QTFPYndnR1IzM1Y1Rkp2a1N2UUkvNUZVeUNSeXFkUHBJSStZOHFIS1J0cDFtdzVQNlhEakhwa3ByUWoKdEZEeW1FWDV5VWNZSkFMRWs4Wk5uR1lISnc3VHo2SU5rMnl2cVpXdlpBTG5qNDhPSFJEaE9ieGdJeFZITHZIdwpzVjFoQ2lnM1FNOVF0L3p4RGo4ejNKVzlsbElzSXBld2ZIaFRyay9XN1NySVozWThHOXI1dnYxeWFmRFFQdnViCnN0ZUZvYWhQQlNmUFdWenJ6aDNtdnBraW1KMzhrRUNEd3JYR0xROGxsenZOdTV1b0JjNkdQRy80cGJwYVJGSGMKTi9jMUVUZVk5MjZyYWNVWWJyR1FLbDJZUE5FWVNjL1ExT0xzaG4za0VjeFhVWjhHTDRGczFhQVdTYVpIbVBEawpKSDdKRWYxM0dyWlc5WW5ua0hvWUl1WFQ1UngzemhBQ0R3MEV3bVRHNGYrTVprbldNbVQ3WDh0Zml5aTFWOUhvCld6QVJnYzhpTDNqZkJ4TDYvTnFoRHFJOUx3dmdzSEZKbnFONjV1Q0xkdHQzek82RXhFSml3akhiVE42NnhocjAKMFB4MXBUb2diakxhYzRoVXNsVklYQUZ1QkJxYlJlZFlDZS8wSnA2YkpSTGtMWngxWmI5YTFBPT0KLS0tLS1FTkQgUlNBIFBSSVZBVEUgS0VZLS0tLS0K",
    "uuids": "F84C3720-F96C-4736-A630-8E4747C79774",
    "motivo": "01",
    "folioSustitucion": "FF74B7E3-96A9-4883-BD3A-3A2FE44E4A94"
}'

```



### Ejemplo de Respuesta correcta

Retorna un objeto con la información del XML, UUID, fecha y un mensaje.

```json

{
    "msg": {
        "error": false,
        "incidencias": [
            {
                "codigo": 201,
                "mensaje": "Se cancelo correctamente el CFDI sin aceptación."
            }
        ],
        "status": "cancelado"
    },
    "data": {
        "xml": "<Acuse Fecha=\"2018-02-21T18:15:45.355-06:00\" RfcEmisor=\"EKU9003173C9\"><Folios xmlns=\"http://cancelacfd.sat.gob.mx\"><UUID>FF74B7E3-96A9-4883-BD3A-3A2FE44E4A94</UUID><EstatusUUID>201</EstatusUUID></Folios><Signature xmlns=\"http://www.w3.org/2000/09/xmldsig#\" Id=\"SelloSAT\"><SignedInfo><CanonicalizationMethod Algorithm=\"http://www.w3.org/TR/2001/REC-xml-c14n-20010315\" /><SignatureMethod Algorithm=\"http://www.w3.org/2001/04/xmldsig-more#hmac-sha512\" /><Reference URI=\"\"><Transforms><Transform Algorithm=\"http://www.w3.org/TR/1999/REC-xpath-19991116\"><XPath>not(ancestor-or-self::*[local-name()='Signature'])</XPath></Transform></Transforms><DigestMethod Algorithm=\"http://www.w3.org/2001/04/xmlenc#sha512\" /><DigestValue>IjFZq+kXo4me8PSQ1j6P+0ROn6F8cEPJZc/UXsdJ4A2RXl1w56tXN0w0TNyukU7jULdBIqk7QvP0g0J1isahGQ==</DigestValue></Reference></SignedInfo><SignatureValue>a6XW+7vvp+frJLNYzSmHR8lY6qToVV6UxObsB0V6gHt3hlLdUFGTywGyUPMpqCTvLoyaLWYN50tWjmTZptfrlQ==</SignatureValue><KeyInfo><KeyName>00001088888800000093</KeyName><KeyValue><RSAKeyValue><Modulus>yxMvUucuS+s3aeWTFZvJrrFWIdes7kIDJmO7DA5DP+ZTapofNt37fgeIHlTUdAVvd/fDKhfiwNSh+vbrNbD58X3UEdQor3ngb6zpjrDjgYsedckPLv6fro4DO0NXLCdALFqhN8ARyX77kYBnvIj1fOSVp401Vc3urLUtiEm16Kle3tOyWhfjgFzdK3oAIXF8oeei/GburWbJnpP+NeGaHVE5bkxLCBp5757nKVonXwzpfpEGuBp204NGkI2/jyA2EH8wyRN4yUvzjT7IJYrHng23klRDlJoRYwa98QQPdQSTpcrlNu8nLhpQdI/zMTLoNF2NiBCkQNuAMacKhnvlVw==</Modulus><Exponent>AQAB</Exponent></RSAKeyValue></KeyValue></KeyInfo></Signature></Acuse>",
        "fecha": "2021-04-18T18:43:58",
        "rfc_emisor": "EKU9003173C9",
        "uuid": "FF74B7E3-96A9-4883-BD3A-3A2FE44E4A94",
        "status_uuid": 201,
        "estado_cfdi": "Cancelado"
    }
}

```

Otra respuesta correcta:

```
#!json

{
    "msg": {
        "error": false,
        "incidencias": [
            {
                "codigo": 201,
                "mensaje": "Se envió la solicitud de cancelación al SAT, se encuentra en proceso de aceptación por el receptor."
            }
        ],
        "status": "cancelado"
    },
    "data": {
        "xml": "<Acuse Fecha=\"2018-02-21T18:15:45.355-06:00\" RfcEmisor=\"EKU9003173C9\"><Folios xmlns=\"http://cancelacfd.sat.gob.mx\"><UUID>FF74B7E3-96A9-4883-BD3A-3A2FE44E4A94</UUID><EstatusUUID>201</EstatusUUID></Folios><Signature xmlns=\"http://www.w3.org/2000/09/xmldsig#\" Id=\"SelloSAT\"><SignedInfo><CanonicalizationMethod Algorithm=\"http://www.w3.org/TR/2001/REC-xml-c14n-20010315\" /><SignatureMethod Algorithm=\"http://www.w3.org/2001/04/xmldsig-more#hmac-sha512\" /><Reference URI=\"\"><Transforms><Transform Algorithm=\"http://www.w3.org/TR/1999/REC-xpath-19991116\"><XPath>not(ancestor-or-self::*[local-name()='Signature'])</XPath></Transform></Transforms><DigestMethod Algorithm=\"http://www.w3.org/2001/04/xmlenc#sha512\" /><DigestValue>IjFZq+kXo4me8PSQ1j6P+0ROn6F8cEPJZc/UXsdJ4A2RXl1w56tXN0w0TNyukU7jULdBIqk7QvP0g0J1isahGQ==</DigestValue></Reference></SignedInfo><SignatureValue>a6XW+7vvp+frJLNYzSmHR8lY6qToVV6UxObsB0V6gHt3hlLdUFGTywGyUPMpqCTvLoyaLWYN50tWjmTZptfrlQ==</SignatureValue><KeyInfo><KeyName>00001088888800000093</KeyName><KeyValue><RSAKeyValue><Modulus>yxMvUucuS+s3aeWTFZvJrrFWIdes7kIDJmO7DA5DP+ZTapofNt37fgeIHlTUdAVvd/fDKhfiwNSh+vbrNbD58X3UEdQor3ngb6zpjrDjgYsedckPLv6fro4DO0NXLCdALFqhN8ARyX77kYBnvIj1fOSVp401Vc3urLUtiEm16Kle3tOyWhfjgFzdK3oAIXF8oeei/GburWbJnpP+NeGaHVE5bkxLCBp5757nKVonXwzpfpEGuBp204NGkI2/jyA2EH8wyRN4yUvzjT7IJYrHng23klRDlJoRYwa98QQPdQSTpcrlNu8nLhpQdI/zMTLoNF2NiBCkQNuAMacKhnvlVw==</Modulus><Exponent>AQAB</Exponent></RSAKeyValue></KeyValue></KeyInfo></Signature></Acuse>",
        "fecha": "2021-04-18T18:47:31",
        "rfc_emisor": "EKU9003173C9",
        "uuid": "FF74B7E3-96A9-4883-BD3A-3A2FE44E4A94",
        "status_uuid": 201,
        "estado_cfdi": "En proceso"
    }
}

```

### El proceso de cancelación funciona de la siguiente manera:

![cancelacion.jpg](https://bitbucket.org/repo/pqRj4L/images/2594533377-cancelacion.jpg)

* Si el campo estado_cfdi es Cancelado, el CFDI se cancelo sin autorización.
* Si el campo estado_cfdi es En proceso, el CFDI se encuentra en el buzón tributario en espera de la aceptación o rechazo del receptor.
* Si un CFDI no es cancelable estado_cfdi también es En proceso ya que la solicitud es enviada.

En los dos puntos anteriores se tiene que usar el servicio timbre/get para verificar el estado del CFDI.

---

### Objeto Error
Kubox responde objetos JSON en caso de error, los errores son muy descriptivos, sin embargo, si tienes una duda puedes contactarnos al correo `soporte@kubox.mx`.

| Propiedad     | Descripción                             |
| ----------    |--------------------------------------   |
| `error`       | __*Bool*__   true                       |
| `incidencias` | __*Object*__ El motivo del error        |
| `status`      | __*String*__ Error                      |


#### Ejemplo de respuesta con error

```json
{
    "msg": {
        "error": true,
        "incidencias": [
            {
                "codigo": "error",
                "mensaje": "Ocurrio un error al cancelar el CFDI. UUID: BD20A82F-91DB-4CFC-85C6-3D1FE4A0ED97 No Encontrado"
            }
        ],
        "status": "error"
    },
    "data": ""
}
```