# 📡 Canales Electrónicos

## 1️⃣ Estándar de Mensajería

El estándar **ISO 20022** es utilizado para el intercambio electrónico de datos entre instituciones financieras. Este estándar permite manejar datos complejos como:

- 📌 **Referencias extensas**  
- 🏛️ **Nombres y direcciones detalladas**  
- 📑 **Datos de remesa más completos**  

---

## 2️⃣ Campos Comunes de Mensajería

Cada petición y respuesta contiene campos comunes, denominados **"Header"** y **"RespuestaComun"**, respectivamente.

### 📨 2.1 HEADER (En las peticiones)

El **HEADER** contiene la información general de la solicitud.

Todas las solicitudes van a requerir que se envie esta información obligatoria (por definirse)

## 🔑 Formato Clave-Valor

| **Clave**            | **Valor**                     | **Descripción**                                                                                               | **Obligatorio/Opcional** | **Ejemplo**                                          |
|----------------------|-------------------------------|---------------------------------------------------------------------------------------------------------------|--------------------------|------------------------------------------------------|
| 📱 id_canal          | APP_MOVIL                      | Identificador del canal de origen.                                                                             | Obligatorio              | mobile_app                                           |
| 🖥️ id_sistema        | FINTECH_CORE                   | Identificador del sistema.                                                                                     | Obligatorio              | android                                               |
| 🏦 id_servicio       | POSICION_CONSOLIDADA           | Identificador del servicio.                                                                                    | Obligatorio              | obtención de posicion consolidada                                 |
| 🔢 versión           | 1.0.0                          | Versión de la aplicación.                                                                                      | Obligatorio              | 1.2.3                                                 |
| 🔒 mac_dispositivo   | 00:1A:2B:3C:4D:5E              | Dirección MAC del dispositivo.                                                                                 | Obligatorio              | 00:1A:2B:3C:4D:5E                                    |
| 🌐 ip_dispositivo    | 192.168.1.100                  | Dirección IP del dispositivo.                                                                                  | Obligatorio              | 192.168.1.100                                        |
| 📲 remitente         | Samsung Galaxy S21             | Nombre, modelo y marca del dispositivo.                                                                         | Obligatorio              | Samsung Galaxy S21                                   |
| 📤 tipo_peticion     | REQ                            | Tipo de petición (debe ser "REQ").                                                                              | Obligatorio              | REQ                                                  |
| 🆔 id_msj            | 123456789                      | Código único para la trazabilidad.                                                                             | Obligatorio              | a1b2c3d4e5f6                                          |
| 📅 fecha_operacion   | 2025-02-11                     | Fecha de la operación (formato: YYYY-MM-DD HH:mm:ss en UTC).                                                   | Obligatorio              | 2025-02-11 14:30:00                                  |
| 🔑 token             | Bearer abcd1234xyz             | Token de autenticación del usuario.                                                                            | Obligatorio              | Bearer abcd1234xyz                                   |
| 👤 login             | usuarioEjemplo                 | Nombre de usuario del cliente.                                                                                 | Obligatorio              | usuarioEjemplo                                        |
| 🗺️ latitud           | -0.1807                        | Latitud del dispositivo.                                                                                       | Obligatorio                 | -0.1807                                               |
| 🗺️ longitud          | -78.4678                       | Longitud del dispositivo.                                                                                      | Obligatorio                 | -78.4678                                              |
| 📶 num_sim           | 0987654321                     | Número de SIM del dispositivo.                                                                                 | Obligatorio                 | 0987654321                                            |
| 🔐 clave_secreta     | encriptado123                  | Clave secreta encriptada.                                                                                      | Obligatorio                 | encriptado123                                         |
| 🇪🇨 país             | EC                             | País del usuario.                                                                                              | Obligatorio              | EC                                                   |
| 🔄 sesión            | sesion1234                     | Identificador de sesión.                                                                                       | Obligatorio                 | sesion1234                                            |
| 🆔 identification     | 1723456789                     | Identificación del usuario en el sistema.                                                                      | Obligatorio                 | 1723456789                                            |
| 👥 id_user           | 1                              | ID del usuario del sistema.                                                                                    | Obligatorio              | 1                                                    |


### 📩 2.2 RESPUESTACOMUN (En las respuestas)

Define el formato de la respuesta del servicio.

