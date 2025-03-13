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

Si las credenciales proporcionadas son válidas, se genera un **token JWT** y se devuelve en el cuerpo de la respuesta. Además se devuelve en segundos el tiempo de duración del token

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
        "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJhZG1pbiIsImlhdCI6MTc0MDEwMzk5NiwiZXhwIjoxNzQwMTA1Nzk2fQ.uqHASczP6ftIdeibel0x7RPn-wwNfqfTClUI_LfPFzU",
        "expiration": 1800
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
| idUser        | `string`   | Número de cédula del socio qe se esta buscando la información | Sí |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
id_user: 1101416319

```
#### ***NOTA***
EL Token se envia directamente en los parametros del header, al igual que el id_user que en este caso es la cedula del usuario que se está buscando


---

### **Respuesta Exitosa**


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
            "idUsuario": 1,
            "nombres": "GALO XXXXXXXX",
            "primerApellido": "AGUIRRE XXXXXXXXXXXX",
            "segundoApellido": null,
            "imagenUsuario": null,
            "correo": "",
            "celular": "0",
            "tipoSocio": "S",
            "fechaNacimiento": "1955-02-06T05:00:00.000+00:00"
        }
}
```



### **Respuestas de Error**

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
        "mensajeFrontal": "Error al recuperar la información del usuario: Socio not found with code: 110xxxxxx",
        "data": null
    },
    "message": "Error al recuperar la información del usuario: Socio not found with code: 110xxxxxx",
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

### **Excepciones Comunes y Códigos de Estado**

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

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un **Bearer Token** en el **Header** de la solicitud  además el idUser que en este caso es el número de cédula del socio a buscar.

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
id_user: 1101416319
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
| idUser        | `string`   | Número de cédula del socio qe se esta buscando la información | Sí |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
id_user: 1101416319
```

---

### **Respuesta Exitosa**

#### **Respuesta Exitosa (200 OK)**

Si la solicitud es exitosa y el usuario tiene productos asociados, el sistema devolverá la información de cuentas, pólizas y créditos.

##### **Estructura de la Respuesta Exitosa:**

```json
{
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
```


---

### **Respuestas de Error**

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

### **Excepciones Comunes y Códigos de Estado**

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

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un **Bearer Token** en el encabezado de la solicitud. Además se debe de eviar el idUser que en este caso es la cédula del socio.

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
id_user: 1101416319

```


### 5.1.3. Consultar Movimientos

#### Descripción

Este endpoint obtiene los movimientos de los productos que los requiera.


#### Detalles del Endpoint

*   **Método HTTP:** `GET`
*   **URL:** `http://190.123.34.157:8000/movimientos` 
*   **Token:** Requiere token JWT en el [Header común de la API].
*   **Formato de Respuesta:** `application/json`

#### Parámetros de Solicitud

*   **Header:** Ver la definición en [Header común de la API].  El Header debe incluir el token JWT para la autenticación.
*   **Query Parameters:**

    | Nombre          | Tipo     | Descripción                                                                                                      | Obligatorio | Ejemplo      |
    |-----------------|----------|------------------------------------------------------------------------------------------------------------------|-------------|--------------|
    | `codCuenta`     | `long`    | Identificación de la cuenta.  Se debe mandar en el header.                                                             | Sí          | `1`  |
    | `codProducto`   | `long`    | Identificación del producto.  Se debe mandar como parametro en el header.                                                               | Sí          | `1`        |
    | `fechaInicio`   | `string` | Fecha de inicio para la consulta de movimientos (formato: `YYYY-MM-DD`). Se debe mandar como parametro en el header.        | Sí          | `2024-01-01` |
    | `fechaFin`      | `string` | Fecha de fin para la consulta de movimientos (formato: `YYYY-MM-DD`). Se debe mandar como parametro en el header.           | Sí          | `2024-01-31` |

#### Ejemplo de Solicitud

**Header:**  (Consulta la definición en [Header común de la API](#21-header-en-las-peticiones))

**Ejemplo de URL:**
http://190.123.34.157:8000/movimientos


**Nota:** El `codCuenta`,`codProducto`,`fechaInicio`,`fechaFin` se extrae de los parámetros que se envián en el header.


#### Estructura de la Respuesta Exitosa

La respuesta sigue la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). El campo `data` contiene una lista de movimientos.  Cada movimiento tendrá al menos los siguientes campos:

| Nombre          | Tipo     | Descripción                                                                 |
|-----------------|----------|-----------------------------------------------------------------------------|
| `transaccion`   | `string` | Tipo de transacción (Débito/Crédito)                                        |
| `concepto`      | `string` | Concepto de la transacción                                                  |
| `fecha`         | `string` | Fecha de la transacción                                                     |
| `hora`          | `string` | Hora de la transacción                                                      |
| `fechaSistema`  | `string` | Fecha en que se registró la transacción en el sistema                      |
| `usuario`       | `string` | Usuario que realizó la transacción                                           |
| `id_transaccion`| `string` | Identificador único de la transacción                                        |
| `valor`         | `number` | Valor de la transacción                                                     |
| `saldo`         | `number` | Saldo después de la transacción                                            |
| `comprobante`   | `string` | Información del comprobante (si está disponible)                             |


#### Ejemplo de Respuesta Exitosa

```json
{
    "data": [
            {
                "transaccion": "NC",
                "concepto": "INTERES AHORRO A LA VISTA",
                "fecha": "2023-01-31T05:00:00.000+00:00",
                "hora": "2023-02-01T04:59:59.000+00:00",
                "fechaSistema": "2023-02-01T13:19:40.245+00:00",
                "usuario": "DAISI ABARCA",
                "valor": 0.03,
                "saldo": 59.75,
                "idTransaccion": 77077,
                "comprobante": null
            },
            {
                "transaccion": "NC",
                "concepto": "INTERES AHORRO A LA VISTA",
                "fecha": "2023-01-31T05:00:00.000+00:00",
                "hora": "2023-02-01T04:59:59.000+00:00",
                "fechaSistema": "2023-02-01T13:19:40.245+00:00",
                "usuario": "DAISI ABARCA",
                "valor": 0.03,
                "saldo": 59.75,
                "idTransaccion": 77077,
                "comprobante": null
            },

            ........
            ........
            ........
  ]
        
}
```
---



**.  Respuestas de Error**

Las respuestas de error siguen la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). Ejemplos:

#### 400 Bad Request - Parámetros de solicitud inválidos

Si alguno de los parámetros `codCuenta`, `codProducto`, `fechaInicio`, o `fechaFin` no es proporcionado o tiene un formato incorrecto.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtención de movimientos",
        "fechaMsj": "2025-02-20T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Parámetros de solicitud inválidos: fechaInicio tiene un formato incorrecto",
        "data": null
    },
    "message": "Parámetros de solicitud inválidos: fechaInicio tiene un formato incorrecto",
    "status": 400
}
```

#### 500 Internal Server Error - Error al obtener los movimientos

Si ocurre un error inesperado en el servidor al intentar obtener los movimientos.

**Ejemplo de Respuesta de Error:**


```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtención de movimientos",
        "fechaMsj": "2025-02-20T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al obtener los movimientos: Error en la base de datos",
        "data": null
    },
    "message": "Error al obtener los movimientos: Error en la base de datos",
    "status": 500
}
```

#### Códigos de Estado HTTP

*   `200 OK`: Movimientos obtenidos correctamente.
*   `400 Bad Request`: Parámetros de solicitud inválidos.
*   `500 Internal Server Error`: Error al obtener los movimientos.



*** Excepciones Comunes y Códigos de Estado**

---

#### Excepciones Comunes:

| **Código** | **Descripción**                             | **Mensaje**                                                              |
|------------|---------------------------------------------|--------------------------------------------------------------------------|
| 400        | Solicitud inválida                           | Parámetros de solicitud inválidos                                           |
| 500        | Error interno del servidor                 | Error al obtener los movimientos                                             |

---

#### Códigos de Estado HTTP

| **Código de Estado** | **Descripción**                    |
|----------------------|------------------------------------|
| 200 OK               | Movimientos obtenidos correctamente |
| 400 Bad Request      | Parámetros de solicitud inválidos  |
| 500 Internal Server Error | Error al obtener los movimientos   |



#### Notas Adicionales

*   Asegúrate de incluir un token JWT válido en el campo `token` del [Header](#21-header-en-las-peticiones).
*   Las fechas deben estar en formato `YYYY-MM-DD`.



---

###  Ejemplo de Header para Solicitudes Posteriores

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### Header de la Solicitud:

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codCuenta: 1
codProducto: 1
fechaInicio: 2024-01-01
fechaFin: 2024-01-31
```


