# LocalAPI

> Laboratorio para diseñar, integrar y publicar productos de información.

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-blue?logo=postgresql)
![PostGIS](https://img.shields.io/badge/PostGIS-enabled-green)
![PostgREST](https://img.shields.io/badge/PostgREST-REST%20API-5C2D91)
![Swagger](https://img.shields.io/badge/Swagger-OpenAPI-85EA2D?logo=swagger)
![FDW](https://img.shields.io/badge/postgres__fdw-enabled-blueviolet)
![Status](https://img.shields.io/badge/status-MVP-orange)

---

# ¿Qué es LocalAPI?

LocalAPI es un laboratorio desarrollado por **MAPA (UEICEE)** para integrar información proveniente de múltiples bases PostgreSQL, construir modelos de información y publicarlos mediante APIs REST.

Su objetivo no es desarrollar APIs por sí mismas.

Su objetivo es construir **productos de información institucionales**, documentados, reutilizables y desacoplados de los sistemas que administran los datos.

La API constituye uno de los mecanismos de publicación de dichos productos.

---

# Objetivos

LocalAPI busca demostrar que es posible construir productos institucionales completos mediante una arquitectura simple basada en PostgreSQL.

Cada producto debe poder:

- integrar información proveniente de distintas fuentes;
- documentar claramente su modelo de información;
- publicarse mediante una API REST;
- consumirse desde aplicaciones web;
- exportarse en distintos formatos;
- evolucionar sin modificar las bases de origen.

---

# Principios

## El producto precede a la implementación

El desarrollo comienza comprendiendo el problema que debe resolverse.

La implementación técnica surge posteriormente como consecuencia del modelo diseñado.

---

## El modelo precede a la API

La API refleja el modelo de información.

No lo define.

---

## Una única fuente de verdad

Cada atributo publicado posee un único sistema responsable de su administración.

LocalAPI integra información.

No reemplaza procesos de carga.

---

## No duplicar responsabilidades

Cada organismo continúa siendo responsable de la información que administra.

LocalAPI reutiliza esas fuentes para construir productos institucionales integrados.

---

## La documentación forma parte del producto

Cada producto posee documentación propia.

El modelo de información debe poder comprenderse independientemente de la implementación SQL.

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

La arquitectura permanece estable.

Lo que evoluciona son los modelos de información construidos sobre ella.

---

# Método de trabajo

Todo producto desarrollado mediante LocalAPI sigue el mismo proceso.

```
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

Aplicación consumidora

↓

Validación contra la publicación oficial
```

La implementación constituye la última etapa del proceso.

---

# Productos

Cada necesidad da origen a un producto independiente.

Actualmente el laboratorio desarrolla:

| Código | Producto | Estado |
|---------|----------|--------|
| 001 | Padrón de Establecimientos Educativos | En desarrollo |

Cada producto posee su propia documentación metodológica, modelo lógico, vista SQL, endpoint y aplicación de referencia.

---

# Infraestructura

La implementación actual utiliza:

- PostgreSQL
- PostGIS
- PostgreSQL Foreign Data Wrapper (FDW)
- PostgREST
- Swagger UI
- Python (servidor HTTP local)

No requiere:

- Docker
- Kubernetes
- OAuth
- CI/CD

El objetivo del laboratorio es validar productos institucionales mediante un MVP funcional.

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
├── productos/
│   └── 001_padron_establecimientos/
│
├── sql/
│
└── restore.md
```

---

# Documentación

La documentación del proyecto se divide en dos niveles.

## Documentación general

Describe la infraestructura y la metodología de LocalAPI.

## Documentación por producto

Cada producto documenta:

- objetivo;
- metadatos;
- hallazgos;
- decisiones de modelo;
- diccionario de datos;
- modelo lógico;
- vista SQL;
- endpoint;
- aplicación de referencia.

---

# Estado actual

La infraestructura del laboratorio se encuentra finalizada.

Actualmente el trabajo se concentra en el desarrollo del **Producto 001 – Padrón de Establecimientos Educativos**, cuyo objetivo es demostrar el ciclo completo de construcción de un producto institucional:

- integración de datos;
- modelo de información;
- publicación mediante API;
- aplicación consumidora;
- validación contra la publicación oficial.

---

# Filosofía

LocalAPI no desarrolla APIs.

LocalAPI desarrolla productos de información.

La API es solamente uno de los formatos mediante los cuales esos productos pueden publicarse y reutilizarse.