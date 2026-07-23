[Atrás ←](/kubox/wiki/Timbre4.0)

## Nomina
El timbrado permite enviar los datos del emisor y los trabajadores, responde  un objeto JSON con la información de los timbres, siempre debe llevar el token en las cabeceras de la petición.

### Token en las peticiones
Para realizar cualquier petición es necesario enviar el token en las cabeceras, así que se tiene que agregar el token:

```php

-H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg3NzM2MTAsImV4cCI6MTUwODc5NTIxMCwibmJmIjoxNTA4NzczNjEwLCJqdGkiOiJIcUZPbDlWSWZSYk53N3ZqIiwic3ViIjo4NX0.GEqizwFutuibe_RYUXh3i0sOmK-PDRKK88tJBSTyJr4' \

```
### Lista de RFC para utilizarse como RECEPTORES en CFDI 4.0
RFCs que acepta el sistema en el ambiente de pruebas para el timbrado el nominas:

| RFC           | Nombre/Razón social             | Domicilio fiscal |
| ------        | -------------------             | ---------------- |
| MASO451221PM4 | MARIA OLIVIA MARTINEZ SAGAZ     | 80290 |
| AABF800614HI0 | FELIX MANUEL ANDRADE BALLADO    | 86400 |
| CUSC850516316 | CESAR OSBALDO CRUZ SOLORZANO    | 45638 |


