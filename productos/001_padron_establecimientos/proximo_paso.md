# Próximos pasos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Estado actual

La etapa de análisis y diseño del Producto 001 se encuentra finalizada.

Se encuentran documentados:

- Objetivo.
- Metadatos.
- Hallazgos.
- Decisiones de modelo.
- Diccionario de datos.
- Modelo lógico.
- Diseño de la vista SQL.
- Diseño del endpoint.

La infraestructura de LocalAPI también se encuentra completamente operativa.

A partir de este punto comienza la etapa de implementación.

---

# Objetivo inmediato

Implementar el **Producto 001 – Padrón de Establecimientos Educativos** respetando íntegramente el modelo de información documentado.

La implementación no debe introducir nuevas decisiones funcionales.

---

# Plan de trabajo

## Etapa 1 — Vista SQL

Construir la vista:

```
api.padron_establecimientos
```

utilizando como referencia:

- modelo lógico;
- diccionario de datos;
- fuentes de verdad;
- transformaciones documentadas.

La vista deberá publicar exactamente las columnas definidas para el Producto 001.

---

## Etapa 2 — Validación

Comparar la vista contra la publicación oficial.

Validar:

- cantidad de registros;
- cantidad de columnas;
- nombres;
- orden;
- contenido;
- transformaciones.

El objetivo consiste en obtener un resultado idéntico al padrón oficial.

---

## Etapa 3 — Publicación

Publicar la vista mediante PostgREST.

Verificar:

- filtros;
- ordenamientos;
- consultas;
- documentación Swagger.

---

## Etapa 4 — Aplicación de referencia

Desarrollar una aplicación mínima para demostrar el consumo del producto.

El MVP contempla dos secciones:

### Padrón

- consulta;
- filtros;
- descarga.

### Mapa

- visualización geográfica;
- navegación sobre los establecimientos.

La aplicación constituye una demostración del producto y no un sistema de gestión.

---

## Etapa 5 — Snapshots

Definir e implementar el mecanismo para conservar publicaciones históricas del padrón.

Cada snapshot representará una publicación oficial correspondiente a una fecha determinada.

---

# Organización del trabajo

La documentación funcional del producto permanece dentro de:

```
productos/
001_padron_establecimientos/
```

La implementación técnica comenzará en:

```
sql/
001_padron_establecimientos/
```

Se prevé crear inicialmente los siguientes archivos:

```
01_vista_padron_establecimientos.sql
02_validacion_excel.sql
```

La documentación y la implementación evolucionarán de forma coordinada.

---

# Criterios de finalización del MVP

El Producto 001 se considerará finalizado cuando un usuario pueda:

- consultar el padrón desde un navegador;
- filtrar registros;
- descargar la información;
- consumir el producto mediante API REST;
- visualizar los establecimientos sobre un mapa.

---

# Próximo paso

El siguiente hito del proyecto consiste en construir la primera versión de la vista SQL del Producto 001 y validar que reproduce exactamente la publicación oficial.

Una vez alcanzado ese objetivo comenzará la etapa de publicación y desarrollo de la aplicación de referencia.