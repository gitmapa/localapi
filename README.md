# RANIE DEV API

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-blue?logo=postgresql)
![PostGIS](https://img.shields.io/badge/PostGIS-enabled-green)
![PostgREST](https://img.shields.io/badge/PostgREST-running-5C2D91)
![Swagger](https://img.shields.io/badge/Swagger-UI-85EA2D?logo=swagger)
![Status](https://img.shields.io/badge/status-local%20development-orange)

## Objetivo

Este repositorio documenta un entorno de desarrollo local para integración y publicación de datos institucionales mediante PostgreSQL + PostGIS + PostgREST.

El objetivo inicial es:

* integrar información de distintas bases institucionales;
* construir vistas SQL limpias y controladas;
* exponer endpoints REST automáticamente;
* generar documentación OpenAPI/Swagger;
* experimentar arquitectura antes de solicitar despliegues productivos al área de Sistemas.

---

# Arquitectura

```text
Bases fuente
│
├── ranie_app
├── ranie_mapa
└── padron_nacion
        │
        ▼
postgres_fdw
        │
        ▼
ranie_dev
│
├── src_ranie_app
├── src_ranie_mapa
├── src_padron_nacion
└── api
        │
        ▼
PostgREST
        │
        ▼
Swagger UI
```

---

# Bases involucradas

| Base            | Función                                   |
| --------------- | ----------------------------------------- |
| `ranie_app`     | referencia funcional similar a productivo |
| `ranie_mapa`    | laboratorio SIG y testing                 |
| `padron_nacion` | fuente nacional institucional             |
| `ranie_dev`     | integración, vistas API y pruebas         |

---

# Tecnologías

| Tecnología    | Uso                             |
| ------------- | ------------------------------- |
| PostgreSQL 16 | motor de base de datos          |
| PostGIS       | geometrías                      |
| postgres_fdw  | integración entre bases         |
| PostgREST     | publicación automática REST     |
| Swagger UI    | exploración y documentación API |

---

# Objetivo funcional inicial

Se exponen dos listados mínimos:

## `/v_cui`

Información de edificios.

Campos:

* `cui`
* `lat`
* `lng`
* `latwgs84`
* `lonwgs84`
* `geom`
* `comuna`
* `barrio`
* `de`

## `/v_cueanexos`

Información de establecimientos/localizaciones.

Campos:

* `cui`
* `cue`
* `anexo`
* `nombre`
* `direccion`

---

# Instalación

## 1. Crear base

```sql
create database ranie_dev;
```

---

## 2. Instalar extensiones

```sql
create extension postgis;
create extension postgres_fdw;
```

---

## 3. Crear schemas

```sql
create schema api;

create schema src_ranie_app;
create schema src_ranie_mapa;
create schema src_padron_nacion;
```

---

# Configuración FDW

## Servidores remotos

```sql
create server srv_ranie_app
foreign data wrapper postgres_fdw
options (
    host 'localhost',
    port '5432',
    dbname 'ranie_app'
);

create server srv_ranie_mapa
foreign data wrapper postgres_fdw
options (
    host 'localhost',
    port '5432',
    dbname 'ranie_mapa'
);
```

---

## User mappings

```sql
create user mapping for current_user
server srv_ranie_app
options (
    user 'postgres',
    password 'PASSWORD'
);

create user mapping for current_user
server srv_ranie_mapa
options (
    user 'postgres',
    password 'PASSWORD'
);
```

---

# Importación de tablas remotas

## RANIE APP

```sql
import foreign schema ranie
limit to (
    edificios,
    edificios_direcciones,
    direcciones,
    ubicacion_administrativa
)
from server srv_ranie_app
into src_ranie_app;
```

## RANIE MAPA

```sql
import foreign schema padrones
limit to (
    padron_ueicee
)
from server srv_ranie_mapa
into src_ranie_mapa;
```

---

# Vistas API

## `api.v_cui`

```sql
create or replace view api.v_cui as
select
    e.cui,
    e.y_gkba as lat,
    e.x_gkba as lng,
    e.y_wgs84 as latwgs84,
    e.x_wgs84 as lonwgs84,
    e.geom,
    ua.comuna,
    ua.barrio,
    ua.distrito_escolar as de
from src_ranie_app.edificios e
left join src_ranie_app.edificios_direcciones ed
    on ed.edificio_id = e.id
   and ed.es_principal = true
left join src_ranie_app.direcciones d
    on d.id = ed.direccion_id
left join src_ranie_app.ubicacion_administrativa ua
    on ua.id = d.ubicacion_administrativa_id
where e.borrado = false;
```

---

## `api.v_cueanexos`

```sql
create or replace view api.v_cueanexos as
select
    pu.cui,
    pu.cue,
    pu.anexo,
    pu.nombre_est as nombre,
    concat_ws(' ', pu.calle, pu.num) as direccion
from src_ranie_mapa.padron_ueicee pu
where pu.cui is not null;
```

---

# Seguridad

## Roles

```sql
create role api_anon nologin;

create role api_authenticator
noinherit
login
password 'PASSWORD';

grant api_anon to api_authenticator;
```

---

## Permisos

```sql
grant usage on schema api to api_anon;

grant select on api.v_cui to api_anon;
grant select on api.v_cueanexos to api_anon;
```

---

# PostgREST

## Archivo `ranie_dev.conf`

```ini
db-uri = "postgres://api_authenticator:PASSWORD@localhost:5432/ranie_dev"

db-schemas = "api"

db-anon-role = "api_anon"

server-host = "127.0.0.1"

server-port = 3000

server-cors-allowed-origins = "*"

openapi-server-proxy-uri = "http://127.0.0.1:3000"
```

---

## Ejecutar

```powershell
.\postgrest.exe .\ranie_dev.conf
```

---

# Swagger UI

## `index.html`

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>RANIE API - Swagger UI</title>
  <link rel="stylesheet" href="https://unpkg.com/swagger-ui-dist/swagger-ui.css">
</head>
<body>
  <div id="swagger-ui"></div>

  <script src="https://unpkg.com/swagger-ui-dist/swagger-ui-bundle.js"></script>

  <script>
    SwaggerUIBundle({
      url: "http://127.0.0.1:3000/",
      dom_id: "#swagger-ui"
    });
  </script>
</body>
</html>
```

---

## Ejecutar servidor local

```powershell
python -m http.server 8080
```

---

# URLs de prueba

## OpenAPI

```text
http://127.0.0.1:3000/
```

## Swagger UI

```text
http://127.0.0.1:8080
```

## Endpoints

```text
http://127.0.0.1:3000/v_cui?limit=5
```

```text
http://127.0.0.1:3000/v_cueanexos?limit=5
```

---

# Ejemplos de filtros

## Buscar CUI

```text
/v_cui?cui=eq.200187
```

## Buscar establecimientos por CUI

```text
/v_cueanexos?cui=eq.200187
```

## Seleccionar columnas

```text
/v_cui?select=cui,latwgs84,lonwgs84,comuna,barrio
```

---

# Próximos pasos

* JWT y autenticación
* perfiles de acceso
* materialized views
* endpoints internos vs públicos
* joins con padrón nacional
* reverse proxy con Nginx
* despliegue Linux
* Docker Compose
* versionado OpenAPI
* métricas y logging

---

# Estado actual

✅ FDW funcionando
✅ PostGIS funcionando
✅ Vistas API funcionando
✅ PostgREST funcionando
✅ Swagger UI funcionando
✅ OpenAPI generado automáticamente