### **5.1.4. Tabla de Amortización Original**

---

### **Descripción**

Este endpoint obtiene la tabla de amortización de un crédito específico. Devuelve una lista de cuotas que contiene detalles como el número de cuota, capital, fecha, interés, días de interés, pago, rubros y total.

---

### **GET /amortizacion**

#### **Detalles del Endpoint**

- **Método HTTP:** `GET`
- **URL:** `http://190.123.34.157:8000/amortizacion`
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
            ......]
        }
}
```
### **Respuestas de Error**

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
### **Excepciones Comunes y Códigos de Estado**

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

### **GET /amortizacionCalculada**

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





### 5.1.6. Tabla de detalle de ahorro programado

---

### Descripción

Obtiene la tabla de cuotas de un ahorro programado específico, utilizando el código de producto y el número de identificación del cliente.

---

### Detalles del Endpoint

*   **Método HTTP:** `GET`
*   **URL:** `http://190.123.34.157:8000/ahorroProgramado`
*   **Token:** Requiere token JWT en el [Header común de la API](#21-header-en-las-peticiones).
*   **Formato de Respuesta:** `application/json`

---

### Parámetros de Solicitud

📌 **Entrada:**
Este endpoint recibe los parámetros de autenticación en el **Header** de la petición y los parámetros de búsqueda también en el Header.

*   **Header:** Ver la definición en [Header común de la API](#21-header-en-las-peticiones). El Header debe incluir el token JWT para la autenticación, además los siguientes parámetros:

    | Nombre          | Tipo     | Descripción                                                                                                        | Obligatorio | Ejemplo       |
    |-----------------|----------|--------------------------------------------------------------------------------------------------------------------|-------------|---------------|
    | `codProducto`   | `long`   | Código del producto de ahorro programado.                                                                        | Sí          | `1`           |
    | `numId`         | `string` | Número de identificación (cédula) del cliente.                                                                    | Sí          | `1717171717`  |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
numId: 1717171717
```



---

### Descripción de los Códigos de Producto

El parámetro `codProducto` identifica el tipo de producto al que corresponde el ahorro programado. A continuación, se describen los valores posibles:

| Código | Descripción                                        |
|--------|----------------------------------------------------|
| 1      | AHORROS A LA VISTA                               |
| 2      | CERTIFICADOS DE APORTACION                         |
| 3      | OPERACIONES DE CAJA                              |
| 4      | DEPOSITO A PLAZO                                 |
| 5      | CREDITO                                          |
| 6      | AHORRO ENCAJE                                    |
| 7      | AHORRO PROGRAMADO                                |
| 8      | AHORRO INFANTIL                                  |
| 9      | AHORRO PERSONAL                                  |
| 10     | AHORRO NAVIDEÑO                                  |
| 11     | RECAUDACION INSTITUCIONES PUBLICAS               |
| 12     | AHORRO DORADO                                    |
| 13     | AHORRO PROFESIONAL                               |
| 14     | CUENTA DE INVERSION                               |



**Ejemplo de Solicitud**




---

### Ejemplo de Solicitud

**Header:** (Consulta la definición en [Header común de la API](#21-header-en-las-peticiones))

**Ejemplo de URL:**

http://190.123.34.157:8000/ahorroProgramado

**Nota:** El `codProducto` y `numId` se extraen de los parámetros que se envían en el header.


---

### Estructura de la Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

Si la solicitud es exitosa, el sistema devolverá la lista de cuotas del ahorro programado solicitada.

##### Estructura de la Respuesta Exitosa

La respuesta sigue la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). El campo `data` contiene una lista de cuotas. Cada cuota tendrá al menos los siguientes campos:

| Nombre             | Tipo        | Descripción                                                                                     |
|--------------------|-------------|-------------------------------------------------------------------------------------------------|
| `numero`           | `integer`   | Número de la cuota                                                                              |
| `fecha`            | `string`    | Fecha de vencimiento de la cuota                                                                |
| `valorCuota`       | `number`    | Valor de la cuota                                                                               |
| `montoAcumulado`   | `number`    | Monto acumulado hasta la fecha                                                                   |
| `interes`          | `number`    | Interés generado por la cuota                                                                   |
| `seguro`           | `number`    | Valor del seguro (si aplica)                                                                     |
| `total`            | `number`    | Valor total de la cuota (valorCuota + interes + seguro)                                           |
| `valorRecaudado`   | `number`    | Valor que realmente se ha pagado                                                                |
| `fechaRecaudado`   | `string`    | Fecha en la que se recaudó el dinero                                                              |
| `estado`           | `string`    | Estado de la cuota (ej: "Pendiente", "Pagada")                                                    |


---

### Ejemplo de Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtención de cuotas ahorro programado",
        "fechaMsj": "2025-02-20T10:00:00.000+00:00",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "DATOS ENVIADOS",
        "data": [
            {
                "numero": 1,
                "fecha": "2024-03-01",
                "valorCuota": 100.00,
                "montoAcumulado": 100.00,
                "interes": 0.50,
                "seguro": 0.00,
                "total": 100.50,
                "valorRecaudado": 100.50,
                "fechaRecaudado": "2024-03-01",
                "estado": "P"
            },
            {
                "numero": 2,
                "fecha": "2024-04-01",
                "valorCuota": 100.00,
                "montoAcumulado": 200.00,
                "interes": 0.50,
                "seguro": 0.00,
                "total": 100.50,
                "valorRecaudado": 0.00,
                "fechaRecaudado": null,
                "estado": "C"
            }
            //..., mas cuotas
        ]
    }
}
```




---

### Respuestas de Error

#### Respuestas de Error

Las respuestas de error siguen la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). Ejemplos:

#### 400 Bad Request - ID de ahorro programado no proporcionado

Si el `idAhorroProgramado` no es proporcionado en el header.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtención de cuotas ahorro programado",
        "fechaMsj": "2025-02-20T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "ID de ahorro programado no proporcionado en el header personalizado",
        "data": null
    },
    "message": "ID de ahorro programado no proporcionado en el header personalizado",
    "status": 400
}