Todas las respuestas que se obtienen van a tener este tipo de formato común, como el que se aprecia en la parte inferior.

```json
{
  "id_respuesta": "RESP123456",
  "original_id_servicio": "POSICION_CONSOLIDADA",
  "fecha_msj": "2025-02-11T14:35:00Z",
  "estado_transaccion": "ÉXITO",
  "codigo": "000",
  "mensaje_frontal": "Operación exitosa",
  "data": {
    "id_usuario": "1001",
    "nombres": "Juan Carlos",
    "primer_apellido": "Pérez",
    "segundo_apellido": "Gómez",
    "imagen_usuario": "url_imagen",
    "correo": "juan.perez@example.com",
    "celular": "0991234567",
    "tipo_socio": "Activo",
    "fecha_nacimiento": "1985-06-25"
  }
}
```

### 🔑 2.3 ACCESO

Para realizar pruebas en los diferentes endpoints, acceda a la siguiente URL:

🌍 **[Plataforma de Pruebas](http://190.123.34.157:8000/)**

### 2.4 GENERACIÓN DEL TOKEN PARA PODER REALIZAR LAS CONSULTAS
Para poder realizar las consultas, es necesario generar un token de autenticación. Para ello, se expone a continuación los pasos necesarios a seguir para la obtención del mismo.


# **POST /auth/authenticate**

## **Descripción**

Este endpoint permite autenticar a un usuario utilizando sus credenciales (nombre de usuario y contraseña) y, si la autenticación es exitosa, genera y devuelve un **token JWT** que podrá ser usado para acceder a otros endpoints protegidos de la API.
## **Parámetros de Solicitud (Cuerpo de la Solicitud)**

| **Nombre**  | **Tipo**  | **Descripción**                      | **Obligatorio** |
|-------------|-----------|--------------------------------------|-----------------|
| user        | `string`  | Nombre de usuario del cliente.       | Sí              |
| password    | `string`  | Contraseña del usuario.              | Sí              |

### **Formato para enviar los parámetros en Postman (Body)**

En **Postman**, selecciona el tipo de cuerpo como `raw` y elige `JSON` en el menú desplegable.

Para motivos de pruebas usar el **usuario:** admin y la **contraseña:** admin.

```json
{
  "user": "admin",
  "password": "admin"
}
```



## **Respuesta Exitosa (200 OK)**

Si las credenciales proporcionadas son válidas, se genera un **token JWT** y se devuelve en el cuerpo de la respuesta.

### **Estructura de la Respuesta Exitosa**

| **Nombre**   | **Tipo**   | **Descripción**                                  |
|--------------|------------|--------------------------------------------------|
| statusCode   | `integer`  | Código de estado de la respuesta (200).           |
| message      | `string`   | Mensaje que indica el éxito de la operación.     |
| data         | `object`   | Objeto que contiene el token JWT generado.       |

#### **Ejemplo de Respuesta Exitosa:**

```json
{
    "data": {
        "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJhZG1pbiIsImlhdCI6MTczOTQwOTE5OSwiZXhwIjo...."
    },
    "message": "OK",
    "status": 200
}

```

## **Respuestas de Error**

Si ocurre algún error durante la autenticación, la respuesta incluirá un código de estado adecuado y un mensaje de error específico.

### **401 Unauthorized** - Usuario o Contraseña Incorrectos

Si el nombre de usuario es incorrecto.

#### Ejemplo de Respuesta de Error:

```json
{
    "data": null,
    "message": "INVALID_USER",
    "status": 401
}
```

Si la contraseña del usuario es incorrectos.

#### Ejemplo de Respuesta de Error:

```json
{
    "data": null,
    "message": "INVALID_PASSWORD",
    "status": 401
}
```

### **403 Forbidden - Usuario Inactivo** 

Si el usuario está inactivo y no tiene permisos para acceder al sistema.

#### Ejemplo de Respuesta de Error:

```json
{
    "data": null,
    "message": "DISABLE_USER",
    "status": 403
}
```
## **Excepciones Comunes:**

| **Código**  | **Descripción**                                  | **Mensaje**                        |
|-------------|--------------------------------------------------|------------------------------------|
| 401         | Credenciales incorrectas (usuario o contraseña) | INVALID_USER, INVALID_PASSWORD         |
| 403         | Usuario inactivo                                | DISABLE_USER                       |

## **Códigos de Estado HTTP:**

| **Código de Estado** | **Descripción**                                          |
|----------------------|----------------------------------------------------------|
| `200 OK`             | Autenticación exitosa y token JWT generado correctamente. |
| `401 Unauthorized`   | Credenciales inválidas (usuario o contraseña incorrecta).|
| `403 Forbidden`      | El usuario está inactivo o no tiene permisos para acceder.|

## **Detalles del Endpoint**

- **Método HTTP:** `POST`
- **URL:** `http://190.123.34.157:8000/auth/authenticate`
- **Descripción:** Este endpoint permite la autenticación del usuario con sus credenciales y la generación de un token JWT.
- **Autorización:** No se requiere autorización previa (público).
- **Formato de Respuesta:** `application/json`
- **Formato de Solicitud:** `application/json`

## **Notas Adicionales**

- El token JWT generado es un **token de acceso** y debe ser incluido en las solicitudes posteriores para acceder a otros endpoints que requieren autenticación. Para ello, se debe agregar el token al header de la solicitud como un `Token` con el prefijo `Bearer`.
  
### Ejemplo de Header para Solicitudes Posteriores:
### **Formato en el Header:**

```http
......
......
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
......
......
```

# **ENDPOINTS**


## **5. POSICIÓN CONSOLIDADA**



### **5.1. Información del Usuario**


### **Descripción**

Este endpoint obtiene la información del usuario autenticado en el sistema, devolviendo datos como su nombre, apellidos, imagen de perfil, correo electrónico y tipo de socio.



### **5.1.1. GET /posicionConsolidada**

#### **Detalles del Endpoint**

- **Método HTTP:** `GET`
- **URL:** `http://190.123.34.157:8000/posicionConsolidada`
- **Token:** Requiere token JWT
- **Formato de Respuesta:** `application/json`

#### **Parámetros de Solicitud**

📌 **Entrada:**  
Este endpoint recibe los parámetros de autenticación que es el **Header** de la petición.

| **Nombre**   | **Tipo**   | **Descripción**                                   | **Obligatorio** |
|--------------|------------|---------------------------------------------------|-----------------|
| Token        | `string`   | Token de autenticación obtenido previamente en `/auth/authenticate`. Se debe enviar con el prefijo `Bearer`. | Sí |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

```
#### ***NOTA***
EL Token se envia directamente en los parametros del header


---

### **Parte 4: Respuesta Exitosa**


#### **Respuesta Exitosa (200 OK)**

Si la solicitud es exitosa y el usuario es encontrado, el sistema devuelve la información del usuario.

#### **Estructura de la Respuesta Exitosa:**

| **Nombre**        | **Tipo**    | **Descripción**                                        |
|-------------------|-------------|--------------------------------------------------------|
| id_usuario        | `long`      | Id del usuario que se usa en el CORE                   |
| nombres           | `string`    | Nombres del usuario                                   |
| primer_apellido   | `string`    | Primer apellido del usuario                           |
| segundo_apellido  | `string`    | Segundo apellido del usuario                          |
| imagen_usuario    | `string`    | Link de la imagen del usuario (si existe)             |
| correo            | `string`    | Correo registrado en el CORE                          |
| celular           | `string`    | Celular registrado en el CORE                         |
| tipo_socio        | `string`    | Tipo de socio del usuario                             |
| fecha_nacimiento  | `string`    | Fecha de nacimiento del socio                         |


#### **Ejemplo de Respuesta Exitosa:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T20:41:07.965195900",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "DATOS ENVIADOS",
        "data": {
            "idUsuario": "canalweb",
            "nombres": "JONATHAN XXXXXXXXXXX",
            "primerApellido": "XXXXXXXXXX XXXXXXXXXX",
            "segundoApellido": null,
            "imagenUsuario": null,
            "correo": "jhon2h@hotmail.es",
            "celular": "0987184820",
            "tipoSocio": "S",
            "fechaNacimiento": "1987-05-24T05:00:00.000+00:00"
        }
    },
    "message": "DATOS ENVIADOS",
    "status": 200
}
```



### **Parte 5: Respuestas de Error**

#### **Respuestas de Error**

Si ocurre algún error, el sistema responderá con un código de estado adecuado.

#### **404 Not Found** - Usuario no encontrado

Si no se encuentra el usuario en la base de datos.

#### Ejemplo de Respuesta de Error:

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T20:43:40.103676200",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al recuperar la información del usuario: Socio not found with code: 10000",
        "data": null
    },
    "message": "Error al recuperar la información del usuario: Socio not found with code: 10000",
    "status": 500
}
```

#### **500 Internal Server Error - Error Interno** - Error en el servidor

Si ocurre un error inesperado en el servidor.

#### Ejemplo de Respuesta de Error:
```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T20:43:40.103676200",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error retrieving user information: ...",
        "data": null
    },
    "message": "Error retrieving user information: ...",
    "status": 500
}
```

---

### **Parte 6: Excepciones Comunes y Códigos de Estado**

#### **Excepciones Comunes:**

| **Código**  | **Descripción**                             | **Mensaje**               |
|-------------|---------------------------------------------|---------------------------|
| 404         | Usuario no encontrado                       | User not found            |
| 500         | Error interno del servidor                  | Error retrieving user information |

---

#### **Códigos de Estado HTTP:**

| **Código de Estado** | **Descripción**                                          |
|----------------------|----------------------------------------------------------|
| `200 OK`             | Información del usuario obtenida correctamente.         |
| `404 Not Found`      | No se encontró el usuario solicitado.                   |
| `500 Internal Server Error` | Error al recuperar la información del usuario. |

---

#### **Notas Adicionales**

- **Autenticación:** Se requiere incluir un **token JWT** válido en el encabezado de la solicitud. El token se obtiene mediante el endpoint `/auth/authenticate`.


---

### **Ejemplo de Header para Solicitudes Posteriores:**

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un **Bearer Token** en el **Header** de la solicitud.

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

### **5.1.2. Información de Productos**

---

### **Descripción**

Este endpoint obtiene la lista de productos asociados a un usuario autenticado.  
Los productos pueden incluir **cuentas, pólizas y créditos**, además de cualquier otro producto adicional definido por la institución financiera.

---

### ** GET /products**

#### **Detalles del Endpoint**

- **Método HTTP:** `GET`
- **URL:** `http://190.123.34.157:8000/products`
- **Autorización:** Requiere token JWT
#### **Parámetros de Solicitud**

