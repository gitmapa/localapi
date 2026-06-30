# 03. Instalación

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Este documento describe la instalación completa de un entorno LocalAPI para desarrollo local.

Al finalizar el procedimiento deberá existir una infraestructura capaz de:

- integrar múltiples bases PostgreSQL;
- publicar endpoints REST automáticamente;
- generar documentación OpenAPI;
- ofrecer una interfaz Swagger para exploración y pruebas.

---

# Requisitos

## Software

Se requiere:

- PostgreSQL 16 o superior
- PostGIS
- PostgreSQL Foreign Data Wrapper (postgres_fdw)
- PostgREST
- Python 3 (para servir Swagger UI)
- Git

---

# Bases de datos

Para la implementación actual se utilizan las siguientes bases.

| Base | Función |
|-------|----------|
| ranie_app | Base funcional de referencia |
| ranie_mapa | Base SIG y laboratorio |
| padron_nacion | Fuente nacional |
| ranie_dev | Base integradora LocalAPI |

Las tres primeras actúan como fuentes.

Toda la integración ocurre dentro de `ranie_dev`.

---

# Crear la base integradora

```sql
CREATE DATABASE ranie_dev;
```

---

# Instalar extensiones

Conectarse a `ranie_dev`.

Ejecutar:

```sql
CREATE EXTENSION postgis;

CREATE EXTENSION postgres_fdw;
```

---

# Crear los schemas

```sql
CREATE SCHEMA api;

CREATE SCHEMA src_ranie_app;

CREATE SCHEMA src_ranie_mapa;

CREATE SCHEMA src_padron_nacion;
```

---

# Configurar servidores FDW

Registrar cada base remota mediante PostgreSQL Foreign Data Wrapper.

Ejemplo:

```sql
CREATE SERVER srv_ranie_app
FOREIGN DATA WRAPPER postgres_fdw
OPTIONS (
    host 'localhost',
    port '5432',
    dbname 'ranie_app'
);
```

Repetir el procedimiento para todas las bases que deban integrarse.

---

# Crear User Mapping

Cada servidor FDW requiere un usuario con permisos de lectura.

Ejemplo:

```sql
CREATE USER MAPPING
FOR CURRENT_USER
SERVER srv_ranie_app
OPTIONS (
    user 'postgres',
    password '******'
);
```

---

# Importar tablas

Las tablas remotas se incorporan utilizando:

```sql
IMPORT FOREIGN SCHEMA
...
```

Se recomienda importar únicamente las tablas necesarias para el proyecto.

No importar esquemas completos sin justificación.

---

# Construir las vistas

Toda la lógica de integración debe implementarse mediante vistas SQL.

Las vistas públicas deben crearse exclusivamente dentro del schema:

```
api
```

Nunca publicar tablas directamente.

---

# Configurar permisos

Crear los roles necesarios.

Asignar permisos sobre:

- schema `api`
- vistas públicas

La configuración detallada se describe en:

```
docs/06_seguridad.md
```

---

# Instalar PostgREST

Crear una carpeta de trabajo.

Ejemplo:

```
C:\postgrest
```

Copiar allí:

```
postgrest.exe

ranie_dev.conf

swagger-ui\
```

No es necesario que estos archivos formen parte del repositorio Git.

---

# Verificar la instalación

La instalación estará completa cuando puedan verificarse las siguientes condiciones.

## Base integradora

Existe la base:

```
ranie_dev
```

---

## Schemas

Existen:

- api
- src_ranie_app
- src_ranie_mapa
- src_padron_nacion

---

## Vistas

Existen las vistas públicas necesarias.

Ejemplo:

- api.v_cui
- api.v_cueanexos

---

## Roles

Existen:

- api_anon
- api_authenticator

---

## PostgREST

Responde correctamente:

```
http://127.0.0.1:3000/
```

---

## Swagger

Se encuentra disponible en:

```
http://127.0.0.1:8080
```

---

# Organización recomendada

```
PostgreSQL

    ranie_app
    ranie_mapa
    padron_nacion
    ranie_dev



Repositorio

    localapi/

        README.md

        docs/

        sql/




Herramientas

    C:\postgrest

        postgrest.exe

        ranie_dev.conf

        swagger-ui\
```

---

# Resultado esperado

Al finalizar la instalación, LocalAPI debe encontrarse en condiciones de integrar nuevas fuentes de datos y publicar automáticamente nuevos endpoints REST sin desarrollar software adicional.