```

#### 400 Bad Request - Formato de ID de ahorro programado inválido

Si el `idAhorroProgramado` tiene un formato inválido.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtención de cuotas ahorro programado",
        "fechaMsj": "2025-02-20T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Formato de ID de ahorro programado inválido en el header personalizado",
        "data": null
    },
    "message": "Formato de ID de ahorro programado inválido en el header personalizado",
    "status": 400
}

```

#### 500  Internal Server Error - Error al obtener las cuotas del ahorro programado

Si ocurre un error inesperado en el servidor al intentar obtener las cuotas.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtención de cuotas ahorro programado",
        "fechaMsj": "2025-02-20T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al obtener las cuotas del ahorro programado: Error en la base de datos",
        "data": null
    },
    "message": "Error al obtener las cuotas del ahorro programado: Error en la base de datos",
    "status": 500
}

```




**Excepciones Comunes y Códigos de Estado**

---

### Excepciones Comunes y Códigos de Estado

#### Excepciones Comunes:

| **Código** | **Descripción**                             | **Mensaje**                                                              |
|------------|---------------------------------------------|--------------------------------------------------------------------------|
| 400        | Solicitud inválida                           | ID de ahorro programado no proporcionado o formato inválido              |
| 500        | Error interno del servidor                 | Error al obtener las cuotas del ahorro programado                         |


---

#### Códigos de Estado HTTP

| **Código de Estado** | **Descripción**                                      |
|----------------------|------------------------------------------------------|
| 200 OK               | Cuotas del ahorro programado obtenidas correctamente |
| 400 Bad Request      | ID de ahorro programado no proporcionado o formato inválido |
| 500 Internal Server Error | Error al obtener las cuotas del ahorro programado   |


---

### Notas Adicionales

*   Asegúrate de incluir un token JWT válido en el campo `token` del [Header](#21-header-en-las-peticiones).
*   El `idAhorroProgramado` debe ser un número entero válido.
*   El `idAhorroProgramado` debe ser enviado en el header de la petición


---

### Ejemplo de Header para Solicitudes Posteriores

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### Header de la Solicitud:

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
idAhorroProgramado: 4
```



### 5.2.1. Validar beneficiario interno

---

### Descripción

Valida si una cuenta interna existe, en caso de existir, devuelve los datos de esta.


---

### Detalles del Endpoint

*   **Método HTTP:** `GET`
*   **URL:** `http://190.123.34.157:8000/beneficiarios`
*   **Token:** Requiere token JWT en el [Header común de la API](#21-header-en-las-peticiones).
*   **Formato de Respuesta:** `application/json`


---

### Parámetros de Solicitud

📌 **Entrada:**
Este endpoint recibe los parámetros de autenticación en el **Header** de la petición y los parámetros de búsqueda también en el Header.

*   **Header:** Ver la definición en [Header común de la API](#21-header-en-las-peticiones). El Header debe incluir el token JWT para la autenticación, además los siguientes parámetros:

    | Nombre          | Tipo     | Descripción                                                                                                  | Obligatorio | Ejemplo        |
    |-----------------|----------|--------------------------------------------------------------------------------------------------------------|-------------|----------------|
    | `codProducto`    | `long`   | Código del producto a validar.                                                                            | Sí          | `1`            |
    | `codCuenta`      | `long`   | Número de cuenta a validar.                                                                                | Sí          | `1234567890`   |
    | `numeroIdentificacion` | `string` | Número de Identificación del socio a validar (alternativo a codCuenta y codProducto). | No | `1723456789`|
    | `celular` | `string` | Número de celular del socio a validar (alternativo a codCuenta y codProducto). | No | `0999999999` |

📌 **Ejemplo de Header en la Solicitud (Búsqueda por CodProducto y CodCuenta):**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
codCuenta: 1234567890
```


**Ejemplo de Solicitud**

---
### Ejemplo de Solicitud

**Ejemplo de URL:**
http://190.123.34.157:8000/beneficiarios


**Nota:** El `codProducto` y `codCuenta`, se extraen de los parámetros que se envían en el header.


---

### Estructura de la Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

Si la solicitud es exitosa, el sistema devolverá la información del beneficiario interno.

##### Estructura de la Respuesta Exitosa

La respuesta sigue la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). El campo `data` contiene la información del beneficiario interno:

| Nombre                  | Tipo        | Descripción                                                                         |
|-------------------------|-------------|-------------------------------------------------------------------------------------|
| `nombreSocio`           | `string`    | Nombre del socio                                                                    |
| `identificacionSocio`   | `string`    | Número de identificación del socio                                                    |
| `email`                 | `string`    | Dirección de correo electrónico del socio                                            |
| `tipoCuenta`            | `string`    | Tipo de cuenta del socio                                                              |
| `celular`               | `string`    | Número de celular del socio                                                           |
| `aceptaCreditos`        | `integer`   | Indica si el socio acepta créditos (1: Sí, 0: No)                                      |
| `aceptaDebitos`         | `integer`   | Indica si el socio acepta débitos (1: Sí, 0: No)                                       |


---

### Ejemplo de Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "validación beneficiario interno",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Beneficiario encontrado",
        "data": {
            "nombreSocio": "Juan Pérez",
            "identificacionSocio": "1717171717",
            "email": "juan.perez@example.com",
            "tipoCuenta": "Ahorros",
            "celular": "0999999999",
            "aceptaCreditos": 1,
            "aceptaDebitos": 0
        }
    }
}
```

---

### Respuestas de Error

#### Respuestas de Error

Las respuestas de error siguen la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). Ejemplos:

#### 400 Bad Request - Parámetros de solicitud inválidos

Si `codProducto` o `codCuenta` no son proporcionados en el header, o si el formato de los números es inválido.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "validación beneficiario interno",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "codProducto y codCuenta deben estar presentes en el encabezado",
        "data": null
    },
    "message": "codProducto y codCuenta deben estar presentes en el encabezado",
    "status": 400
}