📌 **Entrada:**  
Este endpoint recibe los parámetros de autenticación en el **Header** de la petición.

| **Nombre**   | **Tipo**   | **Descripción**                                   | **Obligatorio** |
|--------------|------------|---------------------------------------------------|-----------------|
| Token        | `string`   | Token de autenticación obtenido previamente en `/auth/authenticate`. Se debe enviar con el prefijo `Bearer`. | Sí |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

### **Parte 4: Respuesta Exitosa**

```markdown
#### **Respuesta Exitosa (200 OK)**

Si la solicitud es exitosa y el usuario tiene productos asociados, el sistema devolverá la información de cuentas, pólizas y créditos.

##### **Estructura de la Respuesta Exitosa:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T21:26:56.795516600",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Lista de productos obtenida exitosamente",
        "data": {
            "lista_cuentas": [
            {
                    "codCuenta": 120,
                    "nomCuenta": "CASA TOAPXXXXX XXXXXXXXXXXX",
                    "tipoCuenta": "AHORROS A LA VISTA",
                    "saldoDisponible": 1.00,
                    "saldoBloqueado": 0.00,
                    "saldoTotal": 1.00,
                    "codigoProducto": 1,
                    "moneda": 1,
                    "fechaCreacion": "2024-05-31T05:00:00.000+00:00",
                    "aceptaCreditos": 1,
                    "aceptaDebitos": 1
                },
                {
                    "codCuenta": 119,
                    "nomCuenta": "CASA TOAPXXXXXX XXXXXXXXX",
                    "tipoCuenta": "CERTIFICADOS DE APORTACION",
                    "saldoDisponible": 20.00,
                    "saldoBloqueado": 0.00,
                    "saldoTotal": 20.00,
                    "codigoProducto": 2,
                    "moneda": 1,
                    "fechaCreacion": "2024-05-31T05:00:00.000+00:00",
                    "aceptaCreditos": 1,
                    "aceptaDebitos": 0
                },
                {
                    "codCuenta": 30,
                    "nomCuenta": "CASA TOAXXXXXX XXXXXXXXXXX",
                    "tipoCuenta": "AHORRO ENCAJE",
                    "saldoDisponible": 0.00,
                    "saldoBloqueado": 0.00,
                    "saldoTotal": 0.00,
                    "codigoProducto": 6,
                    "moneda": 1,
                    "fechaCreacion": "2024-05-31T05:00:00.000+00:00",
                    "aceptaCreditos": 1,
                    "aceptaDebitos": 1
                }
            ],
            "lista_polizas": [
             {
                    "capital": 21000.00,
                    "numero": 8,
                    "tasaInteres": 12.00000,
                    "plazo": 360,
                    "total": 23469.60,
                    "fechaInicio": "2024-05-31T05:00:00.000+00:00",
                    "fechaFin": "2025-05-26T05:00:00.000+00:00"
                }
            ],
            "lista_creditos": [
             {
                    "monto": 5900.00,
                    "moneda": 1,
                    "numero": 175,
                    "fechaCredito": "2023-03-18T05:00:00.000+00:00",
                    "fechaCuota": "2025-01-10T05:00:00.000+00:00",
                    "capitalPendiente": 0.00,
                    "estado": "V",
                    "sucursal": 1,
                    "tasa": 18.50,
                    "proximaCuota": 5900.00,
                    "diasMora": 0,
                    "numCuotas": 36,
                    "cuotasPagadas": 15
                }
            ]
        }
    }
}
```


