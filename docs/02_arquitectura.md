# 02. Arquitectura

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

LocalAPI implementa una arquitectura de integración de datos orientada a construir APIs funcionales a partir de múltiples bases institucionales, minimizando el desarrollo de software y concentrando la lógica de integración dentro de PostgreSQL.

La arquitectura fue diseñada para:

- integrar fuentes heterogéneas;
- evitar duplicación de datos;
- construir modelos de información reutilizables;
- publicar APIs REST automáticamente;
- facilitar el desarrollo de aplicaciones consumidoras.

---

# Arquitectura general

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
     schemas src_*                   esquema api
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

# Componentes

## Bases fuente

Las bases institucionales continúan siendo administradas por sus responsables.

LocalAPI nunca modifica información en ellas.

Su única función es consultarlas.

---

## PostgreSQL FDW

PostgreSQL Foreign Data Wrapper (FDW) permite acceder a tablas ubicadas en otras bases como si fueran tablas locales.

De esta manera se evita:

- replicar información;
- construir procesos ETL innecesarios;
- mantener múltiples copias de los mismos datos.

---

## Base integradora

La base `ranie_dev` constituye el núcleo de LocalAPI.

Su función no es almacenar información institucional sino integrar información proveniente de distintas fuentes.

Dentro de esta base conviven:

- conexiones FDW;
- vistas de integración;
- permisos;
- publicación de APIs.

---

## Schemas de origen

Cada fuente remota se incorpora mediante un schema específico.

Ejemplo:

- `src_ranie_app`
- `src_ranie_mapa`
- `src_padron_nacion`

Estos schemas contienen exclusivamente tablas remotas importadas mediante FDW.

No contienen lógica de negocio.

---

## Schema API

Toda información publicada se expone mediante el schema `api`.

Las aplicaciones cliente nunca deberían consultar directamente tablas provenientes de las bases fuente.

El contrato de datos siempre está representado por vistas.

---

## Vistas

Las vistas constituyen el verdadero modelo de información.

En ellas se implementan:

- uniones entre fuentes;
- normalizaciones;
- traducciones;
- filtros;
- enriquecimiento de datos;
- ocultamiento de complejidad técnica.

Cada vista representa un recurso funcional que posteriormente será publicado como endpoint REST.

---

## PostgREST

PostgREST transforma automáticamente las vistas del schema `api` en endpoints REST.

No requiere programación adicional.

Cada modificación realizada sobre una vista queda inmediatamente disponible mediante la API.

---

## OpenAPI

La documentación OpenAPI se genera automáticamente a partir de la estructura de la base.

No requiere mantenimiento manual.

La documentación siempre refleja el estado real de la API.

---

## Swagger UI

Swagger UI consume el documento OpenAPI generado por PostgREST.

Su función es:

- explorar endpoints;
- probar consultas;
- visualizar parámetros;
- validar respuestas.

No implementa ninguna lógica propia.

---

## Aplicaciones cliente

Las aplicaciones desarrolladas sobre LocalAPI consumen únicamente endpoints REST.

No conocen la estructura interna de las bases de datos.

Esto permite modificar la implementación interna sin afectar a los consumidores.

---

# Flujo de publicación

Todo nuevo recurso publicado sigue el mismo proceso.

1. Identificar las fuentes de información.
2. Integrar los datos mediante vistas SQL.
3. Publicar la vista dentro del schema `api`.
4. Verificar automáticamente el endpoint generado.
5. Validar el recurso mediante Swagger.
6. Consumir el endpoint desde aplicaciones cliente.

---

# Beneficios

La arquitectura permite:

- integrar múltiples bases sin copiarlas;
- centralizar la lógica de negocio;
- reducir el desarrollo de backend;
- generar documentación automáticamente;
- construir MVP funcionales en muy poco tiempo;
- validar modelos de información antes de su desarrollo institucional.

---

# Principio fundamental

En LocalAPI el modelo de información constituye el verdadero producto.

Las aplicaciones cliente, la documentación OpenAPI y los endpoints REST son consecuencias automáticas de ese modelo.