```

#### 404 Not Found - Beneficiario interno no encontrado

Si no se encuentra el beneficiario interno con los parámetros proporcionados.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "validación beneficiario interno",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "404",
        "mensajeFrontal": "Beneficiario interno no encontrado",
        "data": null
    },
    "message": "Beneficiario interno no encontrado",
    "status": 404
}

```

#### 500 Internal Server Error - Error al validar beneficiario interno

Si ocurre un error inesperado en el servidor al intentar validar el beneficiario interno.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "validación beneficiario interno",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al validar beneficiario interno: Error en la base de datos",
        "data": null
    },
    "message": "Error al validar beneficiario interno: Error en la base de datos",
    "status": 500
}


```


**Excepciones Comunes y Códigos de Estado**

---

### Excepciones Comunes y Códigos de Estado

#### Excepciones Comunes:

| **Código** | **Descripción**                             | **Mensaje**                                                                               |
|------------|---------------------------------------------|-------------------------------------------------------------------------------------------|
| 400        | Solicitud inválida                           | `codProducto` o `codCuenta` no proporcionados o formato inválido, o parámetros alternativos no proporcionados |
| 404        | Beneficiario no encontrado                   | Beneficiario interno no encontrado                                                           |
| 500        | Error interno del servidor                 | Error al validar beneficiario interno                                                         |


---

#### Códigos de Estado HTTP

| **Código de Estado** | **Descripción**                                      |
|----------------------|------------------------------------------------------|
| 200 OK               | Beneficiario interno validado correctamente           |
| 400 Bad Request      | `codProducto` o `codCuenta` no proporcionados o formato inválido |
| 404 Not Found          | Beneficiario interno no encontrado                   |
| 500 Internal Server Error | Error al validar beneficiario interno                |

---

### Notas Adicionales

*   Asegúrate de incluir un token JWT válido en el campo `token` del [Header](#21-header-en-las-peticiones).
*   Se debe proporcionar `codProducto` y `codCuenta` en el header.

---

### Ejemplo de Header para Solicitudes Posteriores

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### Header de la Solicitud (Ejemplo con codProducto y codCuenta):

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
codCuenta: 1234567890
```



### 5.3. Transferencias

---

### 5.3.1. Registrar transferencia interna

---

### Descripción

Registra una transferencia interna.


---

### Detalles del Endpoint

*   **Método HTTP:** `POST`
*   **URL:** `http://190.123.34.157:8000/transferencias`
*   **Token:** Requiere token JWT en el [Header común de la API](#21-header-en-las-peticiones).
*   **Formato de Respuesta:** `application/json`

---

### Parámetros de Solicitud

📌 **Entrada:**
Este endpoint recibe los parámetros de autenticación en el **Header** de la petición y los datos de la transferencia como Headers adicionales.

*   **Header:** Ver la definición en [Header común de la API](#21-header-en-las-peticiones). El Header debe incluir el token JWT para la autenticación, además los siguientes parámetros:

    | Nombre                    | Tipo         | Descripción                                                                                                 | Obligatorio | Ejemplo            |
    |---------------------------|--------------|-------------------------------------------------------------------------------------------------------------|-------------|--------------------|
    | `codProducto`           | `long`       | Código del producto de destino.                                                                             | Sí          | `1`                |
    | `montoTransferir`           | `decimal`      | Monto para transferir.                                                                                        | Sí          | `100.00`           |
    | `fechaContable`           | `string`       | Fecha contable de la transacción (formato: `YYYY-MM-DD`).                                                   | Sí          | `2024-02-22`       |
    | `cuentaOrigen`          | `long`      | Número de cuenta del origen.                                                                                  | Sí          | `1234567890`       |
    | `cuentaDestino`          | `long`      | Número de cuenta del beneficiario (destino).                                                                 | Sí          | `9876543210`       |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
montoTransferir: 100.00
fechaContable: 2024-02-22
cuentaOrigen: 1
cuentaDestino: 2
```



**Ejemplo de Solicitud**

---

### Ejemplo de Solicitud

**Header:** (Consulta la definición en [Header común de la API](#21-header-en-las-peticiones))

**Ejemplo de URL:**

http://190.123.34.157:8000/transferencias



**Nota:** Los datos de la transferencia (`codProducto`, `montoTransferir`, `fechaContable`, `cuentaOrigen`, `cuentaDestino`) se extraen de los parámetros que se envían en el header.

---

### Estructura de la Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

Si la solicitud es exitosa, el sistema devolverá la información de confirmación de la transferencia.

##### Estructura de la Respuesta Exitosa

La respuesta sigue la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). El campo `data` contiene la información de confirmación de la transferencia:

| Nombre                        | Tipo        | Descripción                                                                                            | Ejemplo                      |
|-------------------------------|-------------|--------------------------------------------------------------------------------------------------------|------------------------------|
| `numeroDocumentoTransaccion`  | `string`    | Número de documento de la transacción realizada.                                                        | `TRANS-20240220-0001`        |
| `fechaContable`               | `string`    | Fecha contable de la transacción (formato: `YYYY-MM-DD`).                                              | `2024-02-22`                 |
| `estadoRetornoDebito`         | `integer`   | Estado de retorno de la función de débito (1: Éxito, otros valores indican error).                    | `1`                          |
| `estadoRetornoCredito`        | `integer`   | Estado de retorno de la función de crédito (1: Éxito, otros valores indican error).                   | `1`                          |
| `mensajeError`                | `string`    | Mensaje de error si el estadoRetorno es diferente de 1.                                                 | `null`                       |

---

### Ejemplo de Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "registro transferencia interna",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Transferencia realizada con éxito",
        "data": {
            "numeroDocumentoTransaccion": "TRANS-20240220-0001",
            "fechaContable": "2024-02-22",
            "estadoRetornoDebito": 1,
            "estadoRetornoCredito": 1,
            "mensajeError": null
        }
    }
}
```

---

### Descripción de los Códigos de Error

La función de transferencia puede retornar códigos de error numéricos específicos en el campo `codigo` de la respuesta y en el campo `estadoRetornoDebito` (o `estadoRetornoCredito`) del objeto `data`. A continuación, se describe el significado de cada código:

| Código | Descripción                                      |
|--------|--------------------------------------------------|
| -2     | Cuenta no encontrada                             |
| -3     | Saldo insuficiente                               |
| -4     | No se pudo obtener la fecha                       |
| -5     | No existe caja                                   |
| -6     | No es posible actualizar el saldo en la cuenta   |
| -7     | El monto a Retirar excede el limite permitido   |
| -8     | No es posible actualizar el número de la transacción |
| -9     | No existe transacción                             |
| -10    | No es posible grabar la transacción              |
| -11    | No es posible grabar la transacción              |
| -12    | No es posible grabar el saldo en el detalle de la transacción |

---

###  Respuestas de Error

#### Respuestas de Error

Las respuestas de error siguen la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). 

Ejemplos:

#### 400 Bad Request - Parámetros de solicitud inválidos

Si alguno de los parámetros (`codProducto`, `montoTransferir`, `fechaContable`, `cuentaOrigen`, `cuentaDestino`) no es proporcionado o tiene un formato incorrecto.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "registro transferencia interna",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Formato de número inválido para los parámetros",
        "data": null
    },
    "message": "Formato de número inválido para los parámetros",
    "status": 400
}

