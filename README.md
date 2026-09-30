# 🚀 node-api-mongo: El Registro Nostálgico del "pasado"

[![Node.js](https://img.shields.io/badge/Node.js-v14%2B-green.svg)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.18.2-lightgrey.svg)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Local-brightgreen.svg)](https://www.mongodb.com/)
[![Mongoose](https://img.shields.io/badge/Mongoose-7.3.0-red.svg)](https://mongoosejs.com/)
[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)

>
> **node-api-mongo** es una API RESTful desarrollada con **Node.js**, **Express** y **MongoDB** (a través de **Mongoose**), concebida con rigor de ingeniería de software y un ingenioso enfoque nostálgico: operar como bitácora digital para documentar, catalogar y homenajear a aquellas parejas y personas significativas que han dejado una huella indeleble en nuestras vidas. ¿Por qué la base de datos se titula `pasado`? Porque toda experiencia sentimental o académica compone nuestra historia; y ahora, gracias a una arquitectura limpia, goza de persistencia confiable, tipado estricto y marcas temporales automáticas.

---

## 📌 Autoría y Contexto Académico

| Metadato | Detalle |
| :--- | :--- |
| **Desarrollador** | **Salomon Montilla** |
| **Asignatura** | **Bases de Datos Avanzadas** |
| **Nivel Académico** | **Semestre 6** |
| **Institución** | Corporación Universitaria Autónoma del Cauca |
| **Proyecto** | `node-api-mongo` |
| **Base de Datos** | `pasado` (MongoDB Community Server, puerto `27017`) |

---

### Aspectos técnicos destacados:
* **Separación de Capas:** Aislamiento modular entre enrutamiento (`routes/`), lógica de controladores (`controllers/`), contratos de datos (`models/`) e inicialización del servidor (`app.js`, `index.js`).
* **Modelo Enriquecido con Timestamps:** Esquema Mongoose (`ParejaSchema`) con validaciones de tipo, rangos numéricos (`min: 1, max: 10`), valores por defecto y gestión nativa de `createdAt` y `updatedAt`.
* **Procesamiento de Payloads Complejos:** Soporte para arrays de strings (`cualidades`), fechas ISO 8601 (`fechaInicio`, `fechaFin`) y objetos JSON anidados.
* **Metadatos y Health Check Dinámico:** Endpoint raíz (`GET /`) que certifica el estado operativo, la versión, la autoría y la base de datos activa.

---

## 🛠️ Stack Tecnológico

* **Entorno de ejecución:** [Node.js](https://nodejs.org/) (v14.x+)
* **Framework Web:** [Express.js](https://expressjs.com/) (v4.18.2)
* **Motor de Base de Datos:** [MongoDB](https://www.mongodb.com/) (Instancia local, base `pasado`)
* **ODM (Object Data Modeling):** [Mongoose](https://mongoosejs.com/) (v7.3.0)
* **Middleware multiparte:** [connect-multiparty](https://www.npmjs.com/package/connect-multiparty) (v2.2.0)
* **Herramienta de desarrollo:** [Nodemon](https://nodemon.io/) (v2.0.22) para recarga en caliente

## ⚙️ Instalación y Puesta en Marcha

### Prerrequisitos

* **Node.js** (versión 14.x, 16.x, 18.x o superior) y **npm**:
  ```bash
  node -v
  npm -v
  ```
* **MongoDB Community Server**: Activo en el puerto estándar `27017`.
  * **macOS (Homebrew):**
    ```bash
    brew services start mongodb-community
    ```
  * **Linux (systemd):**
    ```bash
    sudo systemctl start mongod
    ```
  * **Windows:**
    ```cmd
    net start MongoDB
    ```

### Pasos de Configuración y Ejecución

1. **Ingresar al directorio del proyecto:**
   ```bash
   cd /Users/salomontilla/Universidad/semestre_6/bd_avanzadas/node-api-mongo
   ```

2. **Instalar los paquetes de dependencias:**
   ```bash
   npm install
   ```

3. **Iniciar el servidor en modo desarrollo (con Nodemon):**
   ```bash
   npm start
   ```

   Al conectarse exitosamente con la base de datos `pasado`, se imprimirá el siguiente banner en consola:
   ```text
   Database connected successfully
   ===============================================================
   📖 API REST node-api-mongo | Colección del 'pasado'
   Desarrollador: Salomon Montilla
   Propósito: Documentar relaciones y personas que dejaron huella
   Servidor activo en: http://localhost:3000
   ===============================================================
   ```

> [!TIP]
> Por defecto, la API se expone en el puerto `3000`. Puedes definir un puerto personalizado mediante la variable de entorno `PORT`:
> ```bash
> PORT=8080 npm start
> ```

---

## 📊 Modelo de Datos Ampliado (Mongoose Schema)

El modelo está definido en `models/pareja.js` con el esquema `ParejaSchema` y mapea formalmente a la colección `parejas` dentro de la base de datos `pasado`:

```javascript
const ParejaSchema = new Schema({
  nombre: { type: String, required: true },
  edad: { type: Number, required: true },
  mensaje: { type: String, default: null },
  apodo: { type: String, default: null },
  fechaInicio: { type: Date, default: null },
  fechaFin: { type: Date, default: null },
  leccionAprendida: { type: String, default: null },
  impacto: { type: Number, min: 1, max: 10, default: 5 },
  cancion: { type: String, default: null },
  lugarFavorito: { type: String, default: null },
  cualidades: { type: [String], default: [] }
}, {
  timestamps: true // Genera automáticamente createdAt y updatedAt
})
```

### Diccionario de Datos Completo

| Atributo | Tipo Mongoose | Requerido | Valor por Defecto | Descripción & Sentido Nostálgico |
| :--- | :--- | :---: | :--- | :--- |
| `_id` | `ObjectId` | Auto | `ObjectId()` | Identificador único hexadecimal asignado por MongoDB. |
| `nombre` | `String` | **Sí** | - | Nombre de la persona o pareja que dejó huella. |
| `edad` | `Number` | **Sí** | - | Edad representativa durante la etapa compartida. |
| `mensaje` | `String` | No | `null` | Dedicatoria, recuerdo, palabras no dichas o reflexión. |
| `apodo` | `String` | No | `null` | Sobrenombre cariñoso con el que se recordará la relación. |
| `fechaInicio` | `Date` | No | `null` | Fecha de inicio de la relación o del primer encuentro (ISO 8601). |
| `fechaFin` | `Date` | No | `null` | Fecha de culminación de la etapa o cierre de ciclo (ISO 8601). |
| `leccionAprendida` | `String` | No | `null` | Principal aprendizaje o madurez obtenida tras la vivencia. |
| `impacto` | `Number` | No | `5` | Escala emocional del 1 al 10 sobre cuánto marcó tu vida. |
| `cancion` | `String` | No | `null` | Canción, artista o banda sonora que evoca los mejores momentos. |
| `lugarFavorito` | `String` | No | `null` | Rincón, café, ciudad o escenario inolvidable. |
| `cualidades` | `[String]` | No | `[]` | Colección de virtudes y rasgos admirables de la persona. |
| `createdAt` | `Date` | Auto | Timestamp actual | Fecha exacta en la que se inmortalizó el registro. |
| `updatedAt` | `Date` | Auto | Timestamp actual | Fecha de la última edición o reevaluación del recuerdo. |
| `__v` | `Number` | Auto | `0` | Versión interna de Mongoose para concurrencia optimista. |

---

## 📡 Catálogo Exhaustivo de Endpoints

URL Base local: `http://localhost:3000`

### Matriz Resumen de Rutas

| Método | Endpoint | Acción / Propósito |
| :--- | :--- | :--- |
| `GET` | `/` | Health check, autoría y metadatos de la base de datos `pasado` |
| `GET` | `/api/parejas` | Recuperar el archivo histórico completo de parejas del pasado |
| `GET` | `/api/parejas/:id` | Consultar la ficha detallada de una pareja por su `_id` |
| `POST` | `/api/parejas/save-pareja` | Inmortalizar una nueva historia en el "pasado" |
| `PUT` | `/api/parejas/edit-pareja/:id` | Actualizar lecciones, reflexiones, canciones o atributos |
| `DELETE` | `/api/parejas/delete-pareja/:id` | Cerrar ciclo: eliminar definitivamente un registro del sistema |

---

### 1. Metadatos del Sistema y Health Check

#### `GET /`
Verifica la disponibilidad de la API y expone los metadatos de autoría y de la base de datos `pasado`.

* **URL:** `http://localhost:3000/`
* **Método:** `GET`
* **Headers:** No requeridos
* **Respuesta Exitosa (200 OK):**
  ```json
  {
    "name": "node-api-mongo",
    "version": "1.0.0",
    "description": "El registro del 'pasado': API para documentar relaciones y personas importantes que han dejado huella en nuestras vidas",
    "author": "Salomon Montilla",
    "database": "pasado",
    "status": "online"
  }
  ```

---

### 2. Listar Todas las Parejas

#### `GET /api/parejas`
Recupera todos los documentos registrados en la colección `parejas` dentro de la base de datos `pasado`.

* **URL:** `http://localhost:3000/api/parejas`
* **Método:** `GET`
* **Respuesta Exitosa (200 OK):**
  ```json
  [
    {
      "_id": "65160ef917031405e3208761",
      "nombre": "Carlos y Sofia",
      "edad": 24,
      "mensaje": "Bailarines de salsa - inolvidable competencia en Cali",
      "apodo": "Los Reyes del Compás",
      "fechaInicio": "2020-02-14T00:00:00.000Z",
      "fechaFin": "2022-11-30T00:00:00.000Z",
      "leccionAprendida": "La sincronía en el baile no siempre garantiza sincronía de metas",
      "impacto": 8,
      "cancion": "Aquel Lugar - Adolescentes Orquesta",
      "lugarFavorito": "Bulevar del Río, Cali",
      "cualidades": [
        "Alegre",
        "Disciplinada",
        "Excelente sentido del humor"
      ],
      "createdAt": "2026-09-30T14:10:00.000Z",
      "updatedAt": "2026-09-30T14:10:00.000Z",
      "__v": 0
    },
    {
      "_id": "65160f0a17031405e3208762",
      "nombre": "Mateo y Valentina",
      "edad": 22,
      "mensaje": "Noches interminables de estudio, pizzas y café",
      "apodo": "Compañeros de Biblioteca",
      "fechaInicio": "2021-08-01T00:00:00.000Z",
      "fechaFin": "2023-06-15T00:00:00.000Z",
      "leccionAprendida": "El amor maduro apoya las vocaciones individuales",
      "impacto": 9,
      "cancion": "Sparks - Coldplay",
      "lugarFavorito": "Café Moravia, Popayán",
      "cualidades": [
        "Inteligente",
        "Resiliente",
        "Empática"
      ],
      "createdAt": "2026-09-30T14:25:00.000Z",
      "updatedAt": "2026-09-30T14:25:00.000Z",
      "__v": 0
    }
  ]
  ```
* **Respuestas de Error:**
  * `404 Not Found`: Si la colección está vacía.
    ```json
    {
      "message": "No data found"
    }
    ```
  * `500 Internal Server Error`:
    ```json
    {
      "message": "Error: <descripción_del_error>"
    }
    ```

---

### 3. Consultar una Pareja por ID

#### `GET /api/parejas/:id`
Busca un registro individual a través de su `_id` de MongoDB.

* **URL:** `http://localhost:3000/api/parejas/:id`
* **Método:** `GET`
* **Parámetros de Ruta:**
  * `id` *(obligatorio)*: Cadena hexadecimal de 24 caracteres del documento.
* **Ejemplo de Petición:** `GET http://localhost:3000/api/parejas/65160ef917031405e3208761`
* **Respuesta Exitosa (200 OK):**
  ```json
  {
    "_id": "65160ef917031405e3208761",
    "nombre": "Carlos y Sofia",
    "edad": 24,
    "mensaje": "Bailarines de salsa - inolvidable competencia en Cali",
    "apodo": "Los Reyes del Compás",
    "fechaInicio": "2020-02-14T00:00:00.000Z",
    "fechaFin": "2022-11-30T00:00:00.000Z",
    "leccionAprendida": "La sincronía en el baile no siempre garantiza sincronía de metas",
    "impacto": 8,
    "cancion": "Aquel Lugar - Adolescentes Orquesta",
    "lugarFavorito": "Bulevar del Río, Cali",
    "cualidades": [
      "Alegre",
      "Disciplinada",
      "Excelente sentido del humor"
    ],
    "createdAt": "2026-09-30T14:10:00.000Z",
    "updatedAt": "2026-09-30T14:10:00.000Z",
    "__v": 0
  }
  ```
* **Respuestas de Error:**
  * `404 Not Found`: Documento no encontrado o ID ausente.
    ```json
    {
      "message": "pareja not found"
    }
    ```
  * `500 Internal Server Error`: ID malformado o falla de base de datos.
    ```json
    {
      "message": "Internal error-> <descripción_del_error>"
    }
    ```

---

### 4. Inmortalizar una Nueva Pareja en el "pasado"

#### `POST /api/parejas/save-pareja`
Registra un nuevo documento en la colección `parejas`.

* **URL:** `http://localhost:3000/api/parejas/save-pareja`
* **Método:** `POST`
* **Headers:** `Content-Type: application/json`
* **Cuerpo de la Solicitud (Body JSON Completo):**
  ```json
  {
    "nombre": "Andrés y Camila",
    "edad": 26,
    "mensaje": "Nos conocimos en un festival de música; gran etapa de crecimiento mutuo",
    "apodo": "Los Mochileros",
    "fechaInicio": "2021-06-15T00:00:00.000Z",
    "fechaFin": "2023-08-20T00:00:00.000Z",
    "leccionAprendida": "Aprender a escuchar activamente y valorar los espacios propios",
    "impacto": 9,
    "cancion": "Sparks - Coldplay",
    "lugarFavorito": "Mirador de San Antonio, Cali",
    "cualidades": [
      "Sentido del humor único",
      "Empatía incondicional",
      "Puntualidad admirable",
      "Puntada artística para pintar"
    ]
  }
  ```
* **Respuesta Exitosa (200 OK):**
  ```json
  {
    "pareja": {
      "_id": "6516104217031405e3208765",
      "nombre": "Andrés y Camila",
      "edad": 26,
      "mensaje": "Nos conocimos en un festival de música; gran etapa de crecimiento mutuo",
      "apodo": "Los Mochileros",
      "fechaInicio": "2021-06-15T00:00:00.000Z",
      "fechaFin": "2023-08-20T00:00:00.000Z",
      "leccionAprendida": "Aprender a escuchar activamente y valorar los espacios propios",
      "impacto": 9,
      "cancion": "Sparks - Coldplay",
      "lugarFavorito": "Mirador de San Antonio, Cali",
      "cualidades": [
        "Sentido del humor único",
        "Empatía incondicional",
        "Puntualidad admirable",
        "Puntada artística para pintar"
      ],
      "createdAt": "2026-09-30T15:35:00.000Z",
      "updatedAt": "2026-09-30T15:35:00.000Z",
      "__v": 0
    }
  }
  ```
* **Respuestas de Error:**
  * `400 Bad Request`: Si no se proveen `nombre` y `edad`.
    ```json
    {
      "message": "Data is not right"
    }
    ```
  * `404 Not Found`: Falla al persistir el documento.
    ```json
    {
      "message": "Error saving the document"
    }
    ```
  * `500 Internal Server Error`:
    ```json
    {
      "message": "Error while saving the document"
    }
    ```

---

### 5. Actualizar Pareja

#### `PUT /api/parejas/edit-pareja/:id`
Modifica las propiedades de una pareja existente y devuelve el documento actualizado (`returnDocument: 'after'`).

* **URL:** `http://localhost:3000/api/parejas/edit-pareja/:id`
* **Método:** `PUT`
* **Parámetros de Ruta:**
  * `id` *(obligatorio)*: `_id` de la pareja a actualizar.
* **Headers:** `Content-Type: application/json`
* **Cuerpo de la Solicitud (Body JSON con Campos Ampliados):**
  ```json
  {
    "nombre": "Andrés y Camila Gómez",
    "edad": 27,
    "mensaje": "Actualización: Gran amistad consolidada, respeto inquebrantable y gratitud sincera",
    "apodo": "Los Grandes Amigos",
    "leccionAprendida": "El cariño sincero transmuta y evoluciona; no se destruye",
    "impacto": 10,
    "cancion": "Yellow - Coldplay",
    "lugarFavorito": "Parque Caldas, Popayán",
    "cualidades": [
      "Generosidad desinteresada",
      "Lealtad incondicional",
      "Gran compañera de viajes"
    ]
  }
  ```
* **Respuesta Exitosa (200 OK):**
  ```json
  {
    "pareja": {
      "_id": "6516104217031405e3208765",
      "nombre": "Andrés y Camila Gómez",
      "edad": 27,
      "mensaje": "Actualización: Gran amistad consolidada, respeto inquebrantable y gratitud sincera",
      "apodo": "Los Grandes Amigos",
      "fechaInicio": "2021-06-15T00:00:00.000Z",
      "fechaFin": "2023-08-20T00:00:00.000Z",
      "leccionAprendida": "El cariño sincero transmuta y evoluciona; no se destruye",
      "impacto": 10,
      "cancion": "Yellow - Coldplay",
      "lugarFavorito": "Parque Caldas, Popayán",
      "cualidades": [
        "Generosidad desinteresada",
        "Lealtad incondicional",
        "Gran compañera de viajes"
      ],
      "createdAt": "2026-09-30T15:35:00.000Z",
      "updatedAt": "2026-09-30T15:40:00.000Z",
      "__v": 0
    }
  }
  ```
* **Respuestas de Error:**
  * `404 Not Found`: Si no existe el registro especificado.
    ```json
    {
      "message": "The document does not exist"
    }
    ```
  * `500 Internal Server Error`:
    ```json
    {
      "message": "Error while updating <descripción_del_error>"
    }
    ```

---

### 6. Eliminar Pareja (Cerrar Ciclo)

#### `DELETE /api/parejas/delete-pareja/:id`
Suprime permanentemente el registro de la colección `parejas`. Devuelve el documento eliminado como confirmación de ciclo cerrado.

* **URL:** `http://localhost:3000/api/parejas/delete-pareja/:id`
* **Método:** `DELETE`
* **Parámetros de Ruta:**
  * `id` *(obligatorio)*: `_id` de la pareja a remover.
* **Ejemplo de Petición:** `DELETE http://localhost:3000/api/parejas/delete-pareja/6516104217031405e3208765`
* **Respuesta Exitosa (200 OK):**
  ```json
  {
    "pareja": {
      "_id": "6516104217031405e3208765",
      "nombre": "Andrés y Camila Gómez",
      "edad": 27,
      "mensaje": "Actualización: Gran amistad consolidada, respeto inquebrantable y gratitud sincera",
      "apodo": "Los Grandes Amigos",
      "fechaInicio": "2021-06-15T00:00:00.000Z",
      "fechaFin": "2023-08-20T00:00:00.000Z",
      "leccionAprendida": "El cariño sincero transmuta y evoluciona; no se destruye",
      "impacto": 10,
      "cancion": "Yellow - Coldplay",
      "lugarFavorito": "Parque Caldas, Popayán",
      "cualidades": [
        "Generosidad desinteresada",
        "Lealtad incondicional",
        "Gran compañera de viajes"
      ],
      "createdAt": "2026-09-30T15:35:00.000Z",
      "updatedAt": "2026-09-30T15:40:00.000Z",
      "__v": 0
    }
  }
  ```
* **Respuestas de Error:**
  * `404 Not Found`:
    ```json
    {
      "message": "The pareja does not exist"
    }
    ```
  * `500 Internal Server Error`:
    ```json
    {
      "message": "Error while deleting"
    }
    ```

---

## 🧪 Pruebas Rápidas con cURL (Modelo Ampliado)

Comandos listos para terminal que cubren la totalidad de los atributos ampliados:

```bash
# 1. Health check y metadatos del servicio
curl -X GET http://localhost:3000/

# 2. Consultar todo el archivo histórico
curl -X GET http://localhost:3000/api/parejas

# 3. Guardar una nueva historia completa con todos los campos nuevos
curl -X POST http://localhost:3000/api/parejas/save-pareja \
  -H "Content-Type: application/json" \
  -d '{
    "nombre": "Julian y Mariana",
    "edad": 25,
    "mensaje": "Un viaje inolvidable a Santa Marta y risas infinitas",
    "apodo": "Los Soleados",
    "fechaInicio": "2022-01-10T00:00:00.000Z",
    "fechaFin": "2024-03-01T00:00:00.000Z",
    "leccionAprendida": "Agradecer los buenos momentos sin aferrarse al desenlace",
    "impacto": 9,
    "cancion": "Photograph - Ed Sheeran",
    "lugarFavorito": "Playa Cristal, Parque Tayrona",
    "cualidades": ["Espontaneidad", "Bondad", "Gusto por la aventura"]
  }'

# 4. Consultar una pareja por ID (reemplazar <ID_AQUI> por el _id devuelto)
curl -X GET http://localhost:3000/api/parejas/<ID_AQUI>

# 5. Actualizar reflexiones, cualidades y lección aprendida
curl -X PUT http://localhost:3000/api/parejas/edit-pareja/<ID_AQUI> \
  -H "Content-Type: application/json" \
  -d '{
    "nombre": "Julian y Mariana Silva",
    "edad": 26,
    "mensaje": "Paz interior, gratitud recíproca y un gran recuerdo",
    "impacto": 10,
    "leccionAprendida": "Cada persona llega en el momento oportuno para enseñarte algo de ti mismo",
    "cualidades": ["Espontaneidad", "Bondad", "Madurez emocional"]
  }'

# 6. Eliminar el registro (cerrar ciclo definitivamente)
curl -X DELETE http://localhost:3000/api/parejas/delete-pareja/<ID_AQUI>
```

---

## 📄 Licencia y Créditos

Este proyecto se distribuye bajo los términos de la licencia **ISC**, tal como se estipula en el archivo `package.json`.

* **Desarrollador:** [Salomon Montilla](https://github.com/salomontilla)
* **Curso Académico:** Bases de Datos Avanzadas (Semestre 6)
* **Institución:** Corporación Universitaria Autónoma del Cauca
