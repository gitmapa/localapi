# LocalAPI

> Laboratorio de integración y publicación de productos de información.

## ¿Qué es?

LocalAPI integra múltiples bases PostgreSQL, construye un modelo de información único y lo publica mediante PostgREST.

## Método

Necesidad
↓
Producto
↓
Modelo lógico
↓
Diccionario de datos
↓
Vista SQL
↓
Endpoint
↓
Viewer
↓
Validación contra publicación oficial

## Principios

- El producto precede al SQL.
- El modelo precede a la API.
- No se duplican responsabilidades.
- Cada atributo posee una única fuente de verdad.
- El Excel oficial valida el resultado, no define el modelo.
