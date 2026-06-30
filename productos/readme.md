# Productos

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Esta carpeta reúne los productos de información desarrollados mediante LocalAPI.

Un producto constituye una publicación institucional construida a partir de uno o más modelos de información integrados.

Cada producto puede publicarse mediante distintos formatos (API, JSON, CSV, XLSX, GeoJSON, etc.), pero mantiene un único modelo de información como fuente de verdad.

---

# Metodología

Todos los productos desarrollados mediante LocalAPI siguen el mismo proceso.

```
Necesidad institucional

        ↓

Producto de información

        ↓

Modelo de información

        ↓

Vista SQL

        ↓

Endpoint REST

        ↓

Aplicaciones consumidoras

        ↓

Publicaciones
```

El objetivo de LocalAPI no es construir APIs.

El objetivo es construir productos de información reutilizables, donde la API constituye uno de los mecanismos de publicación.

---

# Productos

| Código | Producto | Estado |
|---------|----------|--------|
| 001 | Padrón de Establecimientos Educativos | En desarrollo |

---

# Estructura

Cada producto posee su propia carpeta y documentación independiente.

Ejemplo:

```
productos/

    001_padron_establecimientos/

        README.md
        modelo_conceptual.md
        modelo_logico.md
        vista_sql.md
        endpoint.md
        snapshots.md
        app.md
        TODO.md
```

No todos los documentos existirán desde el inicio.

Cada producto irá incorporando documentación a medida que evolucione.

---

# Principios

Todos los productos desarrollados mediante LocalAPI cumplen los siguientes principios:

- responden a una necesidad institucional concreta;
- integran información proveniente de una o más fuentes;
- poseen un modelo de información claramente definido;
- pueden publicarse mediante distintos formatos;
- mantienen una única fuente de verdad;
- son reutilizables por distintas aplicaciones.

---

# Evolución

El catálogo de productos crecerá de manera incremental.

Cada nuevo producto será independiente de los anteriores, pero compartirá la misma metodología de diseño, integración y publicación definida por LocalAPI.