---

### **Parte 5: Respuestas de Error**

#### **Respuestas de Error**

Si ocurre algún error, el sistema responderá con un código de estado adecuado.

#### **400 Bad Request** - Encabezado inválido

Si el encabezado de la solicitud no es válido o falta información.

#### Ejemplo de Respuesta de Error:

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T21:31:03.663796700",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Formato de ID del socio inválido",
        "data": null
    },
    "message": "Formato de ID del socio inválido",
    "status": 400
}
```


#### **401 Unauthorized - Token inválido o ausente** 

Si el token de autenticación es incorrecto o no se envió.

#### Ejemplo de Respuesta de Error:

```json
{
    "status": 401,
    "message": "Token has expired, please request a new one",
    "data": null
}
```


#### **404 Not Found - Socio sin productos o no encontrado** 

Si el usuario no tiene productos asociados en la institución financiera o no se encuentra el usuario.

#### Ejemplo de Respuesta de Error:

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T21:33:32.712916300",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Socio no encontrado o sin productos asociados",
        "data": null
    },
    "message": "Socio no encontrado o sin productos asociados",
    "status": 404
}
```

#### **500 Internal Server Error - Error Interno** - Error en el servidor

Si ocurre un error inesperado en el servidor.

#### Ejemplo de Respuesta de Error:
```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener productos de socios",
        "fechaMsj": "2025-02-12T20:43:40.103676200",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error retrieving user information: ...",
        "data": null
    },
    "message": "Error retrieving user information: ...",
    "status": 500
}
```


---

### **Parte 6: Excepciones Comunes y Códigos de Estado**

#### **Excepciones Comunes:**

| **Código**  | **Descripción**                             | **Mensaje**               |
|-------------|---------------------------------------------|---------------------------|
| 400         | Encabezado inválido                        | Encabezado inválido       |
| 401         | Token inválido o ausente                   | Token inválido o ausente  |
| 404         | Socio sin productos                        | Socio no encontrado o sin productos asociados |
| 500         | Error interno del servidor                 | Error interno del servidor: ... |

---

#### **Códigos de Estado HTTP:**

| **Código de Estado** | **Descripción**                                          |
|----------------------|----------------------------------------------------------|
| `200 OK`             | Lista de productos obtenida correctamente.               |
| `400 Bad Request`    | Encabezado inválido en la solicitud.                     |
| `401 Unauthorized`   | Token de autenticación inválido o ausente.               |
| `404 Not Found`      | Socio no encontrado o sin productos asociados.           |
| `500 Internal Server Error` | Error al procesar la solicitud en el servidor.   |

---

#### **Notas Adicionales**

- **Autenticación:** Se requiere incluir un **token JWT** válido en el encabezado de la solicitud. El token se obtiene mediante el endpoint `/auth/authenticate`.

---

### **Ejemplo de Header para Solicitudes Posteriores:**

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un **Bearer Token** en el encabezado de la solicitud.

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

