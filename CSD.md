[Atrás ←](/kubox/Timbre4.0)

## Preparación del Certificado de Sello Digital (CSD)

Para poder usar los servicios de timbrado y cancelación de CFDI, es necesario contar con un certificado de sello digital, el cual se tramita ante el SAT, para efectos de pruebas descargue el siguiente CSD; Nota" todos los CFDI generados en el ambiente de pruebas y con el certificado proporcionado no son reales.

El nombre de la empresa es ESCUELA KEMPER URGATE SA DE CV y el RFC EKU9003173C9

* [Archivo .cer](https://mega.nz/file/cDZlVRxK#VPZGNamKODXcGL813poAK30mbmuRjIGDPJNYGFcFzQw)
* [Archivo .key](https://mega.nz/file/BDIzmY4A#aUhQ3xGkVHvvubLSkc3MrXEoxyKFlHRsvI6yRFQWTW4)
* Password archivo .key: "12345678a" (Sin comillas)

Las tres cosas anteriores son necesarias para realizar los pasos siguientes ya sea para el ambiente de pruebas o producción, en este segundo serian los certificados reales de la empresa.

También es necesario contar con openssl para ejecutar los siguientes comando:

**Archivo .cer**

```
#!php
openssl x509 -inform DER -outform PEM -in CSD_EKU9003173C9.cer -pubkey -out CSD_EKU9003173C9.cer.pem

```
El archivo resultante CSD_EKU9003173C9.cer.pem es el que se usara para hacer las peticiones a la API.

**Archivo .key**

```
#!php
openssl pkcs8 -inform DER -in CSD_EKU9003173C9.key -out aux_CSD_EKU9003173C9.key.pem -passin pass:12345678a
openssl rsa -in aux_CSD_EKU9003173C9.key.pem -des3 -out CSD_EKU9003173C9.key.pem -passout pass:gamaL1!l

```
El archivo resultante CSD_EKU9003173C9.key.pem es el que se usara para hacer las peticiones a la API, cabe señalar que para el ambiente de pruebas se tiene que codificar el archivo .key.pem con el password **gamaL1!l** y para producción con el password **F4ctur4rt!**, de lo contrario no se podrán desencriptar los archivos y realizar el timbrado.

----

En los servicios de timbrado y cancelación se solicitara como parámetros el cer y key, la forma en que se tienen que llenar esos parámetros es obteniendo el contenido (texto) de los archivos generados anteriormente y convirtiéndolo en base64.