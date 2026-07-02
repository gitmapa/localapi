# LocalAPI

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-blue?logo=postgresql)
![PostGIS](https://img.shields.io/badge/PostGIS-enabled-green)
![PostgREST](https://img.shields.io/badge/PostgREST-REST%20API-5C2D91)
![Swagger](https://img.shields.io/badge/Swagger-OpenAPI-85EA2D?logo=swagger)
![FDW](https://img.shields.io/badge/postgres__fdw-enabled-blueviolet)
![Status](https://img.shields.io/badge/status-MVP-orange)

---

# ¿Qué es LocalAPI?

LocalAPI es un laboratorio para integrar, modelar y publicar información proveniente de múltiples bases de datos PostgreSQL.

Su objetivo es construir rápidamente APIs funcionales que permitan validar requerimientos, demostrar su utilidad mediante un MVP y reducir la incertidumbre técnica antes de una implementación institucional.

El proyecto no desarrolla aplicaciones.

Desarrolla **modelos de información** que posteriormente pueden ser consumidos desde aplicaciones web, sistemas institucionales, herramientas SIG o cualquier cliente compatible con HTTP.

---

# Arquitectura

```
                 Bases institucionales

      ranie_app     ranie_mapa     padron_nacion
            │             │               │
            └─────────────┴───────────────┘
                          │
                 PostgreSQL FDW
                          │
                          ▼
                    ranie_dev
          (base integradora LocalAPI)
                          │
          ┌───────────────┴───────────────┐
          │                               │
     schemas src_*                   schema api
 (tablas remotas FDW)            (vistas públicas)
          │                               │
          └───────────────┬───────────────┘
                          │
                     PostgREST
                          │
                 OpenAPI automático
                          │
                     Swagger UI
                          │
                 Aplicaciones cliente
```

---

# Estructura del repositorio

```
localapi/

│
├── README.md
│
├── docs/
│   ├── 01_introduccion.md
│   ├── 02_arquitectura.md
│   ├── 03_instalacion.md
│   ├── 04_postgrest.md
│   ├── 05_swagger.md
│   ├── 06_seguridad.md
│   ├── 07_endpoints.md
│   ├── 08_desarrollo.md
│   └── 09_roadmap.md
│
├── sql/
│
└── restore.md
```

---

# Instalación rápida

La infraestructura utilizada por el proyecto está compuesta por:

- PostgreSQL
- PostGIS
- PostgreSQL Foreign Data Wrapper (FDW)
- PostgREST
- Swagger UI
- Python (servidor HTTP local)

La guía completa de instalación se encuentra en:

```
docs/03_instalacion.md
```

---

# Levantar el laboratorio

## 1. Verificar PostgreSQL

Confirmar que PostgreSQL se encuentre iniciado y que exista la base:

```
ranie_dev
```

---

## 2. Iniciar PostgREST

Abrir una ventana de **Símbolo del sistema (CMD)**.

Ir a:

```cmd
cd C:\postgrest
```

Ejecutar:

```cmd
postgrest.exe ranie_dev.conf
```

No cerrar la ventana.

---

## 3. Verificar la API

Abrir el navegador.

```
http://127.0.0.1:3000/
```

Debe visualizarse el documento OpenAPI generado automáticamente.

También puede verificarse un recurso, por ejemplo:

```
http://127.0.0.1:3000/v_cui?limit=5
```

---

## 4. Iniciar Swagger UI

Abrir una segunda ventana de **CMD**.

Ir a:

```cmd
cd C:\postgrest\swagger-ui
```

Ejecutar:

```cmd
python -m http.server 8080
```

---

## 5. Abrir Swagger

```
http://127.0.0.1:8080
```

Swagger detectará automáticamente todos los endpoints publicados por PostgREST.

---

# Documentación

| Documento | Contenido |
|-----------|-----------|
| `01_introduccion.md` | Objetivos y alcance del proyecto |
| `02_arquitectura.md` | Arquitectura general de LocalAPI |
| `03_instalacion.md` | Instalación completa del entorno |
| `04_postgrest.md` | Publicación automática de APIs |
| `05_swagger.md` | Exploración y validación mediante Swagger UI |
| `06_seguridad.md` | Modelo de seguridad y publicación |
| `07_endpoints.md` | Diseño de recursos REST |
| `08_desarrollo.md` | Metodología de desarrollo de MAPA |
| `09_roadmap.md` | Evolución prevista del proyecto |

---

# Estado actual

La implementación actual permite:

- integrar múltiples bases PostgreSQL;
- construir modelos de información mediante vistas SQL;
- publicar automáticamente APIs REST;
- generar documentación OpenAPI;
- validar recursos mediante Swagger UI.

La primera implementación se desarrolló utilizando información del dominio RANIE, aunque la arquitectura fue diseñada para incorporar nuevos dominios de información sin modificar el modelo general.

---

# Filosofía

En LocalAPI:

- el modelo de información es el producto;
- la API es una consecuencia del modelo;
- la documentación se genera automáticamente;
- las aplicaciones consumen la API, nunca la base de datos.

Cada MVP construido mediante LocalAPI busca responder una pregunta concreta, demostrar la viabilidad de una solución y servir como base para futuros desarrollos.