```
#### 500 Internal Server Error - Error al realizar la transferencia (Errores de la función)

Si ocurre un error inesperado en el servidor o si la función de transferencia retorna un error específico (saldo insuficiente, cuenta no encontrada, etc.).

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "registro transferencia interna",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "-2",
        "mensajeFrontal": "Cuenta no encontrada",
        "data": {
            "numeroDocumentoTransaccion": null,
            "fechaContable": null,
            "estadoRetornoDebito": -2,
            "estadoRetornoCredito": null,
            "mensajeError": "Cuenta no encontrada"
        }
    },
    "message": "Cuenta no encontrada",
    "status": 500
}

```

#### 500 Internal Server Error - Error al realizar la transferencia (Errores de la función)
Si ocurre un error inesperado en el servidor o si la función de transferencia retorna un error específico (saldo insuficiente, cuenta no encontrada, etc.).

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "registro transferencia interna",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "-3",
        "mensajeFrontal": "Saldo insuficiente",
        "data": {
            "numeroDocumentoTransaccion": null,
            "fechaContable": null,
            "estadoRetornoDebito": -3,
            "estadoRetornoCredito": null,
            "mensajeError": "Saldo insuficiente"
        }
    },
    "message": "Saldo insuficiente",
    "status": 500
}

```

#### 500 Ejemplo de Respuesta de Error (Error Interno)
Si ocurre un error inesperado en el servidor 

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "registro transferencia interna",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al realizar la transferencia: Error en la base de datos",
        "data": null
    },
    "message": "Error al realizar la transferencia: Error en la base de datos",
    "status": 500
}

```



**Excepciones Comunes y Códigos de Estado**

---

###  Excepciones Comunes y Códigos de Estado

#### Excepciones Comunes:

| **Código** | **Descripción**                             | **Mensaje**                                                                               |
|------------|---------------------------------------------|-------------------------------------------------------------------------------------------|
| 400        | Solicitud inválida                           | Parámetros no proporcionados o formato inválido                                                                        |
| (Código de error función) | Error función de transferencia   | Mensaje de error específico de la función (ver la sección "Descripción de los Códigos de Error")                   |
| 500        | Error interno del servidor                 | Error al realizar la transferencia                                                         |


---

#### Códigos de Estado HTTP

| **Código de Estado** | **Descripción**                                      |
|----------------------|------------------------------------------------------|
| 200 OK               | Transferencia interna registrada correctamente        |
| 400 Bad Request      | Parámetros no proporcionados o formato inválido |
| 500 Internal Server Error | Error al realizar la transferencia |


---

###  Notas Adicionales

*   Asegúrate de incluir un token JWT válido en el campo `token` del [Header](#21-header-en-las-peticiones).
*   Todos los datos de la transferencia (`codProducto`, `montoTransferir`, `fechaContable`, `cuentaOrigen`, `cuentaDestino`) deben ser enviados en el header de la petición.
*   La fecha debe estar en formato `YYYY-MM-DD`.---




---

### Ejemplo de Header para Solicitudes Posteriores

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### Header de la Solicitud:

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
montoTransferir: 100.00
fechaContable: 2024-02-22
cuentaOrigen: 1
cuentaDestino: 2
```





### **5.3.2. POST /TransferenciaExterna**

---

### Descripción

Realiza un débito en la cuenta del socio para una transferencia externa. Este endpoint solo realiza el débito, validando montos y cupos diarios, pero no completa la transferencia externa.

---

### Detalles del Endpoint

*   **Método HTTP:** `POST`
*    **URL:** `http://190.123.34.157:8000/TransferenciaExterna`
*   **Token:** Requiere token JWT en el [Header común de la API](#21-header-en-las-peticiones).
*   **Formato de Respuesta:** `application/json`




---

### Parámetros de Solicitud

📌 **Entrada:**

Este endpoint recibe los parámetros de autenticación en el **Header** de la petición y los datos del débito (para la transferencia externa) como atributos en el Header.

*   **Header:** Ver la definición en [Header común de la API](#21-header-en-las-peticiones). El Header debe incluir el token JWT para la autenticación, además los siguientes parámetros:

    | Nombre        | Tipo     | Descripción                                                                    | Obligatorio | Ejemplo        |
    | ------------- | -------- | ------------------------------------------------------------------------------ | ----------- | -------------- |
    | `Token`       | `string` | Token de autenticación (Bearer Token). Ejemplo: `Bearer eyJhbGciOiJIUzI1Ni...` | Si          | `Bearer ...`   |
    | `codProducto` | `string` | Código del producto de la cuenta origen.                                       | Sí          | `"1"`          |
    | `codCuenta`   | `string` | Número de la cuenta origen a debitar.                                          | Sí          | `"1"` |
    | `valorRetiro` | `string` | Monto a debitar para la transferencia externa.                                 | Sí          | `"100.00"`     |
    | `fecha`       | `string` | Fecha contable de la transacción (formato: `YYYY-MM-DD`).                      | Sí          | `"2025-03-11"` |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
codCuenta: 1
valorRetiro: 100.00
fecha: 2024-03-13
```



**Sección 3: Ejemplo de Solicitud**

---

### Ejemplo de Solicitud

**Header:** (Consulta la definición en [Header común de la API](#21-header-en-las-peticiones))

**Ejemplo de URL:**

http://190.123.34.157:8000/TransferenciaExterna

**Nota:** Los datos del débito (`codProducto`, `codCuenta`, `valorRetiro`, `fecha`) se extraen de los parámetros que se envían en el header.

---

###  Estructura de la Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

Si el débito para la transferencia externa se realiza con éxito, el sistema devolverá la información de confirmación del débito.

##### Estructura de la Respuesta Exitosa

La respuesta sigue la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). El campo `data` contiene la información de confirmación del débito:

| Nombre                       | Tipo      | Descripción                                                                             | Ejemplo               |
| ---------------------------- | --------- | --------------------------------------------------------------------------------------- | --------------------- |
| `numeroDocumentoTransaccion` | `string`  | Número de documento de la transacción de débito realizada.                              | `NDSPI-20240223-0001` |
| `fechaContable`              | `string`  | Fecha contable de la transacción (formato: `YYYY-MM-DD`).                               | `2024-02-23`          |
| `estadoRetorno`              | `integer` | Estado de retorno de la función (1: Éxito, otros valores indican error).                | `1`                   |
| `mensajeError`               | `string`  | Mensaje de error si `estadoRetorno` es diferente de 1. Nulo si la operación es exitosa. | `null`                |


---

### Ejemplo de Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": null,
        "fechaMsj": "2025-03-12T22:22:07.203891200",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Desacreditación realizada con éxito",
        "data": {
            "numeroDocumentoTransaccion": "NDSPI-Wed Mar 12 22:22:07 ECT 2025-0001",
            "fechaContable": "2025-03-13T03:22:07.203+00:00",
            "estadoRetorno": 1,
            "mensajeError": null
        }
    },
    "message": "Desacreditación realizada con éxito",
    "status": 200
}
```



**Sección 6: Descripción de los Códigos de Error**

---

###  Descripción de los Códigos de Error

La función de débito puede retornar códigos de error numéricos específicos en el campo `codigo` de la respuesta y en el campo `estadoRetorno` del objeto `data`. A continuación, se describe el significado de cada código:

| Código | Descripción                                                   |
| ------ | ------------------------------------------------------------- |
| -2     | Cuenta no encontrada                                          |
| -3     | Saldo insuficiente                                            |
| -4     | No se pudo obtener la fecha                                   |
| -5     | No existe caja                                                |
| -6     | No es posible actualizar el saldo en la cuenta                |
| -7     | El monto a Retirar excede el limite permitido                 |
| -8     | No es posible actualizar el número de la transacción          |
| -9     | No existe transacción                                         |
| -10    | No es posible grabar la transacción                           |
| -11    | No es posible grabar la transacción                           |
| -12    | No es posible grabar el saldo en el detalle de la transacción |


---

### Respuestas de Error

#### Respuestas de Error

Las respuestas de error siguen la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). Ejemplos:

#### 400 Bad Request - Parámetros de solicitud inválidos

Si alguno de los parámetros (`codProducto`, `codCuenta`, `valorRetiro`, `fecha`) no es proporcionado o tiene un formato incorrecto.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito transferencia externa",
        "fechaMsj": "2025-02-23T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Invalid number format in headers",
        "data": null
    },
    "message": "Invalid number format in headers",
    "status": 400
}
```



#### 500 Internal Server Error - Error al realizar el débito (Errores de la función)

Si ocurre un error inesperado en el servidor o si la función de débito retorna un error específico (saldo insuficiente, cuenta no encontrada, etc.).

**Ejemplo de Respuesta de Error (Cuenta no encontrada)**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito transferencia externa",
        "fechaMsj": "2025-02-23T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "-2",
        "mensajeFrontal": "Cuenta no encontrada",
        "data": null
    },
    "message": "Cuenta no encontrada",
    "status": 500
}
```

