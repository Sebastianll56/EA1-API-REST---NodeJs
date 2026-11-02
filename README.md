# Proyecto Integrado II – API REST de Películas y Series

API REST desarrollada con **Node.js**, **Express** y **SQL Server** para administrar la información de un catálogo de películas y series. El proyecto organiza sus funcionalidades en cinco módulos y permite realizar operaciones CRUD (crear, consultar, actualizar y eliminar) mediante solicitudes HTTP.

## Información académica

- **Institución:** IU Digital de Antioquia
- **Programa:** Ingeniería en Software y Datos
- **Curso:** Proyecto Integrado II – Desarrollo de Aplicaciones Web
- **Estudiante:** Sebastián Londoño Londoño
- **Docente:** Federico Henao Villa

## Tecnologías utilizadas

- Node.js
- Express
- JavaScript
- Microsoft SQL Server
- `mssql` y `msnodesqlv8` para la conexión con SQL Server
- `cors` para habilitar solicitudes desde otros orígenes
- Postman para las pruebas de los servicios REST

> La conexión se configuró para trabajar con SQL Server local y el controlador ODBC Driver 18 for SQL Server. El nombre del servidor o instancia puede variar según el equipo donde se ejecute el proyecto.

## Módulos de la API

| Módulo | Descripción | Endpoint base |
|---|---|---|
| Género | Administra los géneros cinematográficos. | `/api/generos` |
| Director | Administra la información de los directores. | `/api/directores` |
| Productora | Administra las productoras. | `/api/productoras` |
| Tipo | Administra los tipos de contenido, por ejemplo, Película y Serie. | `/api/tipos` |
| Media | Administra películas y series y sus relaciones con Género, Director, Productora y Tipo. | `/api/media` |

## Operaciones disponibles

Cada módulo implementa las siguientes rutas:

| Método HTTP | Ruta | Función |
|---|---|---|
| `GET` | `/api/{modulo}` | Consulta todos los registros del módulo. |
| `GET` | `/api/{modulo}/:id` | Consulta un registro por su identificador. |
| `POST` | `/api/{modulo}` | Registra un nuevo registro. |
| `PUT` | `/api/{modulo}/:id` | Actualiza un registro existente. |
| `DELETE` | `/api/{modulo}/:id` | Elimina un registro. |

Sustituya `{modulo}` por `generos`, `directores`, `productoras`, `tipos` o `media`, según corresponda.

## Requisitos previos

1. Node.js y npm instalados.
2. Microsoft SQL Server instalado y en ejecución.
3. La base de datos `ProyectoIntegrado2_Peliculas` creada y con las tablas requeridas.
4. ODBC Driver 18 for SQL Server instalado.
5. Postman (opcional, para ejecutar las pruebas de los endpoints).

## Instalación y ejecución

### 1. Clonar el repositorio

```bash
git clone <URL_DEL_REPOSITORIO>
cd ProyectoIntegrado2_API
```

### 2. Instalar dependencias

```bash
npm install
```

El comando instala las dependencias declaradas en `package.json`.

### 3. Configurar la conexión a SQL Server

Abra el archivo:

```text
src/config/database.js
```

Revise y ajuste la configuración de conexión para el equipo local:

- Nombre del servidor o instancia de SQL Server.
- Nombre de la base de datos: `ProyectoIntegrado2_Peliculas`.
- Controlador ODBC: `ODBC Driver 18 for SQL Server`.
- Método de autenticación y opciones de conexión utilizadas en el entorno.

No publique contraseñas, cadenas de conexión privadas ni otros datos sensibles en GitHub. Si adapta el proyecto para usar variables de entorno, incluya un archivo de ejemplo sin credenciales reales y mantenga el archivo `.env` fuera del repositorio.

### 4. Iniciar la API

Desde la carpeta raíz del proyecto, ejecute:

```bash
node server.js
```

Cuando la conexión y el inicio sean correctos, el servidor informa que la API está en ejecución y muestra las rutas disponibles.

La API utiliza el puerto **3001** de forma predeterminada:

```text
http://localhost:3001
```

Mantenga abierta la terminal mientras realiza las solicitudes. Para detener el servidor, presione `Ctrl + C`.

## Rutas principales

| Recurso | URL local |
|---|---|
| Inicio | `http://localhost:3001/` |
| Estado de la API | `http://localhost:3001/api/estado` |
| Géneros | `http://localhost:3001/api/generos` |
| Directores | `http://localhost:3001/api/directores` |
| Productoras | `http://localhost:3001/api/productoras` |
| Tipos | `http://localhost:3001/api/tipos` |
| Películas y series | `http://localhost:3001/api/media` |

## Ejemplos de solicitudes en Postman

En las solicitudes `POST` y `PUT`, seleccione **Body → raw → JSON**. En las solicitudes `GET` y `DELETE`, no se requiere cuerpo.

### Registrar un género – POST

