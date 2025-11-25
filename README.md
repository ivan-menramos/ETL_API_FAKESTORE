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