#### 500 Internal Server Error - Error al realizar el débito (Error Interno)


```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito transferencia externa",
        "fechaMsj": "2025-02-23T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al realizar el débito: Error en la base de datos",
        "data": null
    },
    "message": "Error al realizar el débito: Error en la base de datos",
    "status": 500
}
```


**Sección 8: Excepciones Comunes y Códigos de Estado**

---

### Excepciones Comunes y Códigos de Estado

#### Excepciones Comunes:

| **Código**                | **Descripción**            | **Mensaje**                                                                                      |
| ------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------ |
| 400                       | Solicitud inválida         | Parámetros no proporcionados o formato inválido                                                  |
| (Código de error función) | Error función de débito    | Mensaje de error específico de la función (ver la sección "Descripción de los Códigos de Error") |
| 500                       | Error interno del servidor | Error al realizar el débito                                                                      |

---

#### Códigos de Estado HTTP

| **Código de Estado**      | **Descripción**                                           |
| ------------------------- | --------------------------------------------------------- |
| 200 OK                    | Débito realizado correctamente para transferencia externa |
| 400 Bad Request           | Parámetros no proporcionados o formato inválido           |
| 500 Internal Server Error | Error al realizar el débito                               |


---

### Notas Adicionales

*   Asegúrate de incluir un token JWT válido en el campo `token` del [Header](#21-header-en-las-peticiones).
*   Todos los datos del débito (`codProducto`, `codCuenta`, `valorRetiro`, `fecha`) deben ser enviados en el header de la petición.
*   La fecha debe estar en formato `YYYY-MM-DD`.


---

### Ejemplo de Header para Solicitudes Posteriores

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### Header de la Solicitud:

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
codCuenta: 123
valorRetiro: 100.00
fecha: 2024-02-23
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










---

### 5.4.2. Obtener comisión

---

### Descripción

Obtiene la comisión basada en el código de transacción.

---

### Detalles del Endpoint

*   **Método HTTP:** `GET`
*   **URL:** `http://190.123.34.157:8000/comisiones`
*   **Token:** Requiere token JWT en el [Header común de la API](#21-header-en-las-peticiones).
*   **Formato de Respuesta:** `application/json`


---

### Parámetros de Solicitud

📌 **Entrada:**
Este endpoint recibe los parámetros de autenticación en el **Header** de la petición. No recibe parámetros adicionales en el Header ni en la URL.  

*   **Header:** Ver la definición en [Header común de la API](#21-header-en-las-peticiones). El Header debe incluir el token JWT para la autenticación.


---

### Ejemplo de Solicitud

**Header:** (Consulta la definición en [Header común de la API](#21-header-en-las-peticiones))

**Ejemplo de URL:** 

http://190.123.34.157:8000/comisiones



**Nota:** Este endpoint no requiere parámetros adicionales en el Header o en la URL.




---

### Estructura de la Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

Si la solicitud es exitosa, el sistema devolverá la información de la comisión.

##### Estructura de la Respuesta Exitosa

La respuesta sigue la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). El campo `data` contiene una lista de comisiones (aunque normalmente solo habrá una). Cada comisión tendrá los siguientes campos:

| Nombre          | Tipo        | Descripción                                                                           | Ejemplo                |
|-----------------|-------------|---------------------------------------------------------------------------------------|------------------------|
| `codigo`       | `string`    | Código de la comisión.                                                                | `001`                  |
| `descripcion`  | `string`    | Descripción de la comisión.                                                           | `comisión transferencia` |
| `valor`        | `number`    | Valor de la comisión.                                                                 | `2.50`                 |


---

###  Ejemplo de Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

```json
{
    "data": [
            {
                "codigo": "C",
                "descripcion": "Comision Consultas",
                "valor": 0.30
            },
            {
                "codigo": "T",
                "descripcion": "Comision Transferencias",
                "valor": 0.50
            }
        ]
}

```



---

###  Respuestas de Error

#### Respuestas de Error

Las respuestas de error siguen la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). Ejemplos:

#### 400 Bad Request - Parámetros de solicitud inválidos

Este error podría ocurrir si se esperara algún parámetro (aunque el código actual no lo requiere).

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtener comision",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Invalid request parameters",
        "data": null
    },
    "message": "Invalid request parameters",
    "status": 400
}
```

#### 500 Internal Server Error - Error obteniendo la comisión

Si ocurre un error inesperado en el servidor al intentar obtener la comisión.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "obtener comision",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error obteniendo la comisión: Error en la base de datos",
        "data": null
    },
    "message": "Error obteniendo la comisión: Error en la base de datos",
    "status": 500
}
```


**Excepciones Comunes y Códigos de Estado**

---

### Excepciones Comunes y Códigos de Estado

#### Excepciones Comunes:

| **Código** | **Descripción**                             | **Mensaje**                                                                               |
|------------|---------------------------------------------|-------------------------------------------------------------------------------------------|
| 400        | Solicitud inválida                           | Parámetros de solicitud inválidos (si se implementaran)                                                                        |
| 500        | Error interno del servidor                 | Error obteniendo la comisión                                                         |


---

#### Códigos de Estado HTTP

| **Código de Estado** | **Descripción**                                      |
|----------------------|------------------------------------------------------|
| 200 OK               | Comisión obtenida correctamente                       |
| 400 Bad Request      | Parámetros de solicitud inválidos (si se implementaran) |
| 500 Internal Server Error | Error al obtener la comisión |


---

###  Notas Adicionales

*   Asegúrate de incluir un token JWT válido en el campo `token` del [Header](#21-header-en-las-peticiones).
*   El código de comisión (ejemplo: 001 comisión de transferencias SPI) para obtener la comisión se debe configurar directamente en el servicio (backend).

---

###  Ejemplo de Header para Solicitudes Posteriores

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### Header de la Solicitud:

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```




### 5.5.  Operaciones de Cuenta

---

### 5.5.1. Débito

---

### Descripción

Realiza un débito en la cuenta del socio.

---

### Detalles del Endpoint

*   **Método HTTP:** `POST`
*   **URL:** `http://190.123.34.157:8000/debitos`
*   **Token:** Requiere token JWT en el [Header común de la API](#21-header-en-las-peticiones).
*   **Formato de Respuesta:** `application/json`


---

### Parámetros de Solicitud

📌 **Entrada:**
Este endpoint recibe los parámetros de autenticación en el **Header** de la petición y los datos del débito como atributos en el Header.

*   **Header:** Ver la definición en [Header común de la API](#21-header-en-las-peticiones). El Header debe incluir el token JWT para la autenticación, además los siguientes parámetros:

    | Nombre            | Tipo      | Descripción                                                                                                  | Obligatorio | Ejemplo            |
    |-------------------|-----------|--------------------------------------------------------------------------------------------------------------|-------------|--------------------|
    | `codProducto`    | `long`    | Código del producto al cual se va a realizar el débito.                                                     | Sí          | `1`                |
    | `codCuenta`      | `long`    | Número de cuenta a la cual se realizará el débito.                                                           | Sí          | `1234567890`       |
    | `valorRetiro`     | `decimal` | Monto a debitar.                                                                                             | Sí          | `100.00`           |
    | `fecha`           | `string`  | Fecha contable de la transacción (formato: `YYYY-MM-DD`).                                                   | Sí          | `2024-02-22`       |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
codCuenta: 1234567890
valorRetiro: 100.00
fecha: 2024-02-22
```


**Ejemplo de Solicitud**

---

### Ejemplo de Solicitud

**Header:** (Consulta la definición en [Header común de la API](#21-header-en-las-peticiones))

**Ejemplo de URL:**

http://190.123.34.157:8000/debitos



**Nota:** Los datos del débito (`codProducto`, `codCuenta`, `valorRetiro`, `fecha`) se extraen de los parámetros que se envían en el header.

---

###  Estructura de la Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

Si la solicitud es exitosa, el sistema devolverá la información de confirmación del débito.

##### Estructura de la Respuesta Exitosa

La respuesta sigue la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). El campo `data` contiene la información de confirmación del débito:

| Nombre                        | Tipo        | Descripción                                                                                            | Ejemplo                      |
|-------------------------------|-------------|--------------------------------------------------------------------------------------------------------|------------------------------|
| `numeroDocumentoTransaccion`  | `string`    | Número de documento de la transacción realizada.                                                        | `NDSPI-20240220-0001`      |
| `fechaContable`               | `string`    | Fecha contable de la transacción (formato: `YYYY-MM-DD`).                                              | `2024-02-20`                 |
| `estadoRetorno`         | `integer`   | Estado de retorno de la función (1: Éxito, otros valores indican error).                                | `1`                          |
| `mensajeError`                | `string`    | Mensaje de error si el estadoRetorno es diferente de 1.                                                 | `null`                       |


---

###  Ejemplo de Respuesta Exitosa

#### Respuesta Exitosa (200 OK)

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Débito realizado con éxito",
        "data": {
            "numeroDocumentoTransaccion": "NDSPI-20240220-0001",
            "fechaContable": "2024-02-22",
            "estadoRetorno": 1,
            "mensajeError": null
        }
    }
}
```

---

###  Descripción de los Códigos de Error

La función de débito puede retornar códigos de error numéricos específicos en el campo `codigo` de la respuesta y en el campo `estadoRetorno` del objeto `data`. A continuación, se describe el significado de cada código:

| Código | Descripción                                      |
|--------|--------------------------------------------------|
| -2     | Cuenta no encontrada                             |
| -3     | Saldo insuficiente                               |
| -4     | No se pudo obtener la fecha                       |
| -5     | No existe caja                                   |
| -6     | No es posible actualizar el saldo en la cuenta   |
| -7     | El monto a Retirar excede el limite permitido   |
| -8     | No es posible actualizar el número de la transacción |
| -9     | No existe transacción                             |
| -10    | No es posible grabar la transacción              |
| -11    | No es posible grabar la transacción              |
| -12    | No es posible grabar el saldo en el detalle de la transacción |


---

### Respuestas de Error

#### Respuestas de Error

Las respuestas de error siguen la estructura [RespuestaComun](#22-respuestacomun-en-las-respuestas). Ejemplos:

#### 400 Bad Request - Parámetros de solicitud inválidos

Si alguno de los parámetros (`codProducto`, `codCuenta`, `valorRetiro`, `fecha`) no es proporcionado o tiene un formato incorrecto.

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "400",
        "mensajeFrontal": "Invalid number format in headers",
        "data": null
    },
    "message": "Invalid number format in headers",
    "status": 400
}
```
#### 500 Internal Server Error - Error al realizar el débito (Errores de la función)

Si ocurre un error inesperado en el servidor o si la función de débito retorna un error específico (saldo insuficiente, cuenta no encontrada, etc.).

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "-2",
        "mensajeFrontal": "Cuenta no encontrada",
        "data": null
    },
    "message": "Cuenta no encontrada",
    "status": 500
}
```

#### 500 Internal Server Error - Error al realizar el débito (Errores de la función)

Ejemplo de Respuesta de Error (Saldo Insuficiente):

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "-3",
        "mensajeFrontal": "Saldo insuficiente",
        "data": null
    },
    "message": "Saldo insuficiente",
    "status": 500
}
```

#### 500 Internal Server Error - Error al realizar el débito (Errores de la función)

Ejemplo de Respuesta de Error (Error Interno):

**Ejemplo de Respuesta de Error:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": "realizar debito",
        "fechaMsj": "2025-02-21T10:00:00.000+00:00",
        "estadoTransaccion": "ERROR",
        "codigo": "500",
        "mensajeFrontal": "Error al realizar el débito: Error en la base de datos",
        "data": null
    },
    "message": "Error al realizar el débito: Error en la base de datos",
    "status": 500
}
```


---

### Excepciones Comunes y Códigos de Estado

#### Excepciones Comunes:

| **Código** | **Descripción**                             | **Mensaje**                                                                               |
|------------|---------------------------------------------|-------------------------------------------------------------------------------------------|
| 400        | Solicitud inválida                           | Parámetros no proporcionados o formato inválido                                                                        |
| (Código de error función) | Error función de débito       | Mensaje de error específico de la función (ver la sección "Descripción de los Códigos de Error")                   |
| 500        | Error interno del servidor                 | Error al realizar el débito                                                         |



---

#### Códigos de Estado HTTP

| **Código de Estado** | **Descripción**                                      |
|----------------------|------------------------------------------------------|
| 200 OK               | Débito realizado correctamente                     |
| 400 Bad Request      | Parámetros no proporcionados o formato inválido |
| 500 Internal Server Error | Error al realizar el débito |



---

###  Notas Adicionales

*   Asegúrate de incluir un token JWT válido en el campo `token` del [Header](#21-header-en-las-peticiones).
*   Todos los datos del débito (`codProducto`, `codCuenta`, `valorRetiro`, `fecha`) deben ser enviados en el header de la petición.
*   La fecha debe estar en formato `YYYY-MM-DD`.

---

###  Ejemplo de Header para Solicitudes Posteriores

Cuando se haga una solicitud a este endpoint, recuerda incluir el token de autenticación obtenido en el endpoint `/auth/authenticate` como un Token en el encabezado de la solicitud.

#### Header de la Solicitud:

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
codCuenta: 123
valorRetiro: 100.00
fecha: 2024-02-22
```




### **5.5.2. POST /reversos**

Se realiza una devolución (acreditación) de dinero al socio en caso de algún error en la transacción que se esta realizando.

#### **Detalles del Endpoint**

- **Método HTTP:** `POST`
- `http://190.123.34.157:8000/reverso`
- **Token:** Requiere token JWT
- **Formato de Solicitud:** `application/json` (a través de headers)
****


#### **Parámetros de Solicitud**

📌 **Entrada:**
Este endpoint recibe los parámetros necesarios para realizar el reverso a través de los **Headers** de la petición.

| **Nombre**       | **Tipo** | **Descripción**                                                                 | **Obligatorio** | **Ejemplo**    |
| ---------------- | -------- | ------------------------------------------------------------------------------- | --------------- | -------------- |
| `Token`          | `string` | Token de autenticación (Bearer Token).  Ejemplo: `Bearer eyJhbGciOiJIUzI1Ni...` | Sí              | `Bearer ...`   |
| `codProducto`    | `string` | Código del producto asociado a la transacción.                                  | Sí              | `"12345"`      |
| `montoAcreditar` | `string` | Monto a acreditar en la cuenta destino.                                         | Sí              | `"100.50"`     |
| `fechaContable`  | `string` | Fecha contable de la transacción (formato: `yyyy-MM-dd`).                       | Sí              | `"2024-01-01"` |
| `cuentaDestino`  | `string` | Número de cuenta destino a la cual se realizará el reverso.                     | Sí              | `"0123456789"` |

📌 **Ejemplo de Header en la Solicitud:**

```http
Token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
codProducto: 1
montoAcreditar: 100.50
cuentaDestino: 1
fechaContable: 2025-03-11
```


**Sección 3: Respuesta Exitosa**

### **Respuesta Exitosa**

#### **Respuesta Exitosa (200 OK)**

Si la acreditación se realiza exitosamente, el sistema devuelve la información de la transacción.

#### **Estructura de la Respuesta Exitosa:**

| **Nombre**                   | **Tipo**  | **Descripción**                                                            |
| ---------------------------- | --------- | -------------------------------------------------------------------------- |
| `estadoRetornoCredito`       | `integer` | Código de estado del resultado de la acreditación. `1` indica éxito.       |
| `mensajeError`               | `string`  | Mensaje descriptivo del resultado de la operación.  Vacío si es exitoso.   |
| `numeroDocumentoTransaccion` | `string`  | Número de documento asociado a la transacción de reverso.                  |
| `fechaContable`              | `string`  | Fecha contable de la transacción (formato: `yyyy-MM-ddTHH:mm:ss.SSSZ`).    |
| ... (Otros campos)           | ...       | Pueden existir otros campos dependiendo de la implementación del servicio. |

#### **Ejemplo de Respuesta Exitosa:**

```json
{
    "data": {
        "idRespuesta": "0",
        "originalIdServicio": realizar reverso,
        "fechaMsj": "2025-03-12T21:09:55.952633300",
        "estadoTransaccion": "OK",
        "codigo": "0",
        "mensajeFrontal": "Acreditación realizada con éxito",
        "data": {
            "numeroDocumentoTransaccion": "ACREDITA-Wed Mar 12 00:00:00 ECT 2025-0001",
            "fechaContable": "2025-03-12T05:00:00.000+00:00",
            "estadoRetornoDebito": null,
            "estadoRetornoCredito": 1,
            "mensajeError": null
        }
    },
    "message": "Acreditación realizada con éxito",
    "status": 200
}
```

#### 500 Internal Server Error - Error en la Acreditación

Si ocurre un error interno en el servicio al intentar realizar la acreditación (ej: falla la conexión a la base de datos, ocurre una excepción no controlada en el servicio).

**Ejemplo de Respuesta de Error:**

```json
{
  "data": null,
  "message": "Error en la acreditación: [Mensaje de error específico]",
  "status": 500
}
```


**Sección 5: Excepciones Comunes y Códigos de Estado**

---

### **Excepciones Comunes y Códigos de Estado**

#### **Excepciones Comunes:**

| **Código** | **Descripción**            | **Mensaje**                                     |
| ---------- | -------------------------- | ----------------------------------------------- |
| `400`      | Parámetros inválidos       | `Formato de número inválido`                    |
| `500`      | Error interno del servidor | `Error en la acreditación: [Mensaje detallado]` |

---

#### **Códigos de Estado HTTP:**

| **Código de Estado**        | **Descripción**                                |
| --------------------------- | ---------------------------------------------- |
| `200 OK`                    | Acreditación realizada correctamente.          |
| `400 Bad Request`           | Uno o más parámetros de entrada son inválidos. |
| `500 Internal Server Error` | Error al realizar la acreditación.             |


---

#### **Notas Adicionales**

- **Autenticación:** Se requiere un token JWT válido en el encabezado `Token` de la solicitud.

- **Manejo de Errores:**  Es importante revisar el campo `mensajeError` en las respuestas de error para obtener información más detallada sobre la causa del fallo.

---