### Catalogos de nomina
[catNomina.xls](https://mega.nz/file/4eAjAIIS#RsHl836hWI_DeeKfuqXjtTXhpLhB6iCSY9oExVO0d9o)

----------

### Timbrado CFDI Nomina
El timbrado requiere que se envíen los datos del emisor y los conceptos del complemento de nomina.
### Petición

    https://development.kubox.mx/v2/timbre/nomina40

| Propiedad                 | Descripción                                   |
| ----------                |--------------------------------------         |
| `emisor`                  | __*Object*__ ([ver Obj Emisor](#markdown-header-obj-emisor))                 |
| `fechaInicialPago`        | __*Date*__ Fecha de inicio del periodo que se esta pagando en la nomina                 |
| `fechaFinalPago`          | __*Date*__ Fecha de fin del periodo que se esta pagando en la nomina                 |
| `fechaPago`               | __*Date*__ Fecha en el que se realizo el pago de la nomina                 |
| `noCertificado`           | __*String*__ Es el número que identifica al certificado de sello digital del emisor, el cual lo incluye en el comprobante fiscal el sistema que utiliza el contribuyente para la emisión              |
| `periodicidadPago`        | __*String*__ Código de periodicidad de pago (c_PeriodicidadPago)                 |
| `registroPatronal`        | __*String*__ Numero de registro patronal del IMSS                 |
| `tipoNomina`              | __*String*__ Código del tipo de nomina a timbrar (c_TipoNomina)
| `origenRecurso`           | __*String*__ Clave para indicar el origen de los recursos con los que se paga la nomina (c_OrigenRecurso)                 |
| `data`                    | __*Array:Trabajador*__ ([Ver Obj Trabajador](#markdown-header-obj-trabajador))                                        |

---

### **Obj Emisor**

| Propiedad         | Descripción                             |
| ----------        |--------------------------------------   |
| `nombreFiscal`    | __*String*__ Se puede registrar el nombre, denominación o razón social del emisor del comprobante                     |
| `rfc`             | __*String*__ Clave del Registro Federal de Contribuyentes                                                |
| `regimenFiscal`   | __*String*__ clave del régimen fiscal del contribuyente (c_RegimenFiscal)                                              |
| `curp`            | __*String*__ (Opcional) CURP si es una persona física                      |
| `cp`              | __*String*__ Código Postal              |
| `cer`             | __*String*__ Certificado .pem en base64 |
| `key`             | __*String*__ Key .pem en base64         |

---

### **Obj Trabajador**

| Propiedad                       | Descripción                             |
| ------------------------------  |--------------------------------------   |
| `serie`                         | __*String*__ Serie del CFDI|
| `folio`                         | __*Number*__ Folio del CFDI|
| `noEmpleado`                    | __*String*__ Identificador interno del trabajador|
| `nombre`                        | __*String*__ Nombre completo del trabajador|
| `rfc`                           | __*String*__ RFC del trabajador|
| `curp`                          | __*String*__ CURP del trabajador|
| `cp`                            | __*String*__ Código Postal del domicilio fiscal del trabajador|
| `claveEntFed`                   | __*String*__ Código del estado del trabajador (c_Estado)|
| `departamento`                  | __*String*__ Departamento en el que se desempeña el trabajador|
| `puesto`                        | __*String*__ Puesto que desempeña el trabajador|
| `sdi`                           | __*Number*__ Salario diario integrado del trabajador|
| `diasPago`                      | __*Number*__ Días pagados del trabajador|
| `ex_FechaInicioRelLaboral`      | __*Date*__ Fecha en que el trabajador inicio las labores en la empresa|
| `ex_RiesgoPuesto`               | __*String*__ Código del riesgo del puesto (c_RiesgoPuesto)    |
| `ex_Sindicalizado`              | __*String*__ Indica si el trabajador tiene sindicato (Sí|No)|
| `ex_TipoJornada`                | __*String*__ Código del la jornada en la que el trabajador se desempeña (c_TipoJornada)    |
| `seguro_social`                 | __*String*__ Numero que el IMSS asigna al trabajador (sin - ni espacios)|
| `tipoContrato`                  | __*String*__ Código del tipo del contrato que tiene el trabajador (c_TipoContrato)|
| `tipoRegimen`                   | __*String*__ Código del régimen en el que se encuentra el trabajador (c_TipoRegimen)|
| `pe_sueldo_clave`               | __*String*__ Cuenta contable de la percepción de nomina (Ej. 43200006)|
| `pe_sueldo_concepto`            | __*String*__ Concepto de la percepción (Ej. Sueldos, Salarios  Rayas y Jornales)|
| `pe_sueldo_excento`             | __*Number*__ El importe exento de la percepción (Ej. 1200.00)|
| `pe_sueldo_gravado`             | __*Number*__ El importe gravado de la percepción (Ej. 1950.00)|
| `de_otros_clave`                | __*String*__ Cuenta contable de la deducción de nomina (Ej. 50000300)|
| `de_otros_concepto`             | __*String*__ Concepto de la deducción (Ej. ISR)|
| `de_otros_importe`              | __*Number*__ El importe de la deducción (Ej. 450.00)|
| `top_subsidio_empleo_clave`     | __*String*__ Cuenta contable de otros pagos (Ej. 11700001)|
| `top_subsidio_empleo_concepto`  | __*String*__ Concepto de otros pagos (Ej. Subsidio para el empleo)|
| `top_subsidio_empleo_importe`   | __*Number*__ El importe de otros pagos (Ej. 500.00)|
| `top_subsidio_empleo_causado`   | __*Number*__ El importe del subsidio causado de acuerdo a las tablas de subsidio (Ej. 900.00), solo aplica para "Subsidio al empleo"|


---

### Lista completa de Percepciones, Deducciones y Otros pagos

Si necesitas agregar más percepciones, deducciones y/o otros pagos, a continuación están las listas completas para agregarlas a la petición de timbrado.

#### Percepciones

| Percepción                              | Campos de la percepción           |
| --------------------------------------- | --------------------------------- |
| pe_sueldo_                              | clave, concepto, excento, gravado |
| pe_comisiones_                          | clave, concepto, excento, gravado |
| pe_ptu_                                 | clave, concepto, excento, gravado |
| pe_fondo_ahorro_                        | clave, concepto, excento, gravado |
| pe_caja_ahorro_                         | clave, concepto, excento, gravado |
| pe_contribuciones_trabajador_           | clave, concepto, excento, gravado |
| pe_premio_puntualidad_                  | clave, concepto, excento, gravado |
| pe_prima_seguro_vida_                   | clave, concepto, excento, gravado |
| pe_seguro_gastos_medicos_               | clave, concepto, excento, gravado |
| pe_cuotas_sindicales_                   | clave, concepto, excento, gravado |
| pe_subsidio_incapacidad_                | clave, concepto, excento, gravado |
| pe_horas_extras_                        | clave, concepto, excento, gravado |
| pe_prima_dominical_                     | clave, concepto, excento, gravado |
| pe_prima_vacacional_                    | clave, concepto, excento, gravado |
| pe_prima_antiguedad_                    | clave, concepto, excento, gravado, ingresoAcumulable, ingresoNoAcumulable, numAñosServicio, ultimoSueldoMensOrd |
| pe_pagos_separacion_                    | clave, concepto, excento, gravado |
| pe_seguro_retiro_                       | clave, concepto, excento, gravado |
| pe_indemnizacion_                       | clave, concepto, excento, gravado |
| pe_vales_despensa_                      | clave, concepto, excento, gravado |
| pe_vales_restaurante_                   | clave, concepto, excento, gravado |
| pe_vales_gasolina_                      | clave, concepto, excento, gravado |
| pe_vales_ropa_                          | clave, concepto, excento, gravado |
| pe_ayuda_renta_                         | clave, concepto, excento, gravado |
| pe_ayuda_anteojos_                      | clave, concepto, excento, gravado |
| pe_ayuda_transporte_                    | clave, concepto, excento, gravado |
| pe_ayuda_gastos_funeral_                | clave, concepto, excento, gravado |
| pe_otros_ingresos_salarios_             | clave, concepto, excento, gravado |
| pe_jubilaciones_pensiones_              | clave, concepto, excento, gravado, ingresoAcumulable, ingresoNoAcumulable |
| pe_acciones_titulos_                    | clave, concepto, excento, gravado |
| pe_alimentacion_                        | clave, concepto, excento, gravado |
| pe_habitacion_                          | clave, concepto, excento, gravado |
| pe_p_asistencia_                        | clave, concepto, excento, gravado |
| pe_cuota_seguro_social_                 | clave, concepto, excento, gravado |
| pe_viaticos_                            | clave, concepto, excento, gravado |
| pe_sueldo_7d_                           | clave, concepto, excento, gravado |
| pe_aguinaldo_                           | clave, concepto, excento, gravado |
| pe_reembolso_gastos_medicos_            | clave, concepto, excento, gravado |
| pe_becas_trabajadores_hijos_            | clave, concepto, excento, gravado |
| pe_reembolso_funeral_                   | clave, concepto, excento, gravado |
| pe_ayuda_articulos_escolares_           | clave, concepto, excento, gravado |
| pe_asimilados_salarios_                 | clave, concepto, excento, gravado |
| pe_retiro_parcialidades_                | clave, concepto, excento, gravado, ingresoAcumulable, ingresoNoAcumulable, montoDiario |
| pe_pagos_gratificaciones_ext_parc_      | clave, concepto, excento, gravado |
| pe_pagos_ext_jubilacion_parc_           | clave, concepto, excento, gravado |
| pe_pagos_ext_jubilacion_exhi_           | clave, concepto, excento, gravado |
| pe_dias_descanso_laborado_              | clave, concepto, excento, gravado |
| pe_dias_descanso_obl_laborado_          | clave, concepto, excento, gravado |
| pe_prevision_social_                    | clave, concepto, excento, gravado |

#### Deducciones

| Deducción                                        | Campos de la deducción   |
| ---------------------------------------          | ----------------------   |
| de_anticipo_salarios_                            | clave, concepto, importe |
| de_pagos_excesos_trabajador_                     | clave, concepto, importe |
| de_errores_                                      | clave, concepto, importe |
| de_perdidas_                                     | clave, concepto, importe |
| de_averias_                                      | clave, concepto, importe |
| de_a_ptu_gravado_                                | clave, concepto, importe |
| de_a_comisiones_gravado_                         | clave, concepto, importe |
| de_isr_                                          | clave, concepto, importe |
| de_otros_                                        | clave, concepto, importe |
| de_aportaciones_fondo_vivienda_                  | clave, concepto, importe |
| de_descuento_incapacidad_                        | clave, concepto, importe |
| de_pencion_alimenticia_                          | clave, concepto, importe |
| de_renta_                                        | clave, concepto, importe |
| de_credito_vivienda_                             | clave, concepto, importe |
| de_cuotas_sindicales_                            | clave, concepto, importe |
| de_ausencia_                                     | clave, concepto, importe |
| de_cuotas_obrero_patronales_                     | clave, concepto, importe |
| de_seguro_social_                                | clave, concepto, importe |
| de_infonavit_                                    | clave, concepto, importe |
| de_infonacot_                                    | clave, concepto, importe |
| de_adquisicion_articulos_                        | clave, concepto, importe |
| de_impuestos_locales_                            | clave, concepto, importe |
| de_aportaciones_voluntarias_                     | clave, concepto, importe |
| de_a_aguinaldo_exento_                           | clave, concepto, importe |
| de_a_aguinaldo_gravado_                          | clave, concepto, importe |
| de_a_gastos_medicos_exento_                      | clave, concepto, importe |
| de_a_fondo_ahorro_exento_                        | clave, concepto, importe |
| de_a_caja_ahorro_exento_                         | clave, concepto, importe |
| de_a_premios_puntualidad_gravado_                | clave, concepto, importe |
| de_a_prima_seguro_vida_exento_                   | clave, concepto, importe |
| de_a_seguro_gastos_medicos_exento_               | clave, concepto, importe |
| de_a_cuotas_sindicales_exento_                   | clave, concepto, importe |
| de_a_subsidios_incapacidad_exento_               | clave, concepto, importe |
| de_a_becas_exento_                               | clave, concepto, importe |
| de_a_horas_extra_exento_                         | clave, concepto, importe |
| de_a_horas_extra_gravado_                        | clave, concepto, importe |
| de_a_prima_dominical_exento_                     | clave, concepto, importe |
| de_a_prima_dominical_gravado_                    | clave, concepto, importe |
| de_a_prima_vacacional_exento_                    | clave, concepto, importe |
| de_a_prima_antiguedad_exento_                    | clave, concepto, importe |
| de_a_prima_antiguedad_gravado_                   | clave, concepto, importe |
| de_a_pagos_separacion_exento_                    | clave, concepto, importe |
| de_a_pagos_separacion_gravado_                   | clave, concepto, importe |
| de_a_seguro_retiro_exento_                       | clave, concepto, importe |
| de_a_indemnizaciones_exento_                     | clave, concepto, importe |
| de_a_indemnizaciones_gravado_                    | clave, concepto, importe |
| de_a_reembolso_funeral_exento_                   | clave, concepto, importe |
| de_a_vales_despensa_exento_                      | clave, concepto, importe |
| de_a_vales_restaurante_exento_                   | clave, concepto, importe |
| de_a_vales_gasolina_exento_                      | clave, concepto, importe |
| de_a_vales_ropa_exento_                          | clave, concepto, importe |
| de_a_ayuda_renta_exento_                         | clave, concepto, importe |
| de_a_ayuda_articulos_escolares_exento_           | clave, concepto, importe |
| de_a_ayuda_anteojos_exento_                      | clave, concepto, importe |
| de_a_ayuda_transporte_exento_                    | clave, concepto, importe |
| de_a_otros_ingresos_salarios_exento_             | clave, concepto, importe |
| de_a_otros_ingresos_salarios_gravado_            | clave, concepto, importe |
| de_a_jubilaciones_pensiones_exento_              | clave, concepto, importe |
| de_a_jubilaciones_pensiones_gravado_             | clave, concepto, importe |
| de_a_pagos_separacion_acumulable_                | clave, concepto, importe |
| de_a_pagos_separacion_no_acumulable_             | clave, concepto, importe |
| de_a_jubilaciones_pensiones_par_gravado_         | clave, concepto, importe |
| de_a_subsidio_empleo_                            | clave, concepto, importe |
| de_a_ingresos_acciones_titulos_exento_           | clave, concepto, importe |
| de_a_ingresos_acciones_titulos_gravado_          | clave, concepto, importe |
| de_a_alimentacion_exento_                        | clave, concepto, importe |
| de_a_alimentacion_gravado_                       | clave, concepto, importe |
| de_a_habitacion_exento_                          | clave, concepto, importe |
| de_a_habitacion_gravado_                         | clave, concepto, importe |
| de_a_premios_asistencia_                         | clave, concepto, importe |
| de_a_viaticos_gravados_                          | clave, concepto, importe |
| de_a_viaticos_                                   | clave, concepto, importe |
| de_a_fondo_ahorro_gravado_                       | clave, concepto, importe |
| de_a_caja_ahorro_gravado_                        | clave, concepto, importe |
| de_a_prima_seguro_vida_gravado_                  | clave, concepto, importe |
| de_a_seguro_gastos_medicos_gravado_              | clave, concepto, importe |
| de_a_subsidios_incapacidad_gravado_              | clave, concepto, importe |
| de_a_becas_gravado_                              | clave, concepto, importe |
| de_a_seguro_retiro_gravado_                      | clave, concepto, importe |
| de_a_vales_despensa_gravado_                     | clave, concepto, importe |
| de_a_vales_restaurante_gravado_                  | clave, concepto, importe |
| de_a_vales_gasolina_gravado_                     | clave, concepto, importe |
| de_a_vales_ropa_gravado_                         | clave, concepto, importe |
| de_a_ayuda_renta_gravado_                        | clave, concepto, importe |
| de_a_ayuda_articulos_escolares_gravado_          | clave, concepto, importe |
| de_a_ayuda_anteojos_gravado_                     | clave, concepto, importe |
| de_a_ayuda_transporte_gravado_                   | clave, concepto, importe |
| de_a_ayuda_gastos_funeral_gravado_               | clave, concepto, importe |
| de_a_ingresos_asimilados_salarios_gravados_      | clave, concepto, importe |
| de_a_viaticos_exentos_                           | clave, concepto, importe |
| de_isr_retenido_ejercicio_anterior_              | clave, concepto, importe |
| de_a_ptu_exento_                                 | clave, concepto, importe |
| de_cesantia_vejez_                               | clave, concepto, importe |
| de_cuotas_constitucion_cajas_ahorro_             | clave, concepto, importe |
| de_a_contribuciones_cargo_trabajador_exento_     | clave, concepto, importe |
| de_a_prima_vacacional_gravado_                   | clave, concepto, importe |
| de_a_cuotas_seguridad_social_exento_             | clave, concepto, importe |
| de_a_ayuda_gastos_funeral_exento_                | clave, concepto, importe |
| de_a_jubilaciones_pensiones_par_exento_          | clave, concepto, importe |
| de_a_pagos_gratificaciones_ext_parc_gravados_    | clave, concepto, importe |
| de_a_pagos_ext_jubilacion_parc_gravados_         | clave, concepto, importe |
| de_a_pagos_ext_jubilacion_parc_exentos_          | clave, concepto, importe |
| de_a_pagos_ext_jubilacion_exhi_gravados_         | clave, concepto, importe |
| de_a_pagos_ext_jubilacion_exhi_exentos_          | clave, concepto, importe |
| de_ajuste_subsidio_causado_                      | clave, concepto, importe |
| de_a_otros_pagos_no_sueldos_salarios_asimilados_ | clave, concepto, importe |
| de_a_ingresos_sueldos_salarios_gravados_         | clave, concepto, importe |
| de_a_dias_descanso_laborados_gravado_            | clave, concepto, importe |
| de_a_dias_descanso_laborados_exento_             | clave, concepto, importe |
| de_a_dias_descanso_obl_laborados_gravado_        | clave, concepto, importe |
| de_a_dias_descanso_obl_laborados_exento_         | clave, concepto, importe |

#### Otros pagos

| Otro pago                               | Campos otros pagos       |
| --------------------------------------- | ------------------------ |
| top_reintegro_isr_                      | clave, concepto, importe |
| top_subsidio_empleo_                    | clave, concepto, importe, causado |
| top_viaticos_                           | clave, concepto, importe |
| top_saldo_favor_compensacion_           | clave, concepto, importe, año, importe, remanenteSalFav, saldoAFavor |
| top_reintegro_isr_ret_ejer_ant_         | clave, concepto, importe |
| top_otros_pagos_                        | clave, concepto, importe |
| top_alimentos_bienes_                   | clave, concepto, importe |
| top_isr_ajustado_subsidio_              | clave, concepto, importe |
| top_subsidio_efectivamente_entregado_   | clave, concepto, importe |

---

### Ejemplo 1 de petición

```php
  curl https://development.kubox.mx/v2/timbre/nomina40 \
     -H "Content-type: application/json" \
     -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg3NzM2MTAsImV4cCI6MTUwODc5NTIxMCwibmJmIjoxNTA4NzczNjEwLCJqdGkiOiJIcUZPbDlWSWZSYk53N3ZqIiwic3ViIjo4NX0.GEqizwFutuibe_RYUXh3i0sOmK-PDRKK88tJBSTyJr4' \
     -X POST -d '{
  "data": [
    {
      "serie": "702",
      "folio": "201802",
      "noEmpleado": "702",
      "nombre": "MARIA OLIVIA MARTINEZ SAGAZ",
      "rfc": "MASO451221PM4",
      "curp": "MELH450218MSLNPL03",
      "cp": "80290",
      "claveEntFed": "COL",
      "departamento": "SOLDADOR",
      "sdi": 180,
      "diasPago": 7,
      "ex_FechaInicioRelLaboral": "2022-01-01",
      "ex_RiesgoPuesto": "1",
      "ex_TipoJornada": "01",
      "seguro_social": "1234567",
      "tipoContrato": "01",
      "tipoRegimen": "02",

      "pe_sueldo_clave": "43200006",
      "pe_sueldo_concepto": "Sueldo",
      "pe_sueldo_gravado": 100,
      "pe_sueldo_excento": 100,
      "pe_fondo_ahorro_clave": "43200004",
      "pe_fondo_ahorro_concepto": "fondo ahorro",
      "pe_fondo_ahorro_gravado": 100,
      "pe_fondo_ahorro_excento": 100,
      "pe_premio_puntualidad_clave": "43200009",
      "pe_premio_puntualidad_concepto": "fondo ahorro",
      "pe_premio_puntualidad_gravado": 110,
      "pe_premio_puntualidad_excento": 100,

      "de_seguro_social_clave": "50000300",
      "de_seguro_social_concepto": "imss",
      "de_seguro_social_importe": 100,
      "de_isr_clave": "50000302",
      "de_isr_concepto": "isr",
      "de_isr_importe": 100,
      "de_otros_clave": "50000305",
      "de_otros_concepto": "otros",
      "de_otros_importe": 100,

      "top_subsidio_empleo_clave": "11700001",
      "top_subsidio_empleo_concepto": "Subsidio para el empleo",
      "top_subsidio_empleo_importe": 100,
      "top_subsidio_empleo_causado": 120,

      "total": 410
    }
  ],
  "emisor": {
    "nombreFiscal": "ESCUELA KEMPER URGATE SA DE CV",
    "rfc": "EKU9003173C9",
    "regimenFiscal": "601",
    "curp": "",
    "cp": "20928",
    "cer": "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQklqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUFqZEtYaXFZSHppKytZbUViOVg2cQp2cUZXTEN6MVZFZnhvbTJKaGluUFNKeHhjdVpXQmVqazJJNXlDTDVwRG5VYUcyeHBRbE1Ua1YvN1M3SmZHR3ZZCkp1bUtPNFI1emcwUVNBN3FkeGlFaGN3Zi9la2ZTdnpNMkVEbkxIRENLQVF3RVdzbkp5Nzh1eFpUTHp1LzY1VloKN0VnRWNXVVR2Q3MvR1pKTEk5czZYbUtZMlNNbXY5K3ZmcUJxa0pOWEUwWkI2T2ZTYnllRTMyNVA5NGlNbitCLwp5SjR2WndYdlhHRnFOREp5cUcrd3c3Zjc3SFl1YlFQSmpMUVBlZHkycVRjZ21TQXdrVUVKVkJqWUE2bVBmL0JlClpsTDFZSkhITTdDSUJuYjMvYnpFRDBuOTQ0d29pbys0K3JuTVpkZmhjQ1ZwbTc0RFpvbWxFZjlLdUp0cTV1L0oKUlFJREFRQUIKLS0tLS1FTkQgUFVCTElDIEtFWS0tLS0tCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQpNSUlGdXpDQ0E2T2dBd0lCQWdJVU16QXdNREV3TURBd01EQTBNREF3TURJME16UXdEUVlKS29aSWh2Y05BUUVMCkJRQXdnZ0VyTVE4d0RRWURWUVFEREFaQlF5QlZRVlF4TGpBc0JnTlZCQW9NSlZORlVsWkpRMGxQSUVSRklFRkUKVFVsT1NWTlVVa0ZEU1U5T0lGUlNTVUpWVkVGU1NVRXhHakFZQmdOVkJBc01FVk5CVkMxSlJWTWdRWFYwYUc5eQphWFI1TVNnd0pnWUpLb1pJaHZjTkFRa0JGaGx2YzJOaGNpNXRZWEowYVc1bGVrQnpZWFF1WjI5aUxtMTRNUjB3Ckd3WURWUVFKREJRemNtRWdZMlZ5Y21Ga1lTQmtaU0JqWVdScGVqRU9NQXdHQTFVRUVRd0ZNRFl6TnpBeEN6QUoKQmdOVkJBWVRBazFZTVJrd0Z3WURWUVFJREJCRFNWVkVRVVFnUkVVZ1RVVllTVU5QTVJFd0R3WURWUVFIREFoRApUMWxQUVVOQlRqRVJNQThHQTFVRUxSTUlNaTQxTGpRdU5EVXhKVEFqQmdrcWhraUc5dzBCQ1FJVEZuSmxjM0J2CmJuTmhZbXhsT2lCQlEwUk5RUzFUUVZRd0hoY05NVGt3TmpFM01UazBOREUwV2hjTk1qTXdOakUzTVRrME5ERTAKV2pDQjRqRW5NQ1VHQTFVRUF4TWVSVk5EVlVWTVFTQkxSVTFRUlZJZ1ZWSkhRVlJGSUZOQklFUkZJRU5XTVNjdwpKUVlEVlFRcEV4NUZVME5WUlV4QklFdEZUVkJGVWlCVlVrZEJWRVVnVTBFZ1JFVWdRMVl4SnpBbEJnTlZCQW9UCkhrVlRRMVZGVEVFZ1MwVk5VRVZTSUZWU1IwRlVSU0JUUVNCRVJTQkRWakVsTUNNR0ExVUVMUk1jUlV0Vk9UQXcKTXpFM00wTTVJQzhnV0VsUlFqZzVNVEV4TmxGRk5ERWVNQndHQTFVRUJSTVZJQzhnV0VsUlFqZzVNVEV4TmsxSApVazFhVWpBMU1SNHdIQVlEVlFRTEV4VkZjMk4xWld4aElFdGxiWEJsY2lCVmNtZGhkR1V3Z2dFaU1BMEdDU3FHClNJYjNEUUVCQVFVQUE0SUJEd0F3Z2dFS0FvSUJBUUNOMHBlS3BnZk9MNzVpWVJ2MWZxcStvVllzTFBWVVIvR2kKYlltR0tjOUluSEZ5NWxZRjZPVFlqbklJdm1rT2RSb2JiR2xDVXhPUlgvdExzbDhZYTlnbTZZbzdoSG5PRFJCSQpEdXAzR0lTRnpCLzk2UjlLL016WVFPY3NjTUlvQkRBUmF5Y25Mdnk3RmxNdk83L3JsVm5zU0FSeFpSTzhLejhaCmtrc2oyenBlWXBqWkl5YS8zNjkrb0dxUWsxY1RSa0hvNTlKdko0VGZiay8zaUl5ZjRIL0luaTluQmU5Y1lXbzAKTW5Lb2I3RER0L3ZzZGk1dEE4bU10QTk1M0xhcE55Q1pJRENSUVFsVUdOZ0RxWTkvOEY1bVV2VmdrY2N6c0lnRwpkdmY5dk1RUFNmM2pqQ2lLajdqNnVjeGwxK0Z3SldtYnZnTm1pYVVSLzBxNG0ycm03OGxGQWdNQkFBR2pIVEFiCk1Bd0dBMVVkRXdFQi93UUNNQUF3Q3dZRFZSMFBCQVFEQWdiQU1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQ0FRQmMKcGoxVGpUNGppaW5JdWpJZEFsRnpFNmtSd1lKQ25ERzA4elNwNGtTblNoanhBREdFWEgyY2hlaEtNVjBGWTdjNApuakE1ZURHZEEvRzJPQ1RQdkY1cnBlQ1pQNUR3NTA0UlprWURsMnN1Unord2Exc05CVnBibkJKRUswZlFjTjNJCmZ0QndzZ05GZEZoVXRDeXczbHVzMVNTSmJQeGpMSFM2RmNaWjUxWVNlSWZjTlhPQXVUcWRpbXVzYVhxMTVHclMKckNPa002bjJqZmoyc01KWU0ySFhhWEo2ckdURWdZbWhZZHd4V3RpbDZSZlpCK2ZHUS9IOUk5V0xubDRLVFpVUwo2QzkrTkxIaDRGUERoU2sxOWZwUzJTLzU2YXFnRm9HQWtYQVl0OUZ5NUVDYVBjVUxJZkoxREVic1hLeVJkQ3YzCkpZODkrME1Oa09kYURuc2VtUzJvNUdsMDh6STRpWXR0M0w0MGdBWjYwTlBoMzFrVkxuWU5zbXZmTnhZeUtwK0EKZUp0REh5Vzl3N2Z0TTBIb2krQnVSbWNBUVNLRlYzcGs4ajUxbGEranJSQnJBVXY4YmxiUmNRNUJpWlV3SnpIRgpFS0l3VHNSR29SeUV4OTZzTm5CMDNuNkdUd2pJR3o5MlNtTGRObDk1cjlya3ZwKzJtNFM2cTFsUHVYYUZnN0RHCkJyWFdDOGl5cWVXRTJpb2Jkd0lJdVhQVE1WcVFiMTJtMWRBa0pWUk81TmRIblAvTXBxT3ZPZ0xxb1pCTkhHeUIKZzRHcW00c0NKSEN4QTFjOEVsZmEyUlFUQ2swdEF6bGxMNHZPbkkxR0hrR0puNjV4b2tHc2FVNEI0RDM2eGg3ZQpXcmZqNC9wZ1dIbXRvREFZYTh3elN3bzJHVkNaT3MrbXRFZ09RQjkxL2c9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==",
    "key": "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpQcm9jLVR5cGU6IDQsRU5DUllQVEVECkRFSy1JbmZvOiBERVMtRURFMy1DQkMsOEY5QzYxOUQyNkM1M0M0QwoKOE5GRVlSSU9ZT0l3aXVOSDNTVUlkeW93WGtxQmVlWDhydGpCYVlXZWJmcHY4dzdEcFJvZnVaVHRzcEtqTXhQSwp5K1NQUHdkVUF1cVlmc3c2UVk3ZWZ2WVRGZ0pFVUlXb2lJRmhlblQyYmtvektPMExoeVVHNXVuZUJWczVObzhkCjZIdDUzdkpXeEkwK2NzYU5nQTNpR0ZUQTVaT2FyQlR1alg4aTVqMFVBR0haMVNURksvQ1BJUHhPVE45bWV4WDcKblFXMzhERzkva1RBd2d4Z3NGaG9EbFdCeWluWndpeXRYcGNEa1Y5UDEwZDF2RUJkeVhFa0FxV25nK0dNa2ZpOApxanI3d29iTDl0Zm9iOW9pb0ZxbVJjQy9lYmlIa3lTZjFuZUlQNEU1RFhHaGJwcFBkWTNhbkdQbjRLaE12TFF6CjZPZ3BOaVkwKzlja3BIclppMlFpMGNwdFBFRjBUWi9IK2dTK1doamtGQWhta2ppSG5CNEZUSy8zVVdmeVhjazUKWXlSWDU2MDV1Q2ZaZ3Jtd3dOMURwQ3dKR2dLcW1EMStZUmZXWDB3TVZSTVMxWDBOVTBIMzZmZGhheFI5OGpPNQp3eHZMVGVlYTF2NUpUTjk1TjZ0R3YxL1BKYVVUQnU5SnlBQmsyRzc5bnl3R0lMdFloLzYzN3ROeUxPaFA3N2FGCmlTL0JWdkFZR1lZZVN5QW9Ra0dQL1poUjFoNFZ4UmFnL21paHpOOE02aHBEN3Nwa2U5MmJ4d0RhZjlLTVhiUVUKZkRCd2tBeis0SjV4TGh6OEgweUpNQjJQUVNQNkJ1M1dhMm5XcnM4THcyTGMxTFhrN1VpZjNSbkd3cDg1WjdregplcEhuQTlUVnRDR3BIME15Y2Z2Mm5FbTk0S2FRVi9lZjVCb3NyWUl4aUl6WkZFZlZ0Q3dXQ2xueHpEWkt1a3ErCkZMZHVrQlpET1k1ekZpM3h4YStKRS9LbjFlcHdxYk9oMDlkVk1UL1ZzUXk4SHZYc3pIcDl3TnhHTEFmV3RrTlAKS0lhTHYyVWxoTkZHekVWbW03U09YU0FRTmM2WFNsT0NzeThhcU5aOE9uS1ppeDVWVSt3Wngxa0Ryd1NObWZ1bQp4Uk9BZjJwdnNTc2hDL045Y2ljTjhmTFpyS2JBbzJoMERCMDJReWt1bW5obnNPVXVEQ2VUUmdlU1pKNTF3M0VwCnBJdHB1WWwvRThITnRpb3hxRG9wL1pOdHhnd05XNm9XaVU4T29sSEFjbzRxd0xMN2hXQThJTDlROGszcy9kQ1QKSWpNUTJKLzhZSkRlM3dRN2xwbXRvZlNSRUNRTGZvYWpEbkdHOXhkaFJkVUdBRnNwM01PcVBpajF6Y3dXYWVJUwpUckRHUnNGMWI1dG85TXRHWHhUV2p1SVVxT3VETVpVcXJkbjQ3THBxZVljLytvNmw5NldvTkpVaW5zN3ZFN21RCldPcjd2QTFPYndnR1IzM1Y1Rkp2a1N2UUkvNUZVeUNSeXFkUHBJSStZOHFIS1J0cDFtdzVQNlhEakhwa3ByUWoKdEZEeW1FWDV5VWNZSkFMRWs4Wk5uR1lISnc3VHo2SU5rMnl2cVpXdlpBTG5qNDhPSFJEaE9ieGdJeFZITHZIdwpzVjFoQ2lnM1FNOVF0L3p4RGo4ejNKVzlsbElzSXBld2ZIaFRyay9XN1NySVozWThHOXI1dnYxeWFmRFFQdnViCnN0ZUZvYWhQQlNmUFdWenJ6aDNtdnBraW1KMzhrRUNEd3JYR0xROGxsenZOdTV1b0JjNkdQRy80cGJwYVJGSGMKTi9jMUVUZVk5MjZyYWNVWWJyR1FLbDJZUE5FWVNjL1ExT0xzaG4za0VjeFhVWjhHTDRGczFhQVdTYVpIbVBEawpKSDdKRWYxM0dyWlc5WW5ua0hvWUl1WFQ1UngzemhBQ0R3MEV3bVRHNGYrTVprbldNbVQ3WDh0Zml5aTFWOUhvCld6QVJnYzhpTDNqZkJ4TDYvTnFoRHFJOUx3dmdzSEZKbnFONjV1Q0xkdHQzek82RXhFSml3akhiVE42NnhocjAKMFB4MXBUb2diakxhYzRoVXNsVklYQUZ1QkJxYlJlZFlDZS8wSnA2YkpSTGtMWngxWmI5YTFBPT0KLS0tLS1FTkQgUlNBIFBSSVZBVEUgS0VZLS0tLS0K"
  },
  "fechaFinalPago": "2022-05-15",
  "fechaInicialPago": "2022-05-09",
  "fechaPago": "2022-05-15",
  "noCertificado": "30001000000400002434",
  "periodicidadPago": "02",
  "registroPatronal": "A4914083100",
  "tipoNomina": "O",
  "origenRecurso": "IP"
}'
```

### Respuesta 1

Retorna un objeto con la información de la cadena original, el sello, certificado, xml, UUID y un mensaje.

```json

{
  "Empleado 1": {
    "errors": false,
    "data": {
      "cadenaOriginal": "||4.0|702|201802|2022-05-15T16:55:56|30001000000400002434|710.00|300.00|MXN|410.00|N|01|PUE|20928|EKU9003173C9|ESCUELA KEMPER URGATE SA DE CV|601|MASO451221PM4|MARIA OLIVIA MARTINEZ SAGAZ|80290|605|CN01|84111505|1|ACT|Pago de nómina|710|710.00|300.00|01|1.2|O|2022-05-15|2022-05-09|2022-05-15|7|610|300|100|A4914083100|IP|MELH450218MSLNPL03|1234567|2022-01-01|P19W|01|No|01|02|702|SOLDADOR|1|02|180.00|COL|610|310|300|001|43200006|Sueldo|100|100|005|43200004|fondo ahorro|100|100|010|43200009|fondo ahorro|110|100|200|100|001|50000300|imss|100|002|50000302|isr|100|004|50000305|otros|100|002|11700001|Subsidio para el empleo|100|120||",
      "sello": "HLPZjaIWbKPQBXl8QPz2NV2GZWYS49IsSVGl0DA4x8hPG8wlbf5L1CaZ5DaJIBPGhyhnP1W6YGES5ha8GarrwLshny3mprO1xR4BeWfqMJM4ksqAgJwjd59BaEeq72eSo5yN8O61Xky/SBPljJDacrROuogLp58G4tnXJdkQy2t6jMY13ZHI43yhhdNb6OYClTEgihC/jdiQQXQ4QfSfKGGINFsF93xPwkNj5jPTx8PqGjpK9+PmdEtd0hknmkhPRgalps9bGpZhDGAHYOuaBvvetp8829SOj7ob6ogD05Op54IaYXZ8as7qtVrCUpufcHsbWVwV5rWoXXbVe2eDGQ==",
      "certificado": "MIIFuzCCA6OgAwIBAgIUMzAwMDEwMDAwMDA0MDAwMDI0MzQwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWRpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMTkwNjE3MTk0NDE0WhcNMjMwNjE3MTk0NDE0WjCB4jEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gWElRQjg5MTExNlFFNDEeMBwGA1UEBRMVIC8gWElRQjg5MTExNk1HUk1aUjA1MR4wHAYDVQQLExVFc2N1ZWxhIEtlbXBlciBVcmdhdGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCN0peKpgfOL75iYRv1fqq+oVYsLPVUR/GibYmGKc9InHFy5lYF6OTYjnIIvmkOdRobbGlCUxORX/tLsl8Ya9gm6Yo7hHnODRBIDup3GISFzB/96R9K/MzYQOcscMIoBDARaycnLvy7FlMvO7/rlVnsSARxZRO8Kz8Zkksj2zpeYpjZIya/369+oGqQk1cTRkHo59JvJ4Tfbk/3iIyf4H/Ini9nBe9cYWo0MnKob7DDt/vsdi5tA8mMtA953LapNyCZIDCRQQlUGNgDqY9/8F5mUvVgkcczsIgGdvf9vMQPSf3jjCiKj7j6ucxl1+FwJWmbvgNmiaUR/0q4m2rm78lFAgMBAAGjHTAbMAwGA1UdEwEB/wQCMAAwCwYDVR0PBAQDAgbAMA0GCSqGSIb3DQEBCwUAA4ICAQBcpj1TjT4jiinIujIdAlFzE6kRwYJCnDG08zSp4kSnShjxADGEXH2chehKMV0FY7c4njA5eDGdA/G2OCTPvF5rpeCZP5Dw504RZkYDl2suRz+wa1sNBVpbnBJEK0fQcN3IftBwsgNFdFhUtCyw3lus1SSJbPxjLHS6FcZZ51YSeIfcNXOAuTqdimusaXq15GrSrCOkM6n2jfj2sMJYM2HXaXJ6rGTEgYmhYdwxWtil6RfZB+fGQ/H9I9WLnl4KTZUS6C9+NLHh4FPDhSk19fpS2S/56aqgFoGAkXAYt9Fy5ECaPcULIfJ1DEbsXKyRdCv3JY89+0MNkOdaDnsemS2o5Gl08zI4iYtt3L40gAZ60NPh31kVLnYNsmvfNxYyKp+AeJtDHyW9w7ftM0Hoi+BuRmcAQSKFV3pk8j51la+jrRBrAUv8blbRcQ5BiZUwJzHFEKIwTsRGoRyEx96sNnB03n6GTwjIGz92SmLdNl95r9rkvp+2m4S6q1lPuXaFg7DGBrXWC8iyqeWE2iobdwIIuXPTMVqQb12m1dAkJVRO5NdHnP/MpqOvOgLqoZBNHGyBg4Gqm4sCJHCxA1c8Elfa2RQTCk0tAzllL4vOnI1GHkGJn65xokGsaU4B4D36xh7eWrfj4/pgWHmtoDAYa8wzSwo2GVCZOs+mtEgOQB91/g==",
      "xml": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\r\n<cfdi:Comprobante xmlns:cfdi=\"http://www.sat.gob.mx/cfd/4\" xmlns:xs=\"http://www.w3.org/2001/XMLSchema\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:nomina12=\"http://www.sat.gob.mx/nomina12\" xsi:schemaLocation=\"http://www.sat.gob.mx/cfd/4 http://www.sat.gob.mx/sitio_internet/cfd/4/cfdv40.xsd http://www.sat.gob.mx/nomina12 http://www.sat.gob.mx/sitio_internet/cfd/nomina/nomina12.xsd\" Version=\"4.0\" Serie=\"702\" Folio=\"201802\" Fecha=\"2022-05-15T16:55:56\" Sello=\"HLPZjaIWbKPQBXl8QPz2NV2GZWYS49IsSVGl0DA4x8hPG8wlbf5L1CaZ5DaJIBPGhyhnP1W6YGES5ha8GarrwLshny3mprO1xR4BeWfqMJM4ksqAgJwjd59BaEeq72eSo5yN8O61Xky/SBPljJDacrROuogLp58G4tnXJdkQy2t6jMY13ZHI43yhhdNb6OYClTEgihC/jdiQQXQ4QfSfKGGINFsF93xPwkNj5jPTx8PqGjpK9+PmdEtd0hknmkhPRgalps9bGpZhDGAHYOuaBvvetp8829SOj7ob6ogD05Op54IaYXZ8as7qtVrCUpufcHsbWVwV5rWoXXbVe2eDGQ==\" NoCertificado=\"30001000000400002434\" Certificado=\"MIIFuzCCA6OgAwIBAgIUMzAwMDEwMDAwMDA0MDAwMDI0MzQwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWRpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMTkwNjE3MTk0NDE0WhcNMjMwNjE3MTk0NDE0WjCB4jEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gWElRQjg5MTExNlFFNDEeMBwGA1UEBRMVIC8gWElRQjg5MTExNk1HUk1aUjA1MR4wHAYDVQQLExVFc2N1ZWxhIEtlbXBlciBVcmdhdGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCN0peKpgfOL75iYRv1fqq+oVYsLPVUR/GibYmGKc9InHFy5lYF6OTYjnIIvmkOdRobbGlCUxORX/tLsl8Ya9gm6Yo7hHnODRBIDup3GISFzB/96R9K/MzYQOcscMIoBDARaycnLvy7FlMvO7/rlVnsSARxZRO8Kz8Zkksj2zpeYpjZIya/369+oGqQk1cTRkHo59JvJ4Tfbk/3iIyf4H/Ini9nBe9cYWo0MnKob7DDt/vsdi5tA8mMtA953LapNyCZIDCRQQlUGNgDqY9/8F5mUvVgkcczsIgGdvf9vMQPSf3jjCiKj7j6ucxl1+FwJWmbvgNmiaUR/0q4m2rm78lFAgMBAAGjHTAbMAwGA1UdEwEB/wQCMAAwCwYDVR0PBAQDAgbAMA0GCSqGSIb3DQEBCwUAA4ICAQBcpj1TjT4jiinIujIdAlFzE6kRwYJCnDG08zSp4kSnShjxADGEXH2chehKMV0FY7c4njA5eDGdA/G2OCTPvF5rpeCZP5Dw504RZkYDl2suRz+wa1sNBVpbnBJEK0fQcN3IftBwsgNFdFhUtCyw3lus1SSJbPxjLHS6FcZZ51YSeIfcNXOAuTqdimusaXq15GrSrCOkM6n2jfj2sMJYM2HXaXJ6rGTEgYmhYdwxWtil6RfZB+fGQ/H9I9WLnl4KTZUS6C9+NLHh4FPDhSk19fpS2S/56aqgFoGAkXAYt9Fy5ECaPcULIfJ1DEbsXKyRdCv3JY89+0MNkOdaDnsemS2o5Gl08zI4iYtt3L40gAZ60NPh31kVLnYNsmvfNxYyKp+AeJtDHyW9w7ftM0Hoi+BuRmcAQSKFV3pk8j51la+jrRBrAUv8blbRcQ5BiZUwJzHFEKIwTsRGoRyEx96sNnB03n6GTwjIGz92SmLdNl95r9rkvp+2m4S6q1lPuXaFg7DGBrXWC8iyqeWE2iobdwIIuXPTMVqQb12m1dAkJVRO5NdHnP/MpqOvOgLqoZBNHGyBg4Gqm4sCJHCxA1c8Elfa2RQTCk0tAzllL4vOnI1GHkGJn65xokGsaU4B4D36xh7eWrfj4/pgWHmtoDAYa8wzSwo2GVCZOs+mtEgOQB91/g==\" SubTotal=\"710.00\" Descuento=\"300.00\" Moneda=\"MXN\" Total=\"410.00\" TipoDeComprobante=\"N\" Exportacion=\"01\" MetodoPago=\"PUE\" LugarExpedicion=\"20928\"><cfdi:Emisor Rfc=\"EKU9003173C9\" Nombre=\"ESCUELA KEMPER URGATE SA DE CV\" RegimenFiscal=\"601\" /><cfdi:Receptor Rfc=\"MASO451221PM4\" Nombre=\"MARIA OLIVIA MARTINEZ SAGAZ\" DomicilioFiscalReceptor=\"80290\" RegimenFiscalReceptor=\"605\" UsoCFDI=\"CN01\" /><cfdi:Conceptos><cfdi:Concepto ClaveProdServ=\"84111505\" Cantidad=\"1\" ClaveUnidad=\"ACT\" Descripcion=\"Pago de nómina\" ValorUnitario=\"710\" Importe=\"710.00\" Descuento=\"300.00\" ObjetoImp=\"01\" /></cfdi:Conceptos><cfdi:Complemento><tfd:TimbreFiscalDigital xmlns:tfd=\"http://www.sat.gob.mx/TimbreFiscalDigital\" xsi:schemaLocation=\"http://www.sat.gob.mx/TimbreFiscalDigital http://www.sat.gob.mx/sitio_internet/cfd/TimbreFiscalDigital/TimbreFiscalDigitalv11.xsd\" Version=\"1.1\" UUID=\"17E7F47E-4A1B-494E-BEEB-55D1D9C509CE\" FechaTimbrado=\"2022-05-15T19:05:57\" RfcProvCertif=\"SPR190613I52\" SelloCFD=\"HLPZjaIWbKPQBXl8QPz2NV2GZWYS49IsSVGl0DA4x8hPG8wlbf5L1CaZ5DaJIBPGhyhnP1W6YGES5ha8GarrwLshny3mprO1xR4BeWfqMJM4ksqAgJwjd59BaEeq72eSo5yN8O61Xky/SBPljJDacrROuogLp58G4tnXJdkQy2t6jMY13ZHI43yhhdNb6OYClTEgihC/jdiQQXQ4QfSfKGGINFsF93xPwkNj5jPTx8PqGjpK9+PmdEtd0hknmkhPRgalps9bGpZhDGAHYOuaBvvetp8829SOj7ob6ogD05Op54IaYXZ8as7qtVrCUpufcHsbWVwV5rWoXXbVe2eDGQ==\" NoCertificadoSAT=\"30001000000400002495\" SelloSAT=\"LfloEvlBnZfaMK76zYNy67DZxnA0ssUNi8b4h2EDNU7hU/6TGX4QYQ4d2sY+HFHnW/ZF0pXwF/PsYnZfN0ejP9GGzy/6jyEPXH3iGH7wPVo4cJVAnZ5cI2fbwAfiX6ZoMLnCvLaOp8F2KMp8ym9wc+bXW8pdvJhLOFBJPCUKB7Quyhz2OMlGgv6UjHv++G6OzM8m99aqzDMfyHXvmdlMYU+GeaVupzLNoW027Z7LVi2bRNYwf+CaqYJmV9/VevvLBfCTLY2p4xHziybsjaRk92dMiLYfeuc4BH9fsvSddDoKajvp6jI1p/uzH726W7JFdShR/KbviKyFoov3Wjdb3g==\" /><nomina12:Nomina Version=\"1.2\" TipoNomina=\"O\" FechaPago=\"2022-05-15\" FechaInicialPago=\"2022-05-09\" FechaFinalPago=\"2022-05-15\" NumDiasPagados=\"7\" TotalPercepciones=\"610\" TotalDeducciones=\"300\" TotalOtrosPagos=\"100\"><nomina12:Emisor RegistroPatronal=\"A4914083100\"><nomina12:EntidadSNCF OrigenRecurso=\"IP\" /></nomina12:Emisor><nomina12:Receptor Curp=\"MELH450218MSLNPL03\" NumSeguridadSocial=\"1234567\" FechaInicioRelLaboral=\"2022-01-01\" Antigüedad=\"P19W\" TipoContrato=\"01\" Sindicalizado=\"No\" TipoJornada=\"01\" TipoRegimen=\"02\" NumEmpleado=\"702\" Departamento=\"SOLDADOR\" RiesgoPuesto=\"1\" PeriodicidadPago=\"02\" SalarioDiarioIntegrado=\"180.00\" ClaveEntFed=\"COL\" /><nomina12:Percepciones TotalGravado=\"310\" TotalExento=\"300\" TotalSueldos=\"610\"><nomina12:Percepcion TipoPercepcion=\"001\" Clave=\"43200006\" Concepto=\"Sueldo\" ImporteGravado=\"100\" ImporteExento=\"100\" /><nomina12:Percepcion TipoPercepcion=\"005\" Clave=\"43200004\" Concepto=\"fondo ahorro\" ImporteGravado=\"100\" ImporteExento=\"100\" /><nomina12:Percepcion TipoPercepcion=\"010\" Clave=\"43200009\" Concepto=\"fondo ahorro\" ImporteGravado=\"110\" ImporteExento=\"100\" /></nomina12:Percepciones><nomina12:Deducciones TotalOtrasDeducciones=\"200\" TotalImpuestosRetenidos=\"100\"><nomina12:Deduccion TipoDeduccion=\"001\" Clave=\"50000300\" Concepto=\"imss\" Importe=\"100\" /><nomina12:Deduccion TipoDeduccion=\"002\" Clave=\"50000302\" Concepto=\"isr\" Importe=\"100\" /><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"50000305\" Concepto=\"otros\" Importe=\"100\" /></nomina12:Deducciones><nomina12:OtrosPagos><nomina12:OtroPago TipoOtroPago=\"002\" Clave=\"11700001\" Concepto=\"Subsidio para el empleo\" Importe=\"100\"><nomina12:SubsidioAlEmpleo SubsidioCausado=\"120\" /></nomina12:OtroPago></nomina12:OtrosPagos></nomina12:Nomina></cfdi:Complemento></cfdi:Comprobante>\r\n",
      "uuid": "17E7F47E-4A1B-494E-BEEB-55D1D9C509CE",
      "msg": "Se timbro el recibo de nomina correctamente.",
      "statusCode": 200
    },
    "row": 0
  }
}

```

### Ejemplo 2 de petición

```php
  curl https://development.kubox.mx/v2/timbre/nomina40 \
     -H "Content-type: application/json" \
     -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg3NzM2MTAsImV4cCI6MTUwODc5NTIxMCwibmJmIjoxNTA4NzczNjEwLCJqdGkiOiJIcUZPbDlWSWZSYk53N3ZqIiwic3ViIjo4NX0.GEqizwFutuibe_RYUXh3i0sOmK-PDRKK88tJBSTyJr4' \
     -X POST -d '{
  "data": [
    {
      "serie": "702",
      "folio": "201802",
      "noEmpleado": "702",
      "nombre": "MARIA OLIVIA MARTINEZ SAGAZ",
      "rfc": "MASO451221PM4",
      "curp": "MELH450218MSLNPL03",
      "cp": "80290",
      "claveEntFed": "COL",
      "departamento": "SOLDADOR",
      "sdi": 180,
      "diasPago": 7,
      "ex_FechaInicioRelLaboral": "2016-05-31",
      "ex_RiesgoPuesto": "1",
      "ex_TipoJornada": "01",
      "seguro_social": "52079004371",
      "tipoContrato": "01",
      "tipoRegimen": "02",

      "pe_aguinaldo_clave": "43200006",
      "pe_aguinaldo_concepto": "Gratificación Anual Aguinaldo",
      "pe_aguinaldo_excento": 500,
      "pe_aguinaldo_gravado": 0,
      "pe_prima_vacacional_clave": "43200004",
      "pe_prima_vacacional_concepto": "Prima vacacional",
      "pe_prima_vacacional_excento": 500,
      "pe_prima_vacacional_gravado": 0,
      "pe_sueldo_clave": "43200003",
      "pe_sueldo_concepto": "Vacaciones",
      "pe_sueldo_excento": 100,
      "pe_sueldo_gravado": 100,
      "pe_fondo_ahorro_clave": "43200014",
      "pe_fondo_ahorro_concepto": "Fondo de ahorro",
      "pe_fondo_ahorro_gravado": 100,
      "pe_fondo_ahorro_excento": 100,
      "pe_premio_puntualidad_clave": "43200013",
      "pe_premio_puntualidad_concepto": "p puntualidad",
      "pe_premio_puntualidad_gravado": 100,
      "pe_premio_puntualidad_excento": 100,

      "de_otros_clave": "50000300",
      "de_otros_concepto": "Otros",
      "de_otros_importe": 100,
      "de_isr_clave": "50000301",
      "de_isr_concepto": "ISR",
      "de_isr_importe": 100,
      "de_seguro_social_clave": "50000303",
      "de_seguro_social_concepto": "Imss",
      "de_seguro_social_importe": 100,

      "top_subsidio_empleo_clave": "11700001",
      "top_subsidio_empleo_concepto": "Subsidio para el empleo",
      "top_subsidio_empleo_causado": 350,
      "top_subsidio_empleo_importe": 10,

      "total": 310
    },
    {
      "serie": "702",
      "folio": "201805",
      "noEmpleado": "702",
      "nombre": "CESAR OSBALDO CRUZ SOLORZANO",
      "rfc": "CUSC850516316",
      "curp": "CUSC850516MCMSLS03",
      "cp": "45638",
      "claveEntFed": "COL",
      "departamento": "SOLDADOR",
      "sdi": 315,
      "diasPago": 7,
      "ex_FechaInicioRelLaboral": "2016-05-31",
      "ex_RiesgoPuesto": "3",
      "ex_TipoJornada": "01",
      "seguro_social": "52079004371",
      "tipoContrato": "01",
      "tipoRegimen": "02",

      "pe_aguinaldo_clave": "43200006",
      "pe_aguinaldo_concepto": "Gratificación Anual Aguinaldo",
      "pe_aguinaldo_excento": 500,
      "pe_aguinaldo_gravado": 0,
      "pe_prima_vacacional_clave": "43200004",
      "pe_prima_vacacional_concepto": "Prima vacacional",
      "pe_prima_vacacional_excento": 500,
      "pe_prima_vacacional_gravado": 0,
      "pe_sueldo_clave": "43200003",
      "pe_sueldo_concepto": "Vacaciones",
      "pe_sueldo_excento": 100,
      "pe_sueldo_gravado": 100,
      "pe_fondo_ahorro_clave": "43200014",
      "pe_fondo_ahorro_concepto": "Fondo de ahorro",
      "pe_fondo_ahorro_gravado": 100,
      "pe_fondo_ahorro_excento": 100,
      "pe_premio_puntualidad_clave": "43200013",
      "pe_premio_puntualidad_concepto": "p puntualidad",
      "pe_premio_puntualidad_gravado": 100,
      "pe_premio_puntualidad_excento": 100,

      "de_otros_clave": "50000300",
      "de_otros_concepto": "Otros",
      "de_otros_importe": 100,
      "de_isr_clave": "50000301",
      "de_isr_concepto": "ISR",
      "de_isr_importe": 100,
      "de_seguro_social_clave": "50000303",
      "de_seguro_social_concepto": "Imss",
      "de_seguro_social_importe": 100,

      "top_subsidio_empleo_clave": "11700001",
      "top_subsidio_empleo_concepto": "Subsidio para el empleo",
      "top_subsidio_empleo_causado": 350,
      "top_subsidio_empleo_importe": 10,

      "total": 310
    }
  ],
  "emisor": {
    "nombreFiscal": "ESCUELA KEMPER URGATE SA DE CV",
    "rfc": "EKU9003173C9",
    "regimenFiscal": "601",
    "curp": "",
    "cp": "20928",
    "cer": "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQklqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUFqZEtYaXFZSHppKytZbUViOVg2cQp2cUZXTEN6MVZFZnhvbTJKaGluUFNKeHhjdVpXQmVqazJJNXlDTDVwRG5VYUcyeHBRbE1Ua1YvN1M3SmZHR3ZZCkp1bUtPNFI1emcwUVNBN3FkeGlFaGN3Zi9la2ZTdnpNMkVEbkxIRENLQVF3RVdzbkp5Nzh1eFpUTHp1LzY1VloKN0VnRWNXVVR2Q3MvR1pKTEk5czZYbUtZMlNNbXY5K3ZmcUJxa0pOWEUwWkI2T2ZTYnllRTMyNVA5NGlNbitCLwp5SjR2WndYdlhHRnFOREp5cUcrd3c3Zjc3SFl1YlFQSmpMUVBlZHkycVRjZ21TQXdrVUVKVkJqWUE2bVBmL0JlClpsTDFZSkhITTdDSUJuYjMvYnpFRDBuOTQ0d29pbys0K3JuTVpkZmhjQ1ZwbTc0RFpvbWxFZjlLdUp0cTV1L0oKUlFJREFRQUIKLS0tLS1FTkQgUFVCTElDIEtFWS0tLS0tCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQpNSUlGdXpDQ0E2T2dBd0lCQWdJVU16QXdNREV3TURBd01EQTBNREF3TURJME16UXdEUVlKS29aSWh2Y05BUUVMCkJRQXdnZ0VyTVE4d0RRWURWUVFEREFaQlF5QlZRVlF4TGpBc0JnTlZCQW9NSlZORlVsWkpRMGxQSUVSRklFRkUKVFVsT1NWTlVVa0ZEU1U5T0lGUlNTVUpWVkVGU1NVRXhHakFZQmdOVkJBc01FVk5CVkMxSlJWTWdRWFYwYUc5eQphWFI1TVNnd0pnWUpLb1pJaHZjTkFRa0JGaGx2YzJOaGNpNXRZWEowYVc1bGVrQnpZWFF1WjI5aUxtMTRNUjB3Ckd3WURWUVFKREJRemNtRWdZMlZ5Y21Ga1lTQmtaU0JqWVdScGVqRU9NQXdHQTFVRUVRd0ZNRFl6TnpBeEN6QUoKQmdOVkJBWVRBazFZTVJrd0Z3WURWUVFJREJCRFNWVkVRVVFnUkVVZ1RVVllTVU5QTVJFd0R3WURWUVFIREFoRApUMWxQUVVOQlRqRVJNQThHQTFVRUxSTUlNaTQxTGpRdU5EVXhKVEFqQmdrcWhraUc5dzBCQ1FJVEZuSmxjM0J2CmJuTmhZbXhsT2lCQlEwUk5RUzFUUVZRd0hoY05NVGt3TmpFM01UazBOREUwV2hjTk1qTXdOakUzTVRrME5ERTAKV2pDQjRqRW5NQ1VHQTFVRUF4TWVSVk5EVlVWTVFTQkxSVTFRUlZJZ1ZWSkhRVlJGSUZOQklFUkZJRU5XTVNjdwpKUVlEVlFRcEV4NUZVME5WUlV4QklFdEZUVkJGVWlCVlVrZEJWRVVnVTBFZ1JFVWdRMVl4SnpBbEJnTlZCQW9UCkhrVlRRMVZGVEVFZ1MwVk5VRVZTSUZWU1IwRlVSU0JUUVNCRVJTQkRWakVsTUNNR0ExVUVMUk1jUlV0Vk9UQXcKTXpFM00wTTVJQzhnV0VsUlFqZzVNVEV4TmxGRk5ERWVNQndHQTFVRUJSTVZJQzhnV0VsUlFqZzVNVEV4TmsxSApVazFhVWpBMU1SNHdIQVlEVlFRTEV4VkZjMk4xWld4aElFdGxiWEJsY2lCVmNtZGhkR1V3Z2dFaU1BMEdDU3FHClNJYjNEUUVCQVFVQUE0SUJEd0F3Z2dFS0FvSUJBUUNOMHBlS3BnZk9MNzVpWVJ2MWZxcStvVllzTFBWVVIvR2kKYlltR0tjOUluSEZ5NWxZRjZPVFlqbklJdm1rT2RSb2JiR2xDVXhPUlgvdExzbDhZYTlnbTZZbzdoSG5PRFJCSQpEdXAzR0lTRnpCLzk2UjlLL016WVFPY3NjTUlvQkRBUmF5Y25Mdnk3RmxNdk83L3JsVm5zU0FSeFpSTzhLejhaCmtrc2oyenBlWXBqWkl5YS8zNjkrb0dxUWsxY1RSa0hvNTlKdko0VGZiay8zaUl5ZjRIL0luaTluQmU5Y1lXbzAKTW5Lb2I3RER0L3ZzZGk1dEE4bU10QTk1M0xhcE55Q1pJRENSUVFsVUdOZ0RxWTkvOEY1bVV2VmdrY2N6c0lnRwpkdmY5dk1RUFNmM2pqQ2lLajdqNnVjeGwxK0Z3SldtYnZnTm1pYVVSLzBxNG0ycm03OGxGQWdNQkFBR2pIVEFiCk1Bd0dBMVVkRXdFQi93UUNNQUF3Q3dZRFZSMFBCQVFEQWdiQU1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQ0FRQmMKcGoxVGpUNGppaW5JdWpJZEFsRnpFNmtSd1lKQ25ERzA4elNwNGtTblNoanhBREdFWEgyY2hlaEtNVjBGWTdjNApuakE1ZURHZEEvRzJPQ1RQdkY1cnBlQ1pQNUR3NTA0UlprWURsMnN1Unord2Exc05CVnBibkJKRUswZlFjTjNJCmZ0QndzZ05GZEZoVXRDeXczbHVzMVNTSmJQeGpMSFM2RmNaWjUxWVNlSWZjTlhPQXVUcWRpbXVzYVhxMTVHclMKckNPa002bjJqZmoyc01KWU0ySFhhWEo2ckdURWdZbWhZZHd4V3RpbDZSZlpCK2ZHUS9IOUk5V0xubDRLVFpVUwo2QzkrTkxIaDRGUERoU2sxOWZwUzJTLzU2YXFnRm9HQWtYQVl0OUZ5NUVDYVBjVUxJZkoxREVic1hLeVJkQ3YzCkpZODkrME1Oa09kYURuc2VtUzJvNUdsMDh6STRpWXR0M0w0MGdBWjYwTlBoMzFrVkxuWU5zbXZmTnhZeUtwK0EKZUp0REh5Vzl3N2Z0TTBIb2krQnVSbWNBUVNLRlYzcGs4ajUxbGEranJSQnJBVXY4YmxiUmNRNUJpWlV3SnpIRgpFS0l3VHNSR29SeUV4OTZzTm5CMDNuNkdUd2pJR3o5MlNtTGRObDk1cjlya3ZwKzJtNFM2cTFsUHVYYUZnN0RHCkJyWFdDOGl5cWVXRTJpb2Jkd0lJdVhQVE1WcVFiMTJtMWRBa0pWUk81TmRIblAvTXBxT3ZPZ0xxb1pCTkhHeUIKZzRHcW00c0NKSEN4QTFjOEVsZmEyUlFUQ2swdEF6bGxMNHZPbkkxR0hrR0puNjV4b2tHc2FVNEI0RDM2eGg3ZQpXcmZqNC9wZ1dIbXRvREFZYTh3elN3bzJHVkNaT3MrbXRFZ09RQjkxL2c9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==",
    "key": "LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpQcm9jLVR5cGU6IDQsRU5DUllQVEVECkRFSy1JbmZvOiBERVMtRURFMy1DQkMsOEY5QzYxOUQyNkM1M0M0QwoKOE5GRVlSSU9ZT0l3aXVOSDNTVUlkeW93WGtxQmVlWDhydGpCYVlXZWJmcHY4dzdEcFJvZnVaVHRzcEtqTXhQSwp5K1NQUHdkVUF1cVlmc3c2UVk3ZWZ2WVRGZ0pFVUlXb2lJRmhlblQyYmtvektPMExoeVVHNXVuZUJWczVObzhkCjZIdDUzdkpXeEkwK2NzYU5nQTNpR0ZUQTVaT2FyQlR1alg4aTVqMFVBR0haMVNURksvQ1BJUHhPVE45bWV4WDcKblFXMzhERzkva1RBd2d4Z3NGaG9EbFdCeWluWndpeXRYcGNEa1Y5UDEwZDF2RUJkeVhFa0FxV25nK0dNa2ZpOApxanI3d29iTDl0Zm9iOW9pb0ZxbVJjQy9lYmlIa3lTZjFuZUlQNEU1RFhHaGJwcFBkWTNhbkdQbjRLaE12TFF6CjZPZ3BOaVkwKzlja3BIclppMlFpMGNwdFBFRjBUWi9IK2dTK1doamtGQWhta2ppSG5CNEZUSy8zVVdmeVhjazUKWXlSWDU2MDV1Q2ZaZ3Jtd3dOMURwQ3dKR2dLcW1EMStZUmZXWDB3TVZSTVMxWDBOVTBIMzZmZGhheFI5OGpPNQp3eHZMVGVlYTF2NUpUTjk1TjZ0R3YxL1BKYVVUQnU5SnlBQmsyRzc5bnl3R0lMdFloLzYzN3ROeUxPaFA3N2FGCmlTL0JWdkFZR1lZZVN5QW9Ra0dQL1poUjFoNFZ4UmFnL21paHpOOE02aHBEN3Nwa2U5MmJ4d0RhZjlLTVhiUVUKZkRCd2tBeis0SjV4TGh6OEgweUpNQjJQUVNQNkJ1M1dhMm5XcnM4THcyTGMxTFhrN1VpZjNSbkd3cDg1WjdregplcEhuQTlUVnRDR3BIME15Y2Z2Mm5FbTk0S2FRVi9lZjVCb3NyWUl4aUl6WkZFZlZ0Q3dXQ2xueHpEWkt1a3ErCkZMZHVrQlpET1k1ekZpM3h4YStKRS9LbjFlcHdxYk9oMDlkVk1UL1ZzUXk4SHZYc3pIcDl3TnhHTEFmV3RrTlAKS0lhTHYyVWxoTkZHekVWbW03U09YU0FRTmM2WFNsT0NzeThhcU5aOE9uS1ppeDVWVSt3Wngxa0Ryd1NObWZ1bQp4Uk9BZjJwdnNTc2hDL045Y2ljTjhmTFpyS2JBbzJoMERCMDJReWt1bW5obnNPVXVEQ2VUUmdlU1pKNTF3M0VwCnBJdHB1WWwvRThITnRpb3hxRG9wL1pOdHhnd05XNm9XaVU4T29sSEFjbzRxd0xMN2hXQThJTDlROGszcy9kQ1QKSWpNUTJKLzhZSkRlM3dRN2xwbXRvZlNSRUNRTGZvYWpEbkdHOXhkaFJkVUdBRnNwM01PcVBpajF6Y3dXYWVJUwpUckRHUnNGMWI1dG85TXRHWHhUV2p1SVVxT3VETVpVcXJkbjQ3THBxZVljLytvNmw5NldvTkpVaW5zN3ZFN21RCldPcjd2QTFPYndnR1IzM1Y1Rkp2a1N2UUkvNUZVeUNSeXFkUHBJSStZOHFIS1J0cDFtdzVQNlhEakhwa3ByUWoKdEZEeW1FWDV5VWNZSkFMRWs4Wk5uR1lISnc3VHo2SU5rMnl2cVpXdlpBTG5qNDhPSFJEaE9ieGdJeFZITHZIdwpzVjFoQ2lnM1FNOVF0L3p4RGo4ejNKVzlsbElzSXBld2ZIaFRyay9XN1NySVozWThHOXI1dnYxeWFmRFFQdnViCnN0ZUZvYWhQQlNmUFdWenJ6aDNtdnBraW1KMzhrRUNEd3JYR0xROGxsenZOdTV1b0JjNkdQRy80cGJwYVJGSGMKTi9jMUVUZVk5MjZyYWNVWWJyR1FLbDJZUE5FWVNjL1ExT0xzaG4za0VjeFhVWjhHTDRGczFhQVdTYVpIbVBEawpKSDdKRWYxM0dyWlc5WW5ua0hvWUl1WFQ1UngzemhBQ0R3MEV3bVRHNGYrTVprbldNbVQ3WDh0Zml5aTFWOUhvCld6QVJnYzhpTDNqZkJ4TDYvTnFoRHFJOUx3dmdzSEZKbnFONjV1Q0xkdHQzek82RXhFSml3akhiVE42NnhocjAKMFB4MXBUb2diakxhYzRoVXNsVklYQUZ1QkJxYlJlZFlDZS8wSnA2YkpSTGtMWngxWmI5YTFBPT0KLS0tLS1FTkQgUlNBIFBSSVZBVEUgS0VZLS0tLS0K"
  },
  "fechaFinalPago": "2022-05-15",
  "fechaInicialPago": "2022-05-09",
  "fechaPago": "2022-05-15",
  "noCertificado": "30001000000400002434",
  "periodicidadPago": "02",
  "registroPatronal": "A4914083100",
  "tipoNomina": "O",
  "origenRecurso": "IP"
}'
```

### Respuesta 2

Retorna un objeto con la información de la cadena original, el sello, certificado, xml, UUID y un mensaje.

```json

{
  "Empleado 1": {
    "errors": false,
    "data": {
      "cadenaOriginal": "||4.0|702|201802|2022-05-15T20:11:38|30001000000400002434|1610.00|300.00|MXN|1310.00|N|01|PUE|20928|EKU9003173C9|ESCUELA KEMPER URGATE SA DE CV|601|MASO451221PM4|MARIA OLIVIA MARTINEZ SAGAZ|80290|605|CN01|84111505|1|ACT|Pago de nómina|1610|1610.00|300.00|01|1.2|O|2022-05-15|2022-05-09|2022-05-15|7|1600|300|10|A4914083100|IP|MELH450218MSLNPL03|52079004371|2016-05-31|P310W|01|No|01|02|702|SOLDADOR|1|02|180.00|COL|1600|300|1300|002|43200006|Gratificación Anual Aguinaldo|0|500|021|43200004|Prima vacacional|0|500|001|43200003|Vacaciones|100|100|005|43200014|Fondo de ahorro|100|100|010|43200013|p puntualidad|100|100|200|100|004|50000300|Otros|100|002|50000301|ISR|100|001|50000303|Imss|100|002|11700001|Subsidio para el empleo|10|350||",
      "sello": "egRsyOe97Z5CYXE3fENgDovh55a+wiUJrZbtsL8m5epb79yLb8I59PdMzU/wH0w9z3L85O1OeKANjtVJTliwBDhzsRUHsqFU0H/TbeXS0W8EP03WaB7yTGklslVTNqAB0AB+CJiYrTh/n7ckq+zHrtajPouRgaqD6UT7LcLhbbfAYxpJ4k/enNk5JZW4LrurdqR2q5HSwCxGZaS9jM6E9/RRoj4oqSvPElGEmHhFT2NhSy5pPbpSGncYVVrKZ78zXKkvSZ0jN3N7aH0a//T37W7TUAh6zXdCE5K/MqluRdE1xjABPDq0SG4EAp+arUgvmZ1PHJAOm0poy3Sa2eLlWA==",
      "certificado": "MIIFuzCCA6OgAwIBAgIUMzAwMDEwMDAwMDA0MDAwMDI0MzQwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWRpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMTkwNjE3MTk0NDE0WhcNMjMwNjE3MTk0NDE0WjCB4jEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gWElRQjg5MTExNlFFNDEeMBwGA1UEBRMVIC8gWElRQjg5MTExNk1HUk1aUjA1MR4wHAYDVQQLExVFc2N1ZWxhIEtlbXBlciBVcmdhdGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCN0peKpgfOL75iYRv1fqq+oVYsLPVUR/GibYmGKc9InHFy5lYF6OTYjnIIvmkOdRobbGlCUxORX/tLsl8Ya9gm6Yo7hHnODRBIDup3GISFzB/96R9K/MzYQOcscMIoBDARaycnLvy7FlMvO7/rlVnsSARxZRO8Kz8Zkksj2zpeYpjZIya/369+oGqQk1cTRkHo59JvJ4Tfbk/3iIyf4H/Ini9nBe9cYWo0MnKob7DDt/vsdi5tA8mMtA953LapNyCZIDCRQQlUGNgDqY9/8F5mUvVgkcczsIgGdvf9vMQPSf3jjCiKj7j6ucxl1+FwJWmbvgNmiaUR/0q4m2rm78lFAgMBAAGjHTAbMAwGA1UdEwEB/wQCMAAwCwYDVR0PBAQDAgbAMA0GCSqGSIb3DQEBCwUAA4ICAQBcpj1TjT4jiinIujIdAlFzE6kRwYJCnDG08zSp4kSnShjxADGEXH2chehKMV0FY7c4njA5eDGdA/G2OCTPvF5rpeCZP5Dw504RZkYDl2suRz+wa1sNBVpbnBJEK0fQcN3IftBwsgNFdFhUtCyw3lus1SSJbPxjLHS6FcZZ51YSeIfcNXOAuTqdimusaXq15GrSrCOkM6n2jfj2sMJYM2HXaXJ6rGTEgYmhYdwxWtil6RfZB+fGQ/H9I9WLnl4KTZUS6C9+NLHh4FPDhSk19fpS2S/56aqgFoGAkXAYt9Fy5ECaPcULIfJ1DEbsXKyRdCv3JY89+0MNkOdaDnsemS2o5Gl08zI4iYtt3L40gAZ60NPh31kVLnYNsmvfNxYyKp+AeJtDHyW9w7ftM0Hoi+BuRmcAQSKFV3pk8j51la+jrRBrAUv8blbRcQ5BiZUwJzHFEKIwTsRGoRyEx96sNnB03n6GTwjIGz92SmLdNl95r9rkvp+2m4S6q1lPuXaFg7DGBrXWC8iyqeWE2iobdwIIuXPTMVqQb12m1dAkJVRO5NdHnP/MpqOvOgLqoZBNHGyBg4Gqm4sCJHCxA1c8Elfa2RQTCk0tAzllL4vOnI1GHkGJn65xokGsaU4B4D36xh7eWrfj4/pgWHmtoDAYa8wzSwo2GVCZOs+mtEgOQB91/g==",
      "xml": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\r\n<cfdi:Comprobante xmlns:cfdi=\"http://www.sat.gob.mx/cfd/4\" xmlns:xs=\"http://www.w3.org/2001/XMLSchema\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:nomina12=\"http://www.sat.gob.mx/nomina12\" xsi:schemaLocation=\"http://www.sat.gob.mx/cfd/4 http://www.sat.gob.mx/sitio_internet/cfd/4/cfdv40.xsd http://www.sat.gob.mx/nomina12 http://www.sat.gob.mx/sitio_internet/cfd/nomina/nomina12.xsd\" Version=\"4.0\" Serie=\"702\" Folio=\"201802\" Fecha=\"2022-05-15T20:11:38\" Sello=\"egRsyOe97Z5CYXE3fENgDovh55a+wiUJrZbtsL8m5epb79yLb8I59PdMzU/wH0w9z3L85O1OeKANjtVJTliwBDhzsRUHsqFU0H/TbeXS0W8EP03WaB7yTGklslVTNqAB0AB+CJiYrTh/n7ckq+zHrtajPouRgaqD6UT7LcLhbbfAYxpJ4k/enNk5JZW4LrurdqR2q5HSwCxGZaS9jM6E9/RRoj4oqSvPElGEmHhFT2NhSy5pPbpSGncYVVrKZ78zXKkvSZ0jN3N7aH0a//T37W7TUAh6zXdCE5K/MqluRdE1xjABPDq0SG4EAp+arUgvmZ1PHJAOm0poy3Sa2eLlWA==\" NoCertificado=\"30001000000400002434\" Certificado=\"MIIFuzCCA6OgAwIBAgIUMzAwMDEwMDAwMDA0MDAwMDI0MzQwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWRpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMTkwNjE3MTk0NDE0WhcNMjMwNjE3MTk0NDE0WjCB4jEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gWElRQjg5MTExNlFFNDEeMBwGA1UEBRMVIC8gWElRQjg5MTExNk1HUk1aUjA1MR4wHAYDVQQLExVFc2N1ZWxhIEtlbXBlciBVcmdhdGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCN0peKpgfOL75iYRv1fqq+oVYsLPVUR/GibYmGKc9InHFy5lYF6OTYjnIIvmkOdRobbGlCUxORX/tLsl8Ya9gm6Yo7hHnODRBIDup3GISFzB/96R9K/MzYQOcscMIoBDARaycnLvy7FlMvO7/rlVnsSARxZRO8Kz8Zkksj2zpeYpjZIya/369+oGqQk1cTRkHo59JvJ4Tfbk/3iIyf4H/Ini9nBe9cYWo0MnKob7DDt/vsdi5tA8mMtA953LapNyCZIDCRQQlUGNgDqY9/8F5mUvVgkcczsIgGdvf9vMQPSf3jjCiKj7j6ucxl1+FwJWmbvgNmiaUR/0q4m2rm78lFAgMBAAGjHTAbMAwGA1UdEwEB/wQCMAAwCwYDVR0PBAQDAgbAMA0GCSqGSIb3DQEBCwUAA4ICAQBcpj1TjT4jiinIujIdAlFzE6kRwYJCnDG08zSp4kSnShjxADGEXH2chehKMV0FY7c4njA5eDGdA/G2OCTPvF5rpeCZP5Dw504RZkYDl2suRz+wa1sNBVpbnBJEK0fQcN3IftBwsgNFdFhUtCyw3lus1SSJbPxjLHS6FcZZ51YSeIfcNXOAuTqdimusaXq15GrSrCOkM6n2jfj2sMJYM2HXaXJ6rGTEgYmhYdwxWtil6RfZB+fGQ/H9I9WLnl4KTZUS6C9+NLHh4FPDhSk19fpS2S/56aqgFoGAkXAYt9Fy5ECaPcULIfJ1DEbsXKyRdCv3JY89+0MNkOdaDnsemS2o5Gl08zI4iYtt3L40gAZ60NPh31kVLnYNsmvfNxYyKp+AeJtDHyW9w7ftM0Hoi+BuRmcAQSKFV3pk8j51la+jrRBrAUv8blbRcQ5BiZUwJzHFEKIwTsRGoRyEx96sNnB03n6GTwjIGz92SmLdNl95r9rkvp+2m4S6q1lPuXaFg7DGBrXWC8iyqeWE2iobdwIIuXPTMVqQb12m1dAkJVRO5NdHnP/MpqOvOgLqoZBNHGyBg4Gqm4sCJHCxA1c8Elfa2RQTCk0tAzllL4vOnI1GHkGJn65xokGsaU4B4D36xh7eWrfj4/pgWHmtoDAYa8wzSwo2GVCZOs+mtEgOQB91/g==\" SubTotal=\"1610.00\" Descuento=\"300.00\" Moneda=\"MXN\" Total=\"1310.00\" TipoDeComprobante=\"N\" Exportacion=\"01\" MetodoPago=\"PUE\" LugarExpedicion=\"20928\"><cfdi:Emisor Rfc=\"EKU9003173C9\" Nombre=\"ESCUELA KEMPER URGATE SA DE CV\" RegimenFiscal=\"601\" /><cfdi:Receptor Rfc=\"MASO451221PM4\" Nombre=\"MARIA OLIVIA MARTINEZ SAGAZ\" DomicilioFiscalReceptor=\"80290\" RegimenFiscalReceptor=\"605\" UsoCFDI=\"CN01\" /><cfdi:Conceptos><cfdi:Concepto ClaveProdServ=\"84111505\" Cantidad=\"1\" ClaveUnidad=\"ACT\" Descripcion=\"Pago de nómina\" ValorUnitario=\"1610\" Importe=\"1610.00\" Descuento=\"300.00\" ObjetoImp=\"01\" /></cfdi:Conceptos><cfdi:Complemento><tfd:TimbreFiscalDigital xmlns:tfd=\"http://www.sat.gob.mx/TimbreFiscalDigital\" xsi:schemaLocation=\"http://www.sat.gob.mx/TimbreFiscalDigital http://www.sat.gob.mx/sitio_internet/cfd/TimbreFiscalDigital/TimbreFiscalDigitalv11.xsd\" Version=\"1.1\" UUID=\"F0D5A2D3-98A0-471E-AA69-EE7EE65A2883\" FechaTimbrado=\"2022-05-15T22:21:39\" RfcProvCertif=\"SPR190613I52\" SelloCFD=\"egRsyOe97Z5CYXE3fENgDovh55a+wiUJrZbtsL8m5epb79yLb8I59PdMzU/wH0w9z3L85O1OeKANjtVJTliwBDhzsRUHsqFU0H/TbeXS0W8EP03WaB7yTGklslVTNqAB0AB+CJiYrTh/n7ckq+zHrtajPouRgaqD6UT7LcLhbbfAYxpJ4k/enNk5JZW4LrurdqR2q5HSwCxGZaS9jM6E9/RRoj4oqSvPElGEmHhFT2NhSy5pPbpSGncYVVrKZ78zXKkvSZ0jN3N7aH0a//T37W7TUAh6zXdCE5K/MqluRdE1xjABPDq0SG4EAp+arUgvmZ1PHJAOm0poy3Sa2eLlWA==\" NoCertificadoSAT=\"30001000000400002495\" SelloSAT=\"qgsTcRmMkJVkt9mdnw+AHGlH/ETFcu2S4OIyE2EmNNq/7r1KltNnUFXWy0Th6O7Qr50ygq3OiX1U9l/WJgHFGhz1Fv4qi6l6vVCi+M4mszbtfK+qkPdjSktVUYOO6Ae5VvYb6H3XkwN37rFl7/MI/qSq2hQjlKlSCCx1NLGRfH93YjMTRjbPIOU2+ufsGjvcStew9jMEPu1KzBZRJvouEFrEHdhbe8TfkBTO0ikR5EltphZhXat2ThWK0TurYJAgxzvby0WdYbyTOf2Vd020urmqHrpmPbjlGetgiRTmCaMGnfOtks+tZcSfJQCiyra/VbIN8TPipo/Eu3xsbBnXNg==\" /><nomina12:Nomina Version=\"1.2\" TipoNomina=\"O\" FechaPago=\"2022-05-15\" FechaInicialPago=\"2022-05-09\" FechaFinalPago=\"2022-05-15\" NumDiasPagados=\"7\" TotalPercepciones=\"1600\" TotalDeducciones=\"300\" TotalOtrosPagos=\"10\"><nomina12:Emisor RegistroPatronal=\"A4914083100\"><nomina12:EntidadSNCF OrigenRecurso=\"IP\" /></nomina12:Emisor><nomina12:Receptor Curp=\"MELH450218MSLNPL03\" NumSeguridadSocial=\"52079004371\" FechaInicioRelLaboral=\"2016-05-31\" Antigüedad=\"P310W\" TipoContrato=\"01\" Sindicalizado=\"No\" TipoJornada=\"01\" TipoRegimen=\"02\" NumEmpleado=\"702\" Departamento=\"SOLDADOR\" RiesgoPuesto=\"1\" PeriodicidadPago=\"02\" SalarioDiarioIntegrado=\"180.00\" ClaveEntFed=\"COL\" /><nomina12:Percepciones TotalGravado=\"300\" TotalExento=\"1300\" TotalSueldos=\"1600\"><nomina12:Percepcion TipoPercepcion=\"002\" Clave=\"43200006\" Concepto=\"Gratificación Anual Aguinaldo\" ImporteGravado=\"0\" ImporteExento=\"500\" /><nomina12:Percepcion TipoPercepcion=\"021\" Clave=\"43200004\" Concepto=\"Prima vacacional\" ImporteGravado=\"0\" ImporteExento=\"500\" /><nomina12:Percepcion TipoPercepcion=\"001\" Clave=\"43200003\" Concepto=\"Vacaciones\" ImporteGravado=\"100\" ImporteExento=\"100\" /><nomina12:Percepcion TipoPercepcion=\"005\" Clave=\"43200014\" Concepto=\"Fondo de ahorro\" ImporteGravado=\"100\" ImporteExento=\"100\" /><nomina12:Percepcion TipoPercepcion=\"010\" Clave=\"43200013\" Concepto=\"p puntualidad\" ImporteGravado=\"100\" ImporteExento=\"100\" /></nomina12:Percepciones><nomina12:Deducciones TotalOtrasDeducciones=\"200\" TotalImpuestosRetenidos=\"100\"><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"50000300\" Concepto=\"Otros\" Importe=\"100\" /><nomina12:Deduccion TipoDeduccion=\"002\" Clave=\"50000301\" Concepto=\"ISR\" Importe=\"100\" /><nomina12:Deduccion TipoDeduccion=\"001\" Clave=\"50000303\" Concepto=\"Imss\" Importe=\"100\" /></nomina12:Deducciones><nomina12:OtrosPagos><nomina12:OtroPago TipoOtroPago=\"002\" Clave=\"11700001\" Concepto=\"Subsidio para el empleo\" Importe=\"10\"><nomina12:SubsidioAlEmpleo SubsidioCausado=\"350\" /></nomina12:OtroPago></nomina12:OtrosPagos></nomina12:Nomina></cfdi:Complemento></cfdi:Comprobante>\r\n",
      "uuid": "F0D5A2D3-98A0-471E-AA69-EE7EE65A2883",
      "msg": "Se timbro el recibo de nomina correctamente.",
      "statusCode": 200
    },
    "row": 0
  },
  "Empleado 2": {
    "errors": false,
    "data": {
      "cadenaOriginal": "||4.0|702|201805|2022-05-15T20:11:39|30001000000400002434|1610.00|300.00|MXN|1310.00|N|01|PUE|20928|EKU9003173C9|ESCUELA KEMPER URGATE SA DE CV|601|CUSC850516316|CESAR OSBALDO CRUZ SOLORZANO|45638|605|CN01|84111505|1|ACT|Pago de nómina|1610|1610.00|300.00|01|1.2|O|2022-05-15|2022-05-09|2022-05-15|7|1600|300|10|A4914083100|IP|CUSC850516MCMSLS03|52079004371|2016-05-31|P310W|01|No|01|02|702|SOLDADOR|3|02|315.00|COL|1600|300|1300|002|43200006|Gratificación Anual Aguinaldo|0|500|021|43200004|Prima vacacional|0|500|001|43200003|Vacaciones|100|100|005|43200014|Fondo de ahorro|100|100|010|43200013|p puntualidad|100|100|200|100|004|50000300|Otros|100|002|50000301|ISR|100|001|50000303|Imss|100|002|11700001|Subsidio para el empleo|10|350||",
      "sello": "LH8RaK/KUL4Fnyon1hKbV75EX97VgFnaWNvwkG+/kQhAF3QbYh85ZiYyzFaUZMQU8HsSemzKCgod6h8k9KoAiiklRLTDE3Lh5ZMNKn07Ql8unrVbu7MOPmnol7/J+8bcY+Qi1ynKrv3E0GCuAZLImMVLPP/kOoOyFm2q0IIySTV0nFhb3Mdq5dMdbBHHcghw1WPW4+n4/biV7HlKjmiTqn/8EAMCUgOchImpZ5q/iC1aiIIHb8EPxzGcxnizXOvvVHKcaar2PLbOe2vsRNjEQWXh+E54IX7RehLXHMiKNAoEvPBzeR41XOWPDEUiLgIzeF1cGkA9QBYI4yXUeisboA==",
      "certificado": "MIIFuzCCA6OgAwIBAgIUMzAwMDEwMDAwMDA0MDAwMDI0MzQwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWRpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMTkwNjE3MTk0NDE0WhcNMjMwNjE3MTk0NDE0WjCB4jEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gWElRQjg5MTExNlFFNDEeMBwGA1UEBRMVIC8gWElRQjg5MTExNk1HUk1aUjA1MR4wHAYDVQQLExVFc2N1ZWxhIEtlbXBlciBVcmdhdGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCN0peKpgfOL75iYRv1fqq+oVYsLPVUR/GibYmGKc9InHFy5lYF6OTYjnIIvmkOdRobbGlCUxORX/tLsl8Ya9gm6Yo7hHnODRBIDup3GISFzB/96R9K/MzYQOcscMIoBDARaycnLvy7FlMvO7/rlVnsSARxZRO8Kz8Zkksj2zpeYpjZIya/369+oGqQk1cTRkHo59JvJ4Tfbk/3iIyf4H/Ini9nBe9cYWo0MnKob7DDt/vsdi5tA8mMtA953LapNyCZIDCRQQlUGNgDqY9/8F5mUvVgkcczsIgGdvf9vMQPSf3jjCiKj7j6ucxl1+FwJWmbvgNmiaUR/0q4m2rm78lFAgMBAAGjHTAbMAwGA1UdEwEB/wQCMAAwCwYDVR0PBAQDAgbAMA0GCSqGSIb3DQEBCwUAA4ICAQBcpj1TjT4jiinIujIdAlFzE6kRwYJCnDG08zSp4kSnShjxADGEXH2chehKMV0FY7c4njA5eDGdA/G2OCTPvF5rpeCZP5Dw504RZkYDl2suRz+wa1sNBVpbnBJEK0fQcN3IftBwsgNFdFhUtCyw3lus1SSJbPxjLHS6FcZZ51YSeIfcNXOAuTqdimusaXq15GrSrCOkM6n2jfj2sMJYM2HXaXJ6rGTEgYmhYdwxWtil6RfZB+fGQ/H9I9WLnl4KTZUS6C9+NLHh4FPDhSk19fpS2S/56aqgFoGAkXAYt9Fy5ECaPcULIfJ1DEbsXKyRdCv3JY89+0MNkOdaDnsemS2o5Gl08zI4iYtt3L40gAZ60NPh31kVLnYNsmvfNxYyKp+AeJtDHyW9w7ftM0Hoi+BuRmcAQSKFV3pk8j51la+jrRBrAUv8blbRcQ5BiZUwJzHFEKIwTsRGoRyEx96sNnB03n6GTwjIGz92SmLdNl95r9rkvp+2m4S6q1lPuXaFg7DGBrXWC8iyqeWE2iobdwIIuXPTMVqQb12m1dAkJVRO5NdHnP/MpqOvOgLqoZBNHGyBg4Gqm4sCJHCxA1c8Elfa2RQTCk0tAzllL4vOnI1GHkGJn65xokGsaU4B4D36xh7eWrfj4/pgWHmtoDAYa8wzSwo2GVCZOs+mtEgOQB91/g==",
      "xml": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\r\n<cfdi:Comprobante xmlns:cfdi=\"http://www.sat.gob.mx/cfd/4\" xmlns:xs=\"http://www.w3.org/2001/XMLSchema\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:nomina12=\"http://www.sat.gob.mx/nomina12\" xsi:schemaLocation=\"http://www.sat.gob.mx/cfd/4 http://www.sat.gob.mx/sitio_internet/cfd/4/cfdv40.xsd http://www.sat.gob.mx/nomina12 http://www.sat.gob.mx/sitio_internet/cfd/nomina/nomina12.xsd\" Version=\"4.0\" Serie=\"702\" Folio=\"201805\" Fecha=\"2022-05-15T20:11:39\" Sello=\"LH8RaK/KUL4Fnyon1hKbV75EX97VgFnaWNvwkG+/kQhAF3QbYh85ZiYyzFaUZMQU8HsSemzKCgod6h8k9KoAiiklRLTDE3Lh5ZMNKn07Ql8unrVbu7MOPmnol7/J+8bcY+Qi1ynKrv3E0GCuAZLImMVLPP/kOoOyFm2q0IIySTV0nFhb3Mdq5dMdbBHHcghw1WPW4+n4/biV7HlKjmiTqn/8EAMCUgOchImpZ5q/iC1aiIIHb8EPxzGcxnizXOvvVHKcaar2PLbOe2vsRNjEQWXh+E54IX7RehLXHMiKNAoEvPBzeR41XOWPDEUiLgIzeF1cGkA9QBYI4yXUeisboA==\" NoCertificado=\"30001000000400002434\" Certificado=\"MIIFuzCCA6OgAwIBAgIUMzAwMDEwMDAwMDA0MDAwMDI0MzQwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWRpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMTkwNjE3MTk0NDE0WhcNMjMwNjE3MTk0NDE0WjCB4jEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gWElRQjg5MTExNlFFNDEeMBwGA1UEBRMVIC8gWElRQjg5MTExNk1HUk1aUjA1MR4wHAYDVQQLExVFc2N1ZWxhIEtlbXBlciBVcmdhdGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCN0peKpgfOL75iYRv1fqq+oVYsLPVUR/GibYmGKc9InHFy5lYF6OTYjnIIvmkOdRobbGlCUxORX/tLsl8Ya9gm6Yo7hHnODRBIDup3GISFzB/96R9K/MzYQOcscMIoBDARaycnLvy7FlMvO7/rlVnsSARxZRO8Kz8Zkksj2zpeYpjZIya/369+oGqQk1cTRkHo59JvJ4Tfbk/3iIyf4H/Ini9nBe9cYWo0MnKob7DDt/vsdi5tA8mMtA953LapNyCZIDCRQQlUGNgDqY9/8F5mUvVgkcczsIgGdvf9vMQPSf3jjCiKj7j6ucxl1+FwJWmbvgNmiaUR/0q4m2rm78lFAgMBAAGjHTAbMAwGA1UdEwEB/wQCMAAwCwYDVR0PBAQDAgbAMA0GCSqGSIb3DQEBCwUAA4ICAQBcpj1TjT4jiinIujIdAlFzE6kRwYJCnDG08zSp4kSnShjxADGEXH2chehKMV0FY7c4njA5eDGdA/G2OCTPvF5rpeCZP5Dw504RZkYDl2suRz+wa1sNBVpbnBJEK0fQcN3IftBwsgNFdFhUtCyw3lus1SSJbPxjLHS6FcZZ51YSeIfcNXOAuTqdimusaXq15GrSrCOkM6n2jfj2sMJYM2HXaXJ6rGTEgYmhYdwxWtil6RfZB+fGQ/H9I9WLnl4KTZUS6C9+NLHh4FPDhSk19fpS2S/56aqgFoGAkXAYt9Fy5ECaPcULIfJ1DEbsXKyRdCv3JY89+0MNkOdaDnsemS2o5Gl08zI4iYtt3L40gAZ60NPh31kVLnYNsmvfNxYyKp+AeJtDHyW9w7ftM0Hoi+BuRmcAQSKFV3pk8j51la+jrRBrAUv8blbRcQ5BiZUwJzHFEKIwTsRGoRyEx96sNnB03n6GTwjIGz92SmLdNl95r9rkvp+2m4S6q1lPuXaFg7DGBrXWC8iyqeWE2iobdwIIuXPTMVqQb12m1dAkJVRO5NdHnP/MpqOvOgLqoZBNHGyBg4Gqm4sCJHCxA1c8Elfa2RQTCk0tAzllL4vOnI1GHkGJn65xokGsaU4B4D36xh7eWrfj4/pgWHmtoDAYa8wzSwo2GVCZOs+mtEgOQB91/g==\" SubTotal=\"1610.00\" Descuento=\"300.00\" Moneda=\"MXN\" Total=\"1310.00\" TipoDeComprobante=\"N\" Exportacion=\"01\" MetodoPago=\"PUE\" LugarExpedicion=\"20928\"><cfdi:Emisor Rfc=\"EKU9003173C9\" Nombre=\"ESCUELA KEMPER URGATE SA DE CV\" RegimenFiscal=\"601\" /><cfdi:Receptor Rfc=\"CUSC850516316\" Nombre=\"CESAR OSBALDO CRUZ SOLORZANO\" DomicilioFiscalReceptor=\"45638\" RegimenFiscalReceptor=\"605\" UsoCFDI=\"CN01\" /><cfdi:Conceptos><cfdi:Concepto ClaveProdServ=\"84111505\" Cantidad=\"1\" ClaveUnidad=\"ACT\" Descripcion=\"Pago de nómina\" ValorUnitario=\"1610\" Importe=\"1610.00\" Descuento=\"300.00\" ObjetoImp=\"01\" /></cfdi:Conceptos><cfdi:Complemento><tfd:TimbreFiscalDigital xmlns:tfd=\"http://www.sat.gob.mx/TimbreFiscalDigital\" xsi:schemaLocation=\"http://www.sat.gob.mx/TimbreFiscalDigital http://www.sat.gob.mx/sitio_internet/cfd/TimbreFiscalDigital/TimbreFiscalDigitalv11.xsd\" Version=\"1.1\" UUID=\"A7CFB796-5649-4F78-8631-625BB88420A7\" FechaTimbrado=\"2022-05-15T22:21:40\" RfcProvCertif=\"SPR190613I52\" SelloCFD=\"LH8RaK/KUL4Fnyon1hKbV75EX97VgFnaWNvwkG+/kQhAF3QbYh85ZiYyzFaUZMQU8HsSemzKCgod6h8k9KoAiiklRLTDE3Lh5ZMNKn07Ql8unrVbu7MOPmnol7/J+8bcY+Qi1ynKrv3E0GCuAZLImMVLPP/kOoOyFm2q0IIySTV0nFhb3Mdq5dMdbBHHcghw1WPW4+n4/biV7HlKjmiTqn/8EAMCUgOchImpZ5q/iC1aiIIHb8EPxzGcxnizXOvvVHKcaar2PLbOe2vsRNjEQWXh+E54IX7RehLXHMiKNAoEvPBzeR41XOWPDEUiLgIzeF1cGkA9QBYI4yXUeisboA==\" NoCertificadoSAT=\"30001000000400002495\" SelloSAT=\"KcTwbwLIO9M93vqneia7qiXm1cBH95yVPcRpTfa69MwVUYyoQH1arjvSkGDcwv5W3Uo3Gc4RtiHiCslvz8lighAJ2oi6GrdfultaVi41n5bvPVMmqwE56bfnQQwwgzizK1TFmyR1kJoc1PaO/O3VfFGcYIXc0R4kHFYgUHlJZjsXhV/NWe8cL1y65QsMSpCk9dtq+yXgxkVvP0jzh30X4WYWiUhItNv61okn50bE0vsCOSdQbQ3Y2HdTh83h+s4FU24sQ0IZ6DYkMk8U0R82JF8PO6YfH0QzYTZ2vDtQv8CUmEF4/jkytEfplcMAV1s1uIwaPjggKpgjTTgj6N91CQ==\" /><nomina12:Nomina Version=\"1.2\" TipoNomina=\"O\" FechaPago=\"2022-05-15\" FechaInicialPago=\"2022-05-09\" FechaFinalPago=\"2022-05-15\" NumDiasPagados=\"7\" TotalPercepciones=\"1600\" TotalDeducciones=\"300\" TotalOtrosPagos=\"10\"><nomina12:Emisor RegistroPatronal=\"A4914083100\"><nomina12:EntidadSNCF OrigenRecurso=\"IP\" /></nomina12:Emisor><nomina12:Receptor Curp=\"CUSC850516MCMSLS03\" NumSeguridadSocial=\"52079004371\" FechaInicioRelLaboral=\"2016-05-31\" Antigüedad=\"P310W\" TipoContrato=\"01\" Sindicalizado=\"No\" TipoJornada=\"01\" TipoRegimen=\"02\" NumEmpleado=\"702\" Departamento=\"SOLDADOR\" RiesgoPuesto=\"3\" PeriodicidadPago=\"02\" SalarioDiarioIntegrado=\"315.00\" ClaveEntFed=\"COL\" /><nomina12:Percepciones TotalGravado=\"300\" TotalExento=\"1300\" TotalSueldos=\"1600\"><nomina12:Percepcion TipoPercepcion=\"002\" Clave=\"43200006\" Concepto=\"Gratificación Anual Aguinaldo\" ImporteGravado=\"0\" ImporteExento=\"500\" /><nomina12:Percepcion TipoPercepcion=\"021\" Clave=\"43200004\" Concepto=\"Prima vacacional\" ImporteGravado=\"0\" ImporteExento=\"500\" /><nomina12:Percepcion TipoPercepcion=\"001\" Clave=\"43200003\" Concepto=\"Vacaciones\" ImporteGravado=\"100\" ImporteExento=\"100\" /><nomina12:Percepcion TipoPercepcion=\"005\" Clave=\"43200014\" Concepto=\"Fondo de ahorro\" ImporteGravado=\"100\" ImporteExento=\"100\" /><nomina12:Percepcion TipoPercepcion=\"010\" Clave=\"43200013\" Concepto=\"p puntualidad\" ImporteGravado=\"100\" ImporteExento=\"100\" /></nomina12:Percepciones><nomina12:Deducciones TotalOtrasDeducciones=\"200\" TotalImpuestosRetenidos=\"100\"><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"50000300\" Concepto=\"Otros\" Importe=\"100\" /><nomina12:Deduccion TipoDeduccion=\"002\" Clave=\"50000301\" Concepto=\"ISR\" Importe=\"100\" /><nomina12:Deduccion TipoDeduccion=\"001\" Clave=\"50000303\" Concepto=\"Imss\" Importe=\"100\" /></nomina12:Deducciones><nomina12:OtrosPagos><nomina12:OtroPago TipoOtroPago=\"002\" Clave=\"11700001\" Concepto=\"Subsidio para el empleo\" Importe=\"10\"><nomina12:SubsidioAlEmpleo SubsidioCausado=\"350\" /></nomina12:OtroPago></nomina12:OtrosPagos></nomina12:Nomina></cfdi:Complemento></cfdi:Comprobante>\r\n",
      "uuid": "A7CFB796-5649-4F78-8631-625BB88420A7",
      "msg": "Se timbro el recibo de nomina correctamente.",
      "statusCode": 200
    },
    "row": 1
  }
}

```

### Ejemplo 3 de petición

```php
  curl https://development.kubox.mx/v2/timbre/nomina40 \
     -H "Content-type: application/json" \
     -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0L2ZhY3R1cmFydGViYXJhdG8vcHVibGljL3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg3NzM2MTAsImV4cCI6MTUwODc5NTIxMCwibmJmIjoxNTA4NzczNjEwLCJqdGkiOiJIcUZPbDlWSWZSYk53N3ZqIiwic3ViIjo4NX0.GEqizwFutuibe_RYUXh3i0sOmK-PDRKK88tJBSTyJr4' \
     -X POST -d '{
  "data": [
    {
      "serie":"3822",
      "folio":"00025152269",
      "noEmpleado":"251",
      "nombre":"MARIA OLIVIA MARTINEZ SAGAZ",
      "rfc":"MASO451221PM4",
      "curp":"MASO451221HCMLDB11",
      "cp":"80290",
      "claveEntFed":"COL",
      "departamento":"PENSIONADOS Y JUBILADOS SINDICALIZADOS",
      "sdi":"315",
      "diasPago":"7",
      "ex_FechaInicioRelLaboral":"2020-01-01",
      "ex_RiesgoPuesto":"1",
      "ex_TipoJornada":"01",
      "seguro_social":"52079004371",
      "tipoContrato":"01",
      "tipoRegimen":"02",

      "pe_sueldo_clave": ["43200001", "43200002"],
      "pe_sueldo_concepto": ["Sueldo", "Vacaciones"],
      "pe_sueldo_excento": [0, 50],
      "pe_sueldo_gravado": [200, 100],
      "pe_otros_ingresos_salarios_clave":[ "0049", "202", "0027"],
      "pe_otros_ingresos_salarios_concepto":[ "APORTACION FONDO DE AHORRO", "APORTAC. 5% AUTOF. VIVI", "RETROACTIVO"],
      "pe_otros_ingresos_salarios_excento":[ 0, 0, 0],
      "pe_otros_ingresos_salarios_gravado":[ 233.6, 111.8, 4724.21],

      "de_otros_clave":[ "0008", "0052", "202", "0140", "0130", "0131"],
      "de_otros_concepto":[ "CUOTA SINDICAL", "FONDO DE AHORRO", "APORT. 5% FONDO AUTOF. VIV ", "APORTACION FONDO DE AHORRO ", "FONDO AUTOFINANCIAMIENTO VIVIENDA ", "5% FONDO AUTOFINANC. VIVIENDA "],
      "de_otros_importe":[ 44.72, 223.6, 111.8, 223.6, 246.86, 111.8],
      "de_isr_clave": "50000301",
      "de_isr_concepto": "ISR",
      "de_isr_importe": 100,

      "top_subsidio_empleo_clave": "11700001",
      "top_subsidio_empleo_concepto": "Subsidio para el empleo",
      "top_subsidio_empleo_causado": 0,
      "top_subsidio_empleo_importe": 0,

      "total":4357.23
    }
  ],
  "emisor": {
    "nombreFiscal": "ESCUELA KEMPER URGATE",
    "rfc": "EKU9003173C9",
    "regimenFiscal": "601",
    "curp": "",
    "cp": "20928",
    "cer": "LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0tLS0KTUlJQklqQU5CZ2txaGtpRzl3MEJBUUVGQUFPQ0FROEFNSUlCQ2dLQ0FRRUF0bWVjTzZuMkdTMHpMMDI1Z2JIRwpRVnh6blBESUNvWHpSMnVVbmd6NERxeFZVQy93OWNFNkZ4U2lYbTJhcDhHY2pnN3dtY1pmbTg1RUJheEN4LzBKCjJ1NUNxbmh6SW9HQ2RoQlB1aFdRbkloNVRMZ2ovWDZ1TnF1d1prS0NoYk5lOWFlRmlyVS9KYnlON0VnaWE5b0sKSDlLWlVzb2RpTS9wV0FIMDBQQ3RvS0o5T0JjU0hNcThScWEzS0tvQmNma2cxWnJndWVmZndSTHdzOXlPY1JXTApiMDJzRE9QekdJbS9qRUZpY1ZZdDJIdzFxZFJFNXhtVFo3QUdHMFVIcyt1bmtHanBDVmVKK0JFQm4wSlBMV1Z2CkRLSFpBUU1qNnM1Qmt1MzUrZC9NeUFUa3BPUHNHVC9WVG5zb3V4ZWtEZmlrSkQxZjdBMVpwSmJxRHBrSm5zczMKdlFJREFRQUIKLS0tLS1FTkQgUFVCTElDIEtFWS0tLS0tCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQpNSUlGc0RDQ0E1aWdBd0lCQWdJVU16QXdNREV3TURBd01EQTFNREF3TURNME1UWXdEUVlKS29aSWh2Y05BUUVMCkJRQXdnZ0VyTVE4d0RRWURWUVFEREFaQlF5QlZRVlF4TGpBc0JnTlZCQW9NSlZORlVsWkpRMGxQSUVSRklFRkUKVFVsT1NWTlVVa0ZEU1U5T0lGUlNTVUpWVkVGU1NVRXhHakFZQmdOVkJBc01FVk5CVkMxSlJWTWdRWFYwYUc5eQphWFI1TVNnd0pnWUpLb1pJaHZjTkFRa0JGaGx2YzJOaGNpNXRZWEowYVc1bGVrQnpZWFF1WjI5aUxtMTRNUjB3Ckd3WURWUVFKREJRemNtRWdZMlZ5Y21Ga1lTQmtaU0JqWVd4cGVqRU9NQXdHQTFVRUVRd0ZNRFl6TnpBeEN6QUoKQmdOVkJBWVRBazFZTVJrd0Z3WURWUVFJREJCRFNWVkVRVVFnUkVVZ1RVVllTVU5QTVJFd0R3WURWUVFIREFoRApUMWxQUVVOQlRqRVJNQThHQTFVRUxSTUlNaTQxTGpRdU5EVXhKVEFqQmdrcWhraUc5dzBCQ1FJVEZuSmxjM0J2CmJuTmhZbXhsT2lCQlEwUk5RUzFUUVZRd0hoY05Nak13TlRFNE1URTBNelV4V2hjTk1qY3dOVEU0TVRFME16VXgKV2pDQjF6RW5NQ1VHQTFVRUF4TWVSVk5EVlVWTVFTQkxSVTFRUlZJZ1ZWSkhRVlJGSUZOQklFUkZJRU5XTVNjdwpKUVlEVlFRcEV4NUZVME5WUlV4QklFdEZUVkJGVWlCVlVrZEJWRVVnVTBFZ1JFVWdRMVl4SnpBbEJnTlZCQW9UCkhrVlRRMVZGVEVFZ1MwVk5VRVZTSUZWU1IwRlVSU0JUUVNCRVJTQkRWakVsTUNNR0ExVUVMUk1jUlV0Vk9UQXcKTXpFM00wTTVJQzhnVmtGRVFUZ3dNRGt5TjBSS016RWVNQndHQTFVRUJSTVZJQzhnVmtGRVFUZ3dNRGt5TjBoVApVbE5TVERBMU1STXdFUVlEVlFRTEV3cFRkV04xY25OaGJDQXhNSUlCSWpBTkJna3Foa2lHOXcwQkFRRUZBQU9DCkFROEFNSUlCQ2dLQ0FRRUF0bWVjTzZuMkdTMHpMMDI1Z2JIR1FWeHpuUERJQ29YelIydVVuZ3o0RHF4VlVDL3cKOWNFNkZ4U2lYbTJhcDhHY2pnN3dtY1pmbTg1RUJheEN4LzBKMnU1Q3FuaHpJb0dDZGhCUHVoV1FuSWg1VExnagovWDZ1TnF1d1prS0NoYk5lOWFlRmlyVS9KYnlON0VnaWE5b0tIOUtaVXNvZGlNL3BXQUgwMFBDdG9LSjlPQmNTCkhNcThScWEzS0tvQmNma2cxWnJndWVmZndSTHdzOXlPY1JXTGIwMnNET1B6R0ltL2pFRmljVll0Mkh3MXFkUkUKNXhtVFo3QUdHMFVIcyt1bmtHanBDVmVKK0JFQm4wSlBMV1Z2REtIWkFRTWo2czVCa3UzNStkL015QVRrcE9QcwpHVC9WVG5zb3V4ZWtEZmlrSkQxZjdBMVpwSmJxRHBrSm5zczN2UUlEQVFBQm94MHdHekFNQmdOVkhSTUJBZjhFCkFqQUFNQXNHQTFVZER3UUVBd0lHd0RBTkJna3Foa2lHOXcwQkFRc0ZBQU9DQWdFQUZhVWdqNVBxZ3ZKaWdOTWcKdHJkWFpuYlBmVkJidWtBYlc0T0duVWhOckE3U1JBQWZ2MkJTR2sxNlBJMG5CT3I3cUYybUl0bUJuamdFd2srRApUdjhacjd3NXFwN3ZsZUM2ZElzWkZOSm9hNlpuZHJFL2Y3S08xQ1lydUxYcjVnd0VrSXlHZko5Tnd5SWFndkhICk1zenp5SGlTWklBODUwZld0YnF0eXRocEFsaUoyakYzNU01cE5TK1lUa1JCK1Q2TC9jNm0wMHltTjNxOWxUMXIKQjAzWXl3eHJMcmVSU0ZaT1NyYndXZmczNEVKYkhmYkZYcENTVllkSlJmaVZkdkhuZXdOMHI1ZlVsUHRSOXN0UQpIeXVxZXd6ZGt5YjVqVFR3MDJEMmNVZkw1N3ZsUFN0Qmo3U0VpM3VPV3ZMcnNpRG5uQ0l4Uk1ZSjJVQTJrdERLCkhrK3pXbnNEbWFlbGVTem9udjJDSFc0MnlYWVBDdldpODhvRTFESk5ZTE5rSWp1YTdNeEFua05aYlNjTncwMUEKNnpiTHNaM3k4RzZlRVlueFNUUmZ3amQ4RVA0a2RpSE5KZnRtN1o0aVJVN0hPVmg3OS9sUldCK2dkMTcxczNkLwptSTlrdGUzTVJ5NlY4TU1FTUNBbk1ib0dwYW9vWXdnQW13Y2xJMlhaQ2N6TldYZmhhV2UwWlM1UG15dEQvR0RwClh6a1gwb0VnWTlLL3VZbzVWNzdOZFpiR0FqbXlpOGNFMkIyb2d2eWFOMlhmSUluclpQZ0VmZko0QUI3a0ZBMm0Kd2VzZExPQ2gwQkxEOWl0bUN2ZTNBMUZHUjQrc3RPMkFOVW9pSTN3M1R2MnlRU2c0YmplRGxKMDhsWGFhRkNMVwoycGVFWE1YalFVazdmbXBiNU1OdU9VVFc2QkU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K",
    "key": "LS0tLS1CRUdJTiBFTkNSWVBURUQgUFJJVkFURSBLRVktLS0tLQpNSUlGSERCT0Jna3Foa2lHOXcwQkJRMHdRVEFwQmdrcWhraUc5dzBCQlF3d0hBUUlFTE5IbVJKcHQ5TUNBZ2dBCk1Bd0dDQ3FHU0liM0RRSUpCUUF3RkFZSUtvWklodmNOQXdjRUNPb3JQei8yeXhqdUJJSUV5QlNobjZpTTZxWUMKWExacUhUU0hjK0ZBbzNNdmNqdXQzRnkxQXdDZ1BYK29YVkprdjE2QVVKWFFiNWlpVUd6UzBXOE0zR3JTMysyaApzbXFKbTdQcHpQdmxhWmU4RkhRaW5yc3hvRnBOUTlFcnhtNlFiUlBvSmdwbWljbWk2dE1jQjFUYWt4Q05iZHFnCklJQWF6cHJtUTNxSWRtR1lVWUZWN1h5OGxzTWhpeXBJSXFlZzRoUFhwWi9hNUI5bXFHNEVQcjJrTGFyWmwvejcKY01Rb0hUVVpZMGFEa2hKb3ZBNnJ3T2RJeWx0YjhZcUpsTGQzWk10cjRUNXByNEcrb3BBcWYzd0l5QWN3S0N6MQo5K21FNUFqdkQ0ejFKMmlFL2VqZnB0TDVhRTNGOWltZys0UXJkK05IWjZZSUxPM3NnZ1hPWEVXZCtWVG84UHpVCitvMWsyc3dGdHJNUk14dUsyWEdhRi9idGVRQkhrWlVqd01LRlQzU0d1YkxqTytKaW52T0hTZmUxbGRJVHRuTmcKOGxBN3lvZnJVbU9UL2dBR1hIZnlaQm90d3EvcTk3YjZIWTFCTHF5WXV1Wmc1dmdsckNoL1QvUlBLYm9kWjd6ZgorS0E0ajRPUlpHbzBXc0NReE51STNDdkZUWUlzWWlPQnBiUjdobEZaMlRyeUsvM1lpMGFxd0o4T0drK1hDdHZLCkxvS3dLQ2dPQjZISG9oR2Mvemxya0Fhd2hXVDU0UXB0V1BBVFQ4Tkl3KzRFN1I4dDlXS0RMTkFBS2NUTTFwS0kKRklrWUp1aUJuUy9UYmpQSnN4VDh0UTMvcm1WRm5XU1hVMTMzeENxMFZubVl2UjRKdCszU0xBdVFDVzdCcElENgprbnB4MlExZUUwUG9ucTBUeXNNdmNkSHEwR1pNWmFxN09vczMzMXBoaDNBbEZvMXpETVRqNENsRlZQNTltRnY0CnRtTTVxY0kzcFFTRTRRWTlESUVWMzYwa3J2Qk15dGFwVUM5SHNwZjB6bGp2Q1F2VDVSajVvMU1LMlZvMko5UnkKTzhFcWtkdThPdnQ5Wjh3Y0ZLSnJaRG0yQTBqTmx1dnhhNS9hNEFUK3pWeEMzNGZFWWhTOUxqa2pWbEJKY0FyUwpjdWtjSDZiUmNwVXc5WU5mSytBQ3NLbWNwbVVJM1BHQkI4V09KZHR4aVNHd09QZG5yTmI2Z3ZOSW5UTXppa1E5CnN3aDJvQ2h0WW92RDFpRGJMd1ZRbTVOWW5HZmtTR2ZsbzhrK3NXR3R4aEE4L3UxYU5QbUVVcFRwYU9pcEM3UUQKc0pVK3l6VFdBajkySUp6WVlkV243dDJHNEJFSGRkQWhtdThYNW5yMG1SbzdxcHFQV1c5OFozZXZGOTlHRHE3agpmUDdMdEtzOHR1cmtaelJiMDhHbHdpU29OM0lKRWljNE9RaG9qZDBVaUpaYlE2a0hFQ0k5MG5SODBJV1BEN3B0CmROeFB3MGtpbzJKckc4bzkrV2VaR081YnprRW9wT2dOR25UTmNuZWRkNHdWYnhmTnNKN0xKVFNocFdLdG1GaHUKQ3hGSTR6dWxPZEt0OGUxK0JicmM5eTROdXpyTE5NVVkrNjB5bWhSV3BJTlpEVStQWkpaRUlNNFBLZDU0RXcrZAozK05MMWMzbEdERW82SEc4Z3NWaXY1WVN4VGJIdHZLUFFNY0h1YVUrQnQ2TnFyUTNRRDBRb2dvVHZDYXQzODk3Clc5WlVPSWpNbkxOeVcxbnF0Q2JTRGNEa25TSXVGT3grUW1IR0pHSmVZa0Q4NjlvamU2QnhmNUUxamE2QXREMXkKL3hveVhVcFRsclpqSFFKZU92SEpCZGZhTjhGa3U5cHZJYTlkVVFtalJydk02MGtHUFlqa2hmU1hIRFZYWHV3MwpGRHFINlBUVFg5K281OGZBdHdZSzd4YlM3SjEyOFRJNEYzdElBVm0zeFF1ajBmUUZtOTVzWFpXbVlhQ21rODBCCmEwSXlGbmpNamtERVF2cThZLy82STA0andveTRhT1MwV0J1cGQ0WlJnclBsRmNOTHEyZStxR1Rjc3h0L2pZT2sKWWUzMkd3SzlpMjFqTk5yanJVajRxcWF1V2ZsRU1XaTM3cGk5Z1hLdTVrTUt6OC9CNGNBRVA2NHdsOVJ4S3hSbQprWmtlUWdiZGhES1ByUUp2VHloTytRPT0KLS0tLS1FTkQgRU5DUllQVEVEIFBSSVZBVEUgS0VZLS0tLS0K"
  },
  "fechaFinalPago": "2026-01-10",
  "fechaInicialPago": "2026-01-05",
  "fechaPago": "2026-01-11",
  "noCertificado": "30001000000500003416",
  "periodicidadPago": "02",
  "registroPatronal": "A4914083100",
  "tipoNomina": "O",
  "origenRecurso": "IP"
}'
```

### Respuesta 3

Retorna un objeto con la información de la cadena original, el sello, certificado, xml, UUID y un mensaje.

```json

{
    "Empleado 1": {
        "errors": false,
        "data": {
            "cadenaOriginal": "||4.0|3822|00025152269|2026-01-10T06:34:18|30001000000500003416|5419.61|1062.38|MXN|4357.23|N|01|PUE|20928|EKU9003173C9|ESCUELA KEMPER URGATE|601|MASO451221PM4|MARIA OLIVIA MARTINEZ SAGAZ|80290|605|CN01|84111505|1|ACT|Pago de nómina|5419.61|5419.610000|1062.380000|01|1.2|O|2026-01-11|2026-01-05|2026-01-10|7|5419.61|1062.38|0|A4914083100|IP|MASO451221HCMLDB11|52079004371|2020-01-01|P314W|01|No|01|02|251|PENSIONADOS Y JUBILADOS SINDICALIZADOS|1|02|315.00|COL|5419.61|5369.61|50|001|43200001|Sueldo|200|0|001|43200002|Vacaciones|100|50|038|0049|APORTACION FONDO DE AHORRO|233.6|0|038|202|APORTAC. 5% AUTOF. VIVI|111.8|0|038|0027|RETROACTIVO|4724.21|0|962.38|100|004|0008|CUOTA SINDICAL|44.72|004|0052|FONDO DE AHORRO|223.6|004|202|APORT. 5% FONDO AUTOF. VIV|111.8|004|0140|APORTACION FONDO DE AHORRO|223.6|004|0130|FONDO AUTOFINANCIAMIENTO VIVIENDA|246.86|004|0131|5% FONDO AUTOFINANC. VIVIENDA|111.8|002|50000301|ISR|100|002|11700001|Subsidio para el empleo|0|0||",
            "sello": "KpQdo1Ww/UWPru1X2IeGrynP+3KKELZAIc1NC5MNLPTTzTNhb/PfSxiCPyGltgx4b0KIPGjyFIS4AlAuTTwPG2I3yau2/tHGgJqvwkRJw2OFWnalRJLB/4DECKnYk6lEgKUMcttul9z+cFwwwmzmh06/ObwOSbv6BK/bu86hGAoswFk1lONxZX0TZgkpQmBKc28PxwaGpeDOtBCXqbtZCnkenhavqlvTPw1k6XzDXfFW1pKahKdjh0DjkY867aT21y3U5he1BKH8HXLIZdvWIOJWXL6I/Eul5RDwQJfgUTsjMZRXf9Helku9GnzQirZJTxoy/+mItRCHldEqAoiWvg==",
            "certificado": "MIIFsDCCA5igAwIBAgIUMzAwMDEwMDAwMDA1MDAwMDM0MTYwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWxpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMjMwNTE4MTE0MzUxWhcNMjcwNTE4MTE0MzUxWjCB1zEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gVkFEQTgwMDkyN0RKMzEeMBwGA1UEBRMVIC8gVkFEQTgwMDkyN0hTUlNSTDA1MRMwEQYDVQQLEwpTdWN1cnNhbCAxMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtmecO6n2GS0zL025gbHGQVxznPDICoXzR2uUngz4DqxVUC/w9cE6FxSiXm2ap8Gcjg7wmcZfm85EBaxCx/0J2u5CqnhzIoGCdhBPuhWQnIh5TLgj/X6uNquwZkKChbNe9aeFirU/JbyN7Egia9oKH9KZUsodiM/pWAH00PCtoKJ9OBcSHMq8Rqa3KKoBcfkg1ZrgueffwRLws9yOcRWLb02sDOPzGIm/jEFicVYt2Hw1qdRE5xmTZ7AGG0UHs+unkGjpCVeJ+BEBn0JPLWVvDKHZAQMj6s5Bku35+d/MyATkpOPsGT/VTnsouxekDfikJD1f7A1ZpJbqDpkJnss3vQIDAQABox0wGzAMBgNVHRMBAf8EAjAAMAsGA1UdDwQEAwIGwDANBgkqhkiG9w0BAQsFAAOCAgEAFaUgj5PqgvJigNMgtrdXZnbPfVBbukAbW4OGnUhNrA7SRAAfv2BSGk16PI0nBOr7qF2mItmBnjgEwk+DTv8Zr7w5qp7vleC6dIsZFNJoa6ZndrE/f7KO1CYruLXr5gwEkIyGfJ9NwyIagvHHMszzyHiSZIA850fWtbqtythpAliJ2jF35M5pNS+YTkRB+T6L/c6m00ymN3q9lT1rB03YywxrLreRSFZOSrbwWfg34EJbHfbFXpCSVYdJRfiVdvHnewN0r5fUlPtR9stQHyuqewzdkyb5jTTw02D2cUfL57vlPStBj7SEi3uOWvLrsiDnnCIxRMYJ2UA2ktDKHk+zWnsDmaeleSzonv2CHW42yXYPCvWi88oE1DJNYLNkIjua7MxAnkNZbScNw01A6zbLsZ3y8G6eEYnxSTRfwjd8EP4kdiHNJftm7Z4iRU7HOVh79/lRWB+gd171s3d/mI9kte3MRy6V8MMEMCAnMboGpaooYwgAmwclI2XZCczNWXfhaWe0ZS5PmytD/GDpXzkX0oEgY9K/uYo5V77NdZbGAjmyi8cE2B2ogvyaN2XfIInrZPgEffJ4AB7kFA2mwesdLOCh0BLD9itmCve3A1FGR4+stO2ANUoiI3w3Tv2yQSg4bjeDlJ08lXaaFCLW2peEXMXjQUk7fmpb5MNuOUTW6BE=",
            "xml": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\r\n<cfdi:Comprobante xmlns:cfdi=\"http://www.sat.gob.mx/cfd/4\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:nomina12=\"http://www.sat.gob.mx/nomina12\" xsi:schemaLocation=\"http://www.sat.gob.mx/cfd/4 http://www.sat.gob.mx/sitio_internet/cfd/4/cfdv40.xsd http://www.sat.gob.mx/nomina12 http://www.sat.gob.mx/sitio_internet/cfd/nomina/nomina12.xsd\" Version=\"4.0\" Serie=\"3822\" Folio=\"00025152269\" Fecha=\"2026-01-10T06:34:18\" Sello=\"KpQdo1Ww/UWPru1X2IeGrynP+3KKELZAIc1NC5MNLPTTzTNhb/PfSxiCPyGltgx4b0KIPGjyFIS4AlAuTTwPG2I3yau2/tHGgJqvwkRJw2OFWnalRJLB/4DECKnYk6lEgKUMcttul9z+cFwwwmzmh06/ObwOSbv6BK/bu86hGAoswFk1lONxZX0TZgkpQmBKc28PxwaGpeDOtBCXqbtZCnkenhavqlvTPw1k6XzDXfFW1pKahKdjh0DjkY867aT21y3U5he1BKH8HXLIZdvWIOJWXL6I/Eul5RDwQJfgUTsjMZRXf9Helku9GnzQirZJTxoy/+mItRCHldEqAoiWvg==\" NoCertificado=\"30001000000500003416\" Certificado=\"MIIFsDCCA5igAwIBAgIUMzAwMDEwMDAwMDA1MDAwMDM0MTYwDQYJKoZIhvcNAQELBQAwggErMQ8wDQYDVQQDDAZBQyBVQVQxLjAsBgNVBAoMJVNFUlZJQ0lPIERFIEFETUlOSVNUUkFDSU9OIFRSSUJVVEFSSUExGjAYBgNVBAsMEVNBVC1JRVMgQXV0aG9yaXR5MSgwJgYJKoZIhvcNAQkBFhlvc2Nhci5tYXJ0aW5lekBzYXQuZ29iLm14MR0wGwYDVQQJDBQzcmEgY2VycmFkYSBkZSBjYWxpejEOMAwGA1UEEQwFMDYzNzAxCzAJBgNVBAYTAk1YMRkwFwYDVQQIDBBDSVVEQUQgREUgTUVYSUNPMREwDwYDVQQHDAhDT1lPQUNBTjERMA8GA1UELRMIMi41LjQuNDUxJTAjBgkqhkiG9w0BCQITFnJlc3BvbnNhYmxlOiBBQ0RNQS1TQVQwHhcNMjMwNTE4MTE0MzUxWhcNMjcwNTE4MTE0MzUxWjCB1zEnMCUGA1UEAxMeRVNDVUVMQSBLRU1QRVIgVVJHQVRFIFNBIERFIENWMScwJQYDVQQpEx5FU0NVRUxBIEtFTVBFUiBVUkdBVEUgU0EgREUgQ1YxJzAlBgNVBAoTHkVTQ1VFTEEgS0VNUEVSIFVSR0FURSBTQSBERSBDVjElMCMGA1UELRMcRUtVOTAwMzE3M0M5IC8gVkFEQTgwMDkyN0RKMzEeMBwGA1UEBRMVIC8gVkFEQTgwMDkyN0hTUlNSTDA1MRMwEQYDVQQLEwpTdWN1cnNhbCAxMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtmecO6n2GS0zL025gbHGQVxznPDICoXzR2uUngz4DqxVUC/w9cE6FxSiXm2ap8Gcjg7wmcZfm85EBaxCx/0J2u5CqnhzIoGCdhBPuhWQnIh5TLgj/X6uNquwZkKChbNe9aeFirU/JbyN7Egia9oKH9KZUsodiM/pWAH00PCtoKJ9OBcSHMq8Rqa3KKoBcfkg1ZrgueffwRLws9yOcRWLb02sDOPzGIm/jEFicVYt2Hw1qdRE5xmTZ7AGG0UHs+unkGjpCVeJ+BEBn0JPLWVvDKHZAQMj6s5Bku35+d/MyATkpOPsGT/VTnsouxekDfikJD1f7A1ZpJbqDpkJnss3vQIDAQABox0wGzAMBgNVHRMBAf8EAjAAMAsGA1UdDwQEAwIGwDANBgkqhkiG9w0BAQsFAAOCAgEAFaUgj5PqgvJigNMgtrdXZnbPfVBbukAbW4OGnUhNrA7SRAAfv2BSGk16PI0nBOr7qF2mItmBnjgEwk+DTv8Zr7w5qp7vleC6dIsZFNJoa6ZndrE/f7KO1CYruLXr5gwEkIyGfJ9NwyIagvHHMszzyHiSZIA850fWtbqtythpAliJ2jF35M5pNS+YTkRB+T6L/c6m00ymN3q9lT1rB03YywxrLreRSFZOSrbwWfg34EJbHfbFXpCSVYdJRfiVdvHnewN0r5fUlPtR9stQHyuqewzdkyb5jTTw02D2cUfL57vlPStBj7SEi3uOWvLrsiDnnCIxRMYJ2UA2ktDKHk+zWnsDmaeleSzonv2CHW42yXYPCvWi88oE1DJNYLNkIjua7MxAnkNZbScNw01A6zbLsZ3y8G6eEYnxSTRfwjd8EP4kdiHNJftm7Z4iRU7HOVh79/lRWB+gd171s3d/mI9kte3MRy6V8MMEMCAnMboGpaooYwgAmwclI2XZCczNWXfhaWe0ZS5PmytD/GDpXzkX0oEgY9K/uYo5V77NdZbGAjmyi8cE2B2ogvyaN2XfIInrZPgEffJ4AB7kFA2mwesdLOCh0BLD9itmCve3A1FGR4+stO2ANUoiI3w3Tv2yQSg4bjeDlJ08lXaaFCLW2peEXMXjQUk7fmpb5MNuOUTW6BE=\" SubTotal=\"5419.61\" Descuento=\"1062.38\" Moneda=\"MXN\" Total=\"4357.23\" TipoDeComprobante=\"N\" Exportacion=\"01\" MetodoPago=\"PUE\" LugarExpedicion=\"20928\"><cfdi:Emisor Rfc=\"EKU9003173C9\" Nombre=\"ESCUELA KEMPER URGATE\" RegimenFiscal=\"601\" /><cfdi:Receptor Rfc=\"MASO451221PM4\" Nombre=\"MARIA OLIVIA MARTINEZ SAGAZ\" DomicilioFiscalReceptor=\"80290\" RegimenFiscalReceptor=\"605\" UsoCFDI=\"CN01\" /><cfdi:Conceptos><cfdi:Concepto ClaveProdServ=\"84111505\" Cantidad=\"1\" ClaveUnidad=\"ACT\" Descripcion=\"Pago de nómina\" ValorUnitario=\"5419.61\" Importe=\"5419.610000\" Descuento=\"1062.380000\" ObjetoImp=\"01\" /></cfdi:Conceptos><cfdi:Complemento><tfd:TimbreFiscalDigital xmlns:tfd=\"http://www.sat.gob.mx/TimbreFiscalDigital\" xsi:schemaLocation=\"http://www.sat.gob.mx/TimbreFiscalDigital http://www.sat.gob.mx/sitio_internet/cfd/TimbreFiscalDigital/TimbreFiscalDigitalv11.xsd\" Version=\"1.1\" UUID=\"7727C59C-A3B2-4E55-93CE-A9A82B87882F\" FechaTimbrado=\"2026-01-10T08:44:20\" RfcProvCertif=\"SPR190613I52\" SelloCFD=\"KpQdo1Ww/UWPru1X2IeGrynP+3KKELZAIc1NC5MNLPTTzTNhb/PfSxiCPyGltgx4b0KIPGjyFIS4AlAuTTwPG2I3yau2/tHGgJqvwkRJw2OFWnalRJLB/4DECKnYk6lEgKUMcttul9z+cFwwwmzmh06/ObwOSbv6BK/bu86hGAoswFk1lONxZX0TZgkpQmBKc28PxwaGpeDOtBCXqbtZCnkenhavqlvTPw1k6XzDXfFW1pKahKdjh0DjkY867aT21y3U5he1BKH8HXLIZdvWIOJWXL6I/Eul5RDwQJfgUTsjMZRXf9Helku9GnzQirZJTxoy/+mItRCHldEqAoiWvg==\" NoCertificadoSAT=\"30001000000500003456\" SelloSAT=\"TKDZsTh6+sxXC5K0yz+hF6z44eDmRK2s6UKB5mjbxwwXPYAXRmnIfiSA7fUC3fG/WcaY7/aLj1hkVQ2RHWVYhIIWxLlfnHZEo4qqaQdPuEvdJD8Bp7jqFCM4w3w8BkUGw2a2CZ4P9h1xcVnCxtSvSq/wOlnlHVC2u0eQdzR9d/SkWfsRrrc/kY/K85wXrmVKg8M0Vy07wyRg34xolskdQZUiZMIuOYu60Gmq9J5BsBNv3xrGZHypyhejXgFpNwnsmjThdCrhV2kAepxHwOtNMnIRbUIwKmPLKEjagn4uauNxoO9k7Eyb766W9yEx/AhiKl0ktOJJio+mVSRFpjJQ5A==\" /><nomina12:Nomina Version=\"1.2\" TipoNomina=\"O\" FechaPago=\"2026-01-11\" FechaInicialPago=\"2026-01-05\" FechaFinalPago=\"2026-01-10\" NumDiasPagados=\"7\" TotalPercepciones=\"5419.61\" TotalDeducciones=\"1062.38\" TotalOtrosPagos=\"0\"><nomina12:Emisor RegistroPatronal=\"A4914083100\"><nomina12:EntidadSNCF OrigenRecurso=\"IP\" /></nomina12:Emisor><nomina12:Receptor Curp=\"MASO451221HCMLDB11\" NumSeguridadSocial=\"52079004371\" FechaInicioRelLaboral=\"2020-01-01\" Antigüedad=\"P314W\" TipoContrato=\"01\" Sindicalizado=\"No\" TipoJornada=\"01\" TipoRegimen=\"02\" NumEmpleado=\"251\" Departamento=\"PENSIONADOS Y JUBILADOS SINDICALIZADOS\" RiesgoPuesto=\"1\" PeriodicidadPago=\"02\" SalarioDiarioIntegrado=\"315.00\" ClaveEntFed=\"COL\" /><nomina12:Percepciones TotalGravado=\"5369.61\" TotalExento=\"50\" TotalSueldos=\"5419.61\"><nomina12:Percepcion TipoPercepcion=\"001\" Clave=\"43200001\" Concepto=\"Sueldo\" ImporteGravado=\"200\" ImporteExento=\"0\" /><nomina12:Percepcion TipoPercepcion=\"001\" Clave=\"43200002\" Concepto=\"Vacaciones\" ImporteGravado=\"100\" ImporteExento=\"50\" /><nomina12:Percepcion TipoPercepcion=\"038\" Clave=\"0049\" Concepto=\"APORTACION FONDO DE AHORRO\" ImporteGravado=\"233.6\" ImporteExento=\"0\" /><nomina12:Percepcion TipoPercepcion=\"038\" Clave=\"202\" Concepto=\"APORTAC. 5% AUTOF. VIVI\" ImporteGravado=\"111.8\" ImporteExento=\"0\" /><nomina12:Percepcion TipoPercepcion=\"038\" Clave=\"0027\" Concepto=\"RETROACTIVO\" ImporteGravado=\"4724.21\" ImporteExento=\"0\" /></nomina12:Percepciones><nomina12:Deducciones TotalOtrasDeducciones=\"962.38\" TotalImpuestosRetenidos=\"100\"><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"0008\" Concepto=\"CUOTA SINDICAL\" Importe=\"44.72\" /><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"0052\" Concepto=\"FONDO DE AHORRO\" Importe=\"223.6\" /><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"202\" Concepto=\"APORT. 5% FONDO AUTOF. VIV \" Importe=\"111.8\" /><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"0140\" Concepto=\"APORTACION FONDO DE AHORRO \" Importe=\"223.6\" /><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"0130\" Concepto=\"FONDO AUTOFINANCIAMIENTO VIVIENDA \" Importe=\"246.86\" /><nomina12:Deduccion TipoDeduccion=\"004\" Clave=\"0131\" Concepto=\"5% FONDO AUTOFINANC. VIVIENDA \" Importe=\"111.8\" /><nomina12:Deduccion TipoDeduccion=\"002\" Clave=\"50000301\" Concepto=\"ISR\" Importe=\"100\" /></nomina12:Deducciones><nomina12:OtrosPagos><nomina12:OtroPago TipoOtroPago=\"002\" Clave=\"11700001\" Concepto=\"Subsidio para el empleo\" Importe=\"0\"><nomina12:SubsidioAlEmpleo SubsidioCausado=\"0\" /></nomina12:OtroPago></nomina12:OtrosPagos></nomina12:Nomina></cfdi:Complemento></cfdi:Comprobante>\r\n",
            "uuid": "7727C59C-A3B2-4E55-93CE-A9A82B87882F",
            "msg": "Se timbro el recibo de nomina correctamente.",
            "statusCode": 200
        },
        "row": 0
    }
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