```


### **5.1.4. Tabla de Amortización Original**

---

### **Descripción**

Este endpoint obtiene la tabla de amortización de un crédito específico. Devuelve una lista de cuotas que contiene detalles como el número de cuota, capital, fecha, interés, días de interés, pago, rubros y total.

---

### **GET /amortization**

#### **Detalles del Endpoint**

- **Método HTTP:** `GET`
- **URL:** `http://190.123.34.157:8000/amortization`
- **Autorización:** Requiere autenticación a través de un encabezado con token JWT.
  
---

### **Parámetros de Solicitud**

📌 **Entrada:**  
Este endpoint recibe los parámetros de autenticación y datos en el **Header** de la petición. En este endpoint se debe de tomar en cuenta que se agrega un campo mas al header predeterminado, en este caso se agrega el campo **idCredito** 

| **Nombre**      | **Tipo**   | **Descripción**                              | **Obligatorio** |
|-----------------|------------|----------------------------------------------|-----------------|
| Token           | `string`   | Token de autenticación obtenido previamente. Se debe enviar con el prefijo `Bearer`. | Sí |
| idCredito      | `long`     | ID del crédito para obtener la tabla de amortización. | Sí |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
id_credito: 12345
```
#### **Respuesta Exitosa (200 OK)**

Si la solicitud es exitosa, el sistema devolverá la tabla de amortización correspondiente al crédito solicitado.

##### **Estructura de la Respuesta Exitosa:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener tabla de amortización",
        "fechaMsj": "2025-02-12T21:45:56.795516600",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Tabla de amortización obtenida exitosamente",
        "data": {
            [
            {
                "numeroCuota": 1,
                "capital": 120.51,
                "fecha": "2020-11-10",
                "interes": 50.00,
                "diasInteres": 31,
                "pago": "P",
                "rubros": 0.00,
                "total": 120.51
            },
            {
                "numeroCuota": 3,
                "capital": 123.31,
                "fecha": "2021-01-10",
                "interes": 38.87,
                "diasInteres": 31,
                "pago": "P",
                "rubros": 0.00,
                "total": 123.31
            },
            {
                "numeroCuota": 5,
                "capital": 130.94,
                "fecha": "2021-03-10",
                "interes": 31.24,
                "diasInteres": 28,
                "pago": "P",
                "rubros": 0.00,
                "total": 130.94
            },
            {
                "numeroCuota": 6,
                "capital": 129.85,
                "fecha": "2021-04-10",
                "interes": 32.33,
                "diasInteres": 31,
                "pago": "P",
                "rubros": 0.00,
                "total": 129.85
            },
            ......
            ......
            ......
        }
    }
}
```
### **Parte 5: Respuestas de Error**

#### **Respuestas de Error**

Si ocurre algún error, el sistema responderá con un código de estado adecuado.

---

#### **400 Bad Request - Solicitud inválida**

Si el ID del crédito no es proporcionado o el formato es incorrecto.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T21:51:00.771897300",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Invalid credit ID format in the custom header",
        "data": null
    },
    "message": "Invalid credit ID format in the custom header",
    "status": 400
}
```
### **401 Unauthorized - Token inválido o ausente**

Si el token de autenticación es incorrecto o no se envió.

**Ejemplo de Respuesta de Error:**

```json
{
    "status": 401,
    "message": "Token has expired, please request a new one",
    "data": null
}
```
### **500 Internal Server Error - Error Interno**

Si ocurre un error inesperado en el servidor.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener tabla de amortización",
        "fechaMsj": "2025-02-12T21:48:40.103676200",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al obtener la tabla de amortización: ...",
        "data": null
    },
    "message": "Error al obtener la tabla de amortización: ...",
    "status": 500
}
```
### **Parte 6: Excepciones Comunes y Códigos de Estado**

#### **Excepciones Comunes:**

| **Código** | **Descripción**                             | **Mensaje**                                |
|------------|---------------------------------------------|--------------------------------------------|
| 400        | Solicitud inválida                         | ID de crédito no proporcionado            |
| 401        | Token inválido o ausente                   | Token inválido o ausente                  |
| 500        | Error interno del servidor                 | Error al obtener la tabla de amortización |

---

#### **Códigos de Estado HTTP:**

| **Código de Estado**             | **Descripción**                                      |
|----------------------------------|------------------------------------------------------|
| `200 OK`                         | Tabla de amortización obtenida correctamente.        |
| `400 Bad Request`                | ID de crédito no proporcionado o formato incorrecto.|
| `401 Unauthorized`               | Token de autenticación inválido o ausente.           |
| `500 Internal Server Error`      | Error en el servidor al procesar la solicitud.       |

---

### **Notas Adicionales**

- **Autenticación:** Se requiere incluir un **token JWT** válido en el encabezado de la solicitud.
- **Formato del ID de crédito:** El ID de crédito debe ser un valor numérico válido.

### **Ejemplo de Header para Solicitudes Posteriores:**

Cuando se haga una solicitud a este endpoint, recuerda incluir el **token de autenticación** obtenido en el endpoint `/auth/authenticate` como un **Token** en el encabezado de la solicitud.

#### **Header de la Solicitud:**


```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

```

### **5.1.5. Tabla de Amortización Calculada**

---

### **Descripción**

Este endpoint obtiene la tabla de amortización calculada para un crédito específico. Devuelve una lista de cuotas que contiene detalles como el número de cuota, capital, fecha de inicio, fecha de fin, interés, mora, rubros, saldo, estado, días de mora, días de interés, gestión de cobro y total.

---

### **GET /amortizacion-calculada**

#### **Detalles del Endpoint**

- **Método HTTP:** `GET`
- **URL:** `http://190.123.34.157:8000/amortizacionCalculada`
- **Autorización:** Requiere autenticación a través de un encabezado con token JWT.

---

### **Parámetros de Solicitud**

📌 **Entrada:**  
Este endpoint recibe los parámetros de autenticación y datos en el **Header** de la petición. En este caso, se debe agregar un campo adicional en el encabezado: **idCredito**.

| **Nombre**      | **Tipo**   | **Descripción**                              | **Obligatorio** |
|-----------------|------------|----------------------------------------------|-----------------|
| Token           | `string`   | Token de autenticación obtenido previamente. Se debe enviar con el prefijo `Bearer`. | Sí |
| idCredito      | `long`     | ID del crédito para obtener la tabla de amortización calculada. | Sí |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
idCredito: 12345
```

### **Respuesta Exitosa (200 OK)**

Si la solicitud es exitosa, el sistema devolverá la tabla de amortización calculada correspondiente al crédito solicitado.

#### **Estructura de la Respuesta Exitosa:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener tabla de amortización calculada",
        "fechaMsj": "2025-02-12T21:47:03.663796700",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "DATOS ENVIADOS",
        "data": [
            {
                "numero": 1,
                "capital": 500.00,
                "fechaInicio": "2025-03-01",
                "fechaFin": "2025-04-01",
                "interes": 50.00,
                "mora": 0.00,
                "rubros": ["Rubro 1", "Rubro 2"],
                "saldo": 4500.00,
                "estado": "Pendiente",
                "diasmora": 0,
                "diasInteres": 30,
                "gestionCobro": "Pago mensual",
                "total": 550.00
            },
            {
                "numero": 2,
                "capital": 500.00,
                "fechaInicio": "2025-04-01",
                "fechaFin": "2025-05-01",
                "interes": 45.00,
                "mora": 0.00,
                "rubros": ["Rubro 3", "Rubro 4"],
                "saldo": 4000.00,
                "estado": "Pendiente",
                "diasmora": 0,
                "diasInteres": 30,
                "gestionCobro": "Pago mensual",
                "total": 545.00
            }
        ]
    },
    "message": "DATOS ENVIADOS",
    "status": 200
}
```
### **Respuestas de Error**

Si ocurre algún error, el sistema responderá con un código de estado adecuado.

#### **400 Bad Request - Solicitud inválida**

Si el ID del crédito no es proporcionado o el formato es incorrecto.

##### **Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener tabla de amortización calculada",
        "fechaMsj": "2025-02-12T21:47:03.663796700",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "No se proporcionó el ID de crédito en el header personalizado",
        "data": null
    },
    "message": "No se proporcionó el ID de crédito en el header personalizado",
    "status": 400
}
```

### **500 Internal Server Error - Error Interno**

Si ocurre un error inesperado en el servidor.

#### **Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener tabla de amortización calculada",
        "fechaMsj": "2025-02-12T21:47:03.663796700",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al obtener la tabla de amortización calculada: Error inesperado en el servidor",
        "data": null
    },
    "message": "Error al obtener la tabla de amortización calculada: Error inesperado en el servidor",
    "status": 500
}
```


