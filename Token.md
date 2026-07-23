[Atrás ←](/garotec/kubox/wiki/Timbre4.0)

## Registro

Para poder usar el servicio, es necesario tener una cuenta en la plataforma [kubox.mx](https://kubox.mx/) la cual se obtiene llenando el [formulario de registro](https://panel.kubox.mx/register) y activando la cuenta conforme las instrucciones recibidas por correo electrónico.

En el caso del ambiente de pruebas, el usuario y contraseña sera proporcionado por el personal de Kubox, una ves que pase a producción los datos de acceso serán los generados en [kubox.mx](https://kubox.mx/) descrito en el párrafo anterior.

----------
## Acceso a la API
Existe un ambiente de desarrollo y un ambiente de producción, para poder acceder al ambiente de desarrollo es necesario que tengas una cuenta registrada y mandar un correo a la dirección soporte@kubox.mx con el asunto "¡Soy desarrollador!" y un breve mensaje con tu nombre de usuario para proporcionarte el acceso.

### Desarrollo URL

    https://development.kubox.mx/v2/
### Producción URL

    https://api.kubox.mx/v2/
Para crear una petición completa es necesaria envíar las cabeceras HTTP correctas y la información en formato JSON.

** Todos los ejemplos de está documentación están apuntados al ambiente de pruebas.

----------
## Token
### Autenticarse
Se necesita autenticarse en la plataforma para obtener un objeto con la información de usuario.

#### Petición

    https://development.kubox.mx/v2/auth/login


| Propiedad   | Descripción                             |
| ----------  |--------------------------------------   |
| `usuario`   | __*String*__ Nombre de usuario          |
| `password`  | __*String*__ Contraseña de usuario      |

#### Ejemplo de petición:

```php
  curl https://development.kubox.mx/v2/auth/login \
     -H "Content-type: application/json" \
     -X POST -d '{
    "usuario": "usuario",
    "password": "123"
    }'
```

#### Respuesta
Retorna un objeto con la información del usuario y el token para usarlo en las peticiones.
```json

  {
    "errors": false,
    "status_code": 200,
    "data": {
        "id": 52,
        "nombre": "Alan",
        "apellido": "Piña",
        "usuario": "alanpina",
        "email": "ejemplo@kubox.com",
        "tipo": "user",
        "avatar": null,
        "created_at": "2017-09-04",
        "updated_at": "2017-09-13",
        "deleted_at": null,
        "status": true,
        "precio_timbre": 1,
        "acep_contrato": true,
        "view_guide": false,
        "saldo": {
            "saldo": "50.000",
            "saldo_actual": "50.000",
            "pagar": [
                "",
                ""
            ],
            "status": "pagado",
            "referencia": 52
        },
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczovL2RldmVsb3BtZW50Lmt1Ym94Lm14L3YyL2F1dGgvbG9naW4iLCJpYXQiOjE1MDg1MzIyODMsImV4cCI6MTUwODU1Mzg4MywibmJmIjoxNTA4NTMyMjgzLCJqdGkiOiIwWGVSM3pMaFR2bm1IVWhSIiwic3ViIjo1Mn0.MrXBKWeixKZtc0YmeiKU7qOmsnar72zK1p4HrNmui7A",
    }
  }
```
### Objeto Error
Kubox responde objetos JSON en caso de error con la siguiente estructura:

| Propiedad     | Descripción                             |
| ----------    |--------------------------------------   |
| `errors`      | __*Object/String*__ Errores             |
| `status_code` | __*String*__ Código de error HTTP       |

#### Códigos de error

| Error HTTP | Causa                                   |
| ---------- |--------------------------------------   |
| `422`      | Error en la validación de datos         |
| `401`      | Problema al autenticar la cuenta        |

#### Ejemplo de respuesta con error de validación
```json

    {
        "errors": {
            "usuario": [
                "El campo usuario es obligatorio."
            ],
            "password": [
                "El campo contraseña es obligatorio."
            ]
        },
        "status_code": 422
    }
```

#### Ejemplo de respuesta con error de autenticación
```json

    {
        "errors": "El usuario o contraseña son incorrectas",
        "status_code": 401
    }
```