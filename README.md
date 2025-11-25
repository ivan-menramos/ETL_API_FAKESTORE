# Proyecto ETL: Integración de datos desde FakeStoreAPI hacia PostgreSQL

Desarrollé un pipeline ETL completo utilizando Python para extraer información de productos, 
usuarios y ventas desde la API pública FakeStoreAPI. 
Implementé un módulo de extracción con requests para recuperar 
los datos en formato JSON, seguido de un proceso de transformación 
donde estructuré, normalicé y limpié la información más relevante (
datos de productos, direcciones de usuarios y ventas generadas a partir de los carritos de compra).
Finalmente, construí un módulo de carga empleando SQLAlchemy para insertar los datos procesados en un modelo de Data Warehouse dentro de PostgreSQL,
utilizando tablas de dimensiones y una tabla de hechos. Las credenciales y la configuración de conexión se gestionan mediante variables de entorno (.env).
El proceso permite integrar los tres conjuntos de datos, generar DataFrames consistentes y almacenarlos en una base de datos de forma segura, flexible y escalable.

# Tecnologías
Python, Pandas, Requests, SQLAlchemy, PostgreSQL, dotenv

## Conceptos aplicados
ETL, APIs REST, JSON parsing, data cleaning, carga en base de datos, manejo de excepciones, diseño modular de pipelines.

---

## 1.Extracción (Extract)

El módulo de extracción obtiene la información desde tres endpoints de FakeStoreAPI:

- Products : productos del catálogo
- Users : usuarios registrados
- Carts : carritos que representan ventas
Cada función:
Realiza una solicitud HTTP con requests, valida el código de respuesta, devuelve los datos brutos en formato JSON como listas de diccionarios, esto permite desacoplar la extracción del resto del pipeline y reutilizarla en futuros procesos.

---
## 2. Transformación (Transform)

El módulo de transformación procesa cada conjunto de datos de manera independiente:

Transformación de productos
- Selecciona campos relevantes (id, nombre, precio, categoría).
- Construye un DataFrame limpio y estructurado.
- Reemplaza valores faltantes: media para columnas numéricas, 0 para columnas de texto

Transformación de usuarios
- Normaliza campos anidados (ciudad, código postal).
- Construye un DataFrame estructurado con identificador, username, email y dirección.
- Aplica reglas de limpieza y completado de valores.

Transformación de ventas (carts)
- Convierte cada carrito en varias filas de ventas individuales.
- Extrae productId, userId, quantity y fecha.
- Devuelve un DataFrame listo para nutrir la tabla de hechos.

Todo el proceso garantiza consistencia entre las dimensiones y la tabla fact.

---

## 3. Carga en PostgreSQL (Load)
 
El módulo de carga utiliza SQLAlchemy para:
- Conectarse al motor de PostgreSQL mediante un engine.
- Insertar los datos procesados en tres tablas: dim_productos2, dim_usuarios2, fact_ventas2
- Inserción fila por fila para asegurar control y manejo de excepciones.
- Lectura de credenciales desde .env.
- Este enfoque permite mantener las tablas actualizadas incluso si la API regresa nueva información.