### **Excepciones Comunes y Códigos de Estado**

#### **Excepciones Comunes:**

| **Código** | **Descripción**                              | **Mensaje**                                      |
|------------|----------------------------------------------|--------------------------------------------------|
| 400        | Solicitud inválida                           | ID de crédito no proporcionado o formato incorrecto |
| 500        | Error interno del servidor                   | Error al obtener la tabla de amortización calculada |

#### **Códigos de Estado HTTP:**

| **Código de Estado**      | **Descripción**                                    |
|---------------------------|----------------------------------------------------|
| 200 OK                    | Tabla de amortización calculada obtenida correctamente. |
| 400 Bad Request           | ID de crédito no proporcionado o formato incorrecto. |
| 500 Internal Server Error | Error en el servidor al procesar la solicitud. |

---

### **Notas Adicionales**

- **Autenticación:** Se requiere incluir un token JWT válido en el encabezado de la solicitud.
- **Formato del ID de crédito:** El ID de crédito debe ser un valor numérico válido.

---

### **Ejemplo de Header para Solicitudes Posteriores:**

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### **Header de la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
idCredito: 12345
```



### **5.4.1. Listar IFIs**

---

### **Descripción**

Este endpoint permite obtener una lista de todas las Instituciones Financieras (IFIs) activas.

---

### **GET /ifis**

#### **Detalles del Endpoint**

- **Método HTTP:** `GET`
- **URL:** `http://http://190.123.34.157:8000/ifis`
- **Autorización:** Requiere autenticación a través de un encabezado con token JWT.

---

### **Parámetros de Solicitud**

📌 **Entrada:**  
Este endpoint recibe los parámetros de autenticación en el **Header** de la petición.

| **Nombre**             | **Tipo**   | **Descripción**                                    | **Obligatorio** |
|------------------------|------------|----------------------------------------------------|-----------------|
| Token                  | `string`   | Token de autenticación obtenido previamente. Se debe enviar con el prefijo `Bearer`. | Sí |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```
### **Respuesta Exitosa (200 OK)**

Si la solicitud es exitosa, el sistema devolverá la lista de las IFIs activas disponibles.

#### **Estructura de la Respuesta Exitosa:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Obtener información de usuario",
        "fechaMsj": "2025-02-12T22:31:11.881215800",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "DATOS ENVIADOS",
        "data": [
            {
                "codigo": 2,
                "nombre": "BANCO DEL PICHINCHA"
            },
            {
                "codigo": 3,
                "nombre": "BANCO BOLIVARIANO"
            },
            {
                "codigo": 4,
                "nombre": "BANCO DEL AUSTRO"
            },
            {
                "codigo": 1,
                "nombre": "BANCO DE GUAYAQUIL"
            },
        ]
    },
    "message": "DATOS ENVIADOS",
    "status": 200
}
```
### **Descripción de la Respuesta**

- **codigo**: Código de la Institución Financiera.
- **nombre**: Nombre de la Institución Financiera.

---

### **Respuestas de Error**

Si ocurre algún error, el sistema responderá con un código de estado adecuado.

#### **500 Internal Server Error - Error Interno**

Si ocurre un error inesperado en el servidor.

##### **Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "Listar IFIs",
        "fechaMsj": "2025-02-12T21:47:03.663796700",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al obtener la lista de IFIs: Error inesperado en el servidor",
        "data": null
    },
    "message": "Error al obtener la lista de IFIs: Error inesperado en el servidor",
    "status": 500
}
```


### **Excepciones Comunes y Códigos de Estado**

#### **Excepciones Comunes:**

| **Código** | **Descripción**            | **Mensaje**                                           |
|------------|----------------------------|-------------------------------------------------------|
| 500        | Error interno del servidor | Error al obtener la lista de IFIs                    |

#### **Códigos de Estado HTTP:**

| **Código de Estado**      | **Descripción**                                    |
|---------------------------|----------------------------------------------------|
| 200 OK                    | IFIs obtenidas correctamente.                     |
| 500 Internal Server Error | Error en el servidor al procesar la solicitud.    |

---

### **Notas Adicionales**

- **Autenticación:** Se requiere incluir un token JWT válido en el encabezado de la solicitud.

---

### **Ejemplo de Header para Solicitudes Posteriores:**

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### **Header de la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```