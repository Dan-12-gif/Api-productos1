# Api-productos1

Una API REST desarrollada con **FastAPI** para gestionar un catálogo de productos. Permite realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre productos con almacenamiento en base de datos SQLite.

## Requisitos Previos

- **Python 3.8+** instalado en tu sistema
- **pip** (gestor de paquetes de Python)
- **Git** (opcional, para clonar el repositorio)

## Instalación

### 1. Clona o descarga el proyecto

```bash
git clone <URL-del-repositorio>
cd api-productos
```

### 2. Crea un entorno virtual

**En Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**En macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Instala las dependencias

```bash
pip install -r requirements.txt
```

Si no existe `requirements.txt`, instala manualmente:

```bash
pip install fastapi uvicorn sqlalchemy
```

## Estructura del Proyecto

```
api-productos/
├── productos/
│   ├── main.py          # Punto de entrada de la API
│   ├── database.py      # Configuración de la base de datos
│   ├── models.py        # Modelos SQLAlchemy (Producto)
│   ├── dtos.py          # Data Transfer Objects (esquemas)
│   ├── crud.py          # Operaciones de base de datos
│   └── __init__.py      # Archivo de inicialización
├── sql_app.db           # Base de datos SQLite (se crea automáticamente)
└── README.md            # Este archivo
```

## Ejecución

### Inicia el servidor

```bash
uvicorn productos.main:app --reload
```

El servidor estará disponible en: **http://localhost:8000**

### Interfaz interactiva (Swagger UI)

Abre tu navegador en: **http://localhost:8000/docs**

Aquí podrás probar todos los endpoints de forma interactiva.

## Endpoints Disponibles

### 1. Listar todos los productos

```http
GET /productos
```

**Respuesta:**
```json
[
  {
    "id": 1,
    "nombre": "Laptop",
    "precio": 1200.50
  }
]
```

---

### 2. Obtener un producto por ID

```http
GET /productos/{producto_id}
```

**Ejemplo:**
```http
GET /productos/1
```

**Respuesta:**
```json
{
  "id": 1,
  "nombre": "Laptop",
  "precio": 1200.50
}
```

---

### 3. Crear un nuevo producto

```http
POST /productos
```

**Body (JSON):**
```json
{
  "nombre": "Mouse inalámbrico",
  "precio": 25.99
}
```

**Respuesta:**
```json
{
  "id": 2,
  "nombre": "Mouse inalámbrico",
  "precio": 25.99
}
```

---

### 4. Actualizar un producto

```http
PUT /productos/{producto_id}
```

**Ejemplo:**
```http
PUT /productos/1
```

**Body (JSON):**
```json
{
  "nombre": "Laptop Gaming",
  "precio": 1500.00
}
```

**Respuesta:**
```json
{
  "id": 1,
  "nombre": "Laptop Gaming",
  "precio": 1500.00
}
```

---

### 5. Eliminar un producto

```http
DELETE /productos/{producto_id}
```

**Ejemplo:**
```http
DELETE /productos/1
```

**Respuesta:**
```json
{
  "id": 1,
  "nombre": "Laptop Gaming",
  "precio": 1500.00
}
```

## Códigos de estado HTTP

| Código | Descripción |
|--------|-------------|
| `200` | Operación exitosa |
| `201` | Recurso creado exitosamente |
| `404` | Producto no encontrado |
| `422` | Datos inválidos en la solicitud |
| `500` | Error interno del servidor |

## Ejemplo con cURL

```bash
# Crear un producto
curl -X POST "http://localhost:8000/productos" \
  -H "Content-Type: application/json" \
  -d '{"nombre": "Teclado", "precio": 75.50}'

# Listar todos los productos
curl "http://localhost:8000/productos"

# Obtener un producto específico
curl "http://localhost:8000/productos/1"

# Actualizar un producto
curl -X PUT "http://localhost:8000/productos/1" \
  -H "Content-Type: application/json" \
  -d '{"nombre": "Teclado Mecánico", "precio": 85.50}'

# Eliminar un producto
curl -X DELETE "http://localhost:8000/productos/1"
```

## Base de Datos

- **Tipo:** SQLite
- **Archivo:** `sql_app.db` (se crea automáticamente en `productos/`)
- **Tabla:** `productos`

La base de datos se inicializa automáticamente al ejecutar la aplicación por primera vez.

## Solución de Problemas

### Error: `ModuleNotFoundError: No module named 'fastapi'`

Asegúrate de haber activado el entorno virtual e instalado las dependencias:

```bash
venv\Scripts\activate  # Windows
pip install fastapi uvicorn sqlalchemy
```

### Error: `Could not import module "main"`

Ejecuta el servidor desde la carpeta raíz del proyecto:

```bash
cd api-productos
uvicorn productos.main:app --reload
```

### El navegador no abre `localhost:8000`

Verifica que:
1. El servidor esté corriendo (deberías ver "Uvicorn running on http://127.0.0.1:8000")
2. El puerto 8000 no esté ocupado por otro programa

## Tecnologías Utilizadas

- **FastAPI** - Framework web moderno y rápido
- **Uvicorn** - Servidor ASGI
- **SQLAlchemy** - ORM para base de datos
- **Pydantic** - Validación de datos
- **SQLite** - Base de datos

## Próximos Pasos

Puedes extender esta API agregando:
- Autenticación y autorización (JWT)
- Categorías de productos
- Sistema de inventario
- Búsqueda y filtrado avanzado
- Tests unitarios

## Autor

Desarrollado con ❤️ usando FastAPI

## Licencia

Este proyecto está disponible bajo la licencia MIT.
