# Inventario de Equipos Médicos

Aplicación web para gestionar un inventario de equipos médicos. Permite consultar, filtrar, registrar, actualizar y eliminar equipos, relacionándolos con ubicaciones almacenadas en la base de datos.

## Tecnologías

### Backend
- Node.js
- Express
- MySQL
- mysql2
- dotenv
- csv-parse
- CORS

### Frontend
- React
- Vite
- JavaScript
- CSS

### Base de datos
- MySQL

## Estructura del proyecto

```text
├── Backend/
│   ├── config/
│   ├── controllers/
│   ├── middlewares/
│   ├── models/
│   ├── routes/
│   ├── utils/
│   ├── data/
│   │   └── medical_equipment.csv
│   ├── app.js
│   ├── database.js
│   ├── seed.js
│   ├── server.js
│   └── package.json
│
├── Frontend/
│   ├── src/
│   ├── public/
│   ├── index.html
│   └── package.json
│
└── README.md
```

## Requisitos

Antes de ejecutar el proyecto se necesita tener instalado:

- Node.js
- npm
- MySQL

## Configuración de la base de datos

Crear una base de datos MySQL llamada:

```sql
CREATE DATABASE inventario_equipos_medicos;
```

El proyecto utiliza dos tablas principales:

- `ubicaciones`: almacena las ubicaciones disponibles.
- `equipos`: almacena los equipos médicos y su ubicación mediante una llave foránea.

## Configuración del Backend

Entrar a la carpeta:

```bash
cd Backend
```

Instalar las dependencias:

```bash
npm install
```

Crear un archivo `.env` dentro de `Backend`:

```env
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=
DB_NAME=inventario_equipos_medicos
```

La contraseña debe ajustarse según la configuración local de MySQL.

## Carga inicial de datos

El proyecto incluye un archivo CSV con los equipos médicos:

```text
Backend/data/medical_equipment.csv
```

Para cargar las ubicaciones y los equipos en MySQL:

```bash
npm run seed
```

El proceso valida los datos del CSV, relaciona cada equipo con una ubicación existente y carga los registros en la base de datos.

## Ejecutar el Backend

Desde la carpeta `Backend`:

```bash
npm start
```

La API estará disponible en:

```text
http://localhost:3000
```

También se puede ejecutar en modo desarrollo:

```bash
npm run dev
```

## Ejecutar el Frontend

Abrir otra terminal y entrar a:

```bash
cd Frontend
```

Instalar las dependencias:

```bash
npm install
```

Ejecutar la aplicación:

```bash
npm run dev
```

El frontend estará disponible normalmente en:

```text
http://localhost:5173
```

## API REST

### Obtener ubicaciones

```http
GET /ubicaciones
```

Devuelve las ubicaciones disponibles para relacionarlas con los equipos.

### Obtener equipos

```http
GET /equipos
```

También permite aplicar filtros combinados.

Por tipo de equipo:

```http
GET /equipos?tipo_equipo=Vital%20Signs%20Monitor
```

Por búsqueda de texto:

```http
GET /equipos?query=GE
```

La búsqueda de texto se realiza sobre:

- nombre
- marca
- modelo
- número de serie
- código de inventario

Los filtros `tipo_equipo` y `query` pueden utilizarse al mismo tiempo.

### Obtener un equipo

```http
GET /equipos/:id
```

### Registrar un equipo

```http
POST /equipos
```

### Actualizar un equipo

```http
PUT /equipos/:id
```

### Eliminar un equipo

```http
DELETE /equipos/:id
```

## Funcionamiento

El frontend consume la API REST del backend mediante solicitudes HTTP.

La información se almacena en MySQL. Cada equipo contiene una referencia `ubicacion_id` hacia la tabla `ubicaciones`, evitando guardar la ubicación como texto libre.

El frontend permite:

- Consultar los equipos.
- Filtrar por tipo.
- Buscar por texto.
- Combinar filtros.
- Limpiar filtros.
- Visualizar los resultados en una tabla.
- Eliminar equipos.

## Validaciones y manejo de errores

El backend valida los datos recibidos antes de realizar operaciones sobre la base de datos.

También controla errores como:

- Equipos inexistentes.
- IDs inválidos.
- Ubicaciones inexistentes.
- Datos duplicados.
- Rutas no encontradas.
- Errores de integridad referencial.
- Errores inesperados del servidor.

Las respuestas de error se entregan en formato JSON.

## Scripts disponibles

### Backend

```bash
npm start
```

Inicia el servidor.

```bash
npm run dev
```

Inicia el servidor en modo desarrollo.

```bash
npm run seed
```

Carga los datos iniciales desde el CSV.

### Frontend

```bash
npm run dev
```

Inicia el servidor de desarrollo de React.

```bash
npm run build
```

Genera la versión de producción.

```bash
npm run lint
```

Verifica el código con ESLint.

## Flujo de ejecución

```text
CSV
 │
 ▼
Seed
 │
 ▼
MySQL
 │
 ▼
API REST - Express
 │
 ▼
Frontend - React
 │
 ▼
Usuario
```

## Autor

Proyecto desarrollado como prueba técnica para la gestión de un inventario de equipos médicos.