**URL:** `http://localhost:3001/api/generos`

```json
{
  "nombre": "Animación",
  "estado": true,
  "descripcion": "Producciones de animación."
}
```

### Registrar un director – POST

**URL:** `http://localhost:3001/api/directores`

```json
{
  "nombres": "Nombre del director",
  "estado": true
}
```

### Registrar una productora – POST

**URL:** `http://localhost:3001/api/productoras`

```json
{
  "nombre": "Productora de ejemplo",
  "estado": true,
  "slogan": "Historias que inspiran",
  "descripcion": "Descripción de la productora."
}
```

### Registrar un tipo – POST

**URL:** `http://localhost:3001/api/tipos`

```json
{
  "nombre": "Tipo de prueba",
  "descripcion": "Descripción del tipo de contenido."
}
```

### Registrar una película o serie – POST

**URL:** `http://localhost:3001/api/media`

```json
{
  "serial": "MEDIA-EJEMPLO-001",
  "titulo": "Título de ejemplo",
  "sinopsis": "Sinopsis de la película o serie.",
  "url": "https://ejemplo.com/contenido",
  "imagenPortada": null,
  "anioEstreno": 2024,
  "idGenero": 1,
  "idDirector": 1,
  "idProductora": 1,
  "idTipo": 1
}
```

**Importante:** los identificadores de las relaciones (`idGenero`, `idDirector`, `idProductora` e `idTipo`) deben existir previamente en la base de datos. Los valores `1` del ejemplo son ilustrativos; consulte los IDs reales antes de registrar el contenido.

## Estructura del proyecto

```text
ProyectoIntegrado2_API/
├── src/
│   ├── config/
│   │   └── database.js
│   ├── controllers/
│   │   ├── genero.controller.js
│   │   ├── director.controller.js
│   │   ├── productora.controller.js
│   │   ├── tipo.controller.js
│   │   └── media.controller.js
│   └── routes/
│       ├── genero.routes.js
│       ├── director.routes.js
│       ├── productora.routes.js
│       ├── tipo.routes.js
│       └── media.routes.js
├── server.js
├── package.json
└── package-lock.json
```

## Modelo de relaciones

La tabla `Media` contiene las llaves foráneas que la relacionan con las otras cuatro tablas:

- `Media.IdGenero` → `Genero.IdGenero`
- `Media.IdDirector` → `Director.IdDirector`
- `Media.IdProductora` → `Productora.IdProductora`
- `Media.IdTipo` → `Tipo.IdTipo`

Al consultar películas y series, el módulo Media utiliza estas relaciones para devolver también los nombres del género, director, productora y tipo asociados.

## Pruebas realizadas

Las operaciones CRUD de los cinco módulos se probaron en Postman. Entre los resultados observados se encuentran:

- `200 OK` para consultas y actualizaciones exitosas.
- `201 Created` para registros exitosos.
- `404 Not Found` al consultar un registro después de eliminarlo.
- `200 OK` en las eliminaciones confirmadas por la API.

En la revisión final de la base de datos se obtuvo el siguiente conteo:

| Tabla | Registros observados |
|---|---:|
| Género | 5 |
| Director | 1 |
| Productora | 1 |
| Tipo | 2 |
| Media | 0 |

La consulta de relaciones inválidas devolvió `0`. Esta consulta se ejecutó cuando la tabla Media no tenía registros; por tanto, el resultado confirma que no había filas de Media con referencias inválidas en ese momento. Durante las pruebas CRUD también se registró y consultó una película de prueba, y la respuesta incluyó correctamente los nombres de sus cuatro entidades relacionadas. El registro temporal de Media fue eliminado y su consulta posterior devolvió `404 Not Found`.

## Respuestas HTTP utilizadas

| Código | Significado en las pruebas |
|---|---|
| `200 OK` | Consulta, actualización o eliminación completada correctamente. |
| `201 Created` | Registro creado correctamente. |
| `400 Bad Request` | Datos enviados no válidos o incompletos. |
| `404 Not Found` | Ruta o registro solicitado no encontrado. |
| `409 Conflict` | Conflicto con una relación o valor duplicado, cuando aplica. |
| `500 Internal Server Error` | Error interno durante el procesamiento de la solicitud. |

## Consideraciones

- La API se ejecuta localmente; para utilizarla desde otro equipo se requiere configurar la red y el entorno de ejecución.
- La base de datos debe existir antes de iniciar la API.
- Los IDs utilizados en los ejemplos deben reemplazarse por identificadores existentes en la base de datos de destino.
- El repositorio documenta el Backend API REST desarrollado y probado. No se debe asumir que incluye un Frontend o un despliegue en producción.

## Autor

**Sebastián Londoño Londoño**  
Ingeniería en Software y Datos  
IU Digital de Antioquia  
Proyecto Integrado II – Desarrollo de Aplicaciones Web  
Docente: Federico Henao Villa
