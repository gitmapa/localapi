# Metadatos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Identificación

| Campo | Valor |
|-------|-------|
| Código | 001 |
| Nombre | Padrón de Establecimientos Educativos |
| Estado | En desarrollo (MVP) |
| Versión | 1.0 |
| Organismo responsable | UEICEE |
| Desarrollo e integración | MAPA |
| Plataforma | LocalAPI |

---

# Descripción

El Padrón de Establecimientos Educativos constituye el producto institucional que integra la información necesaria para identificar, localizar y consultar los establecimientos educativos de la Ciudad Autónoma de Buenos Aires.

Su construcción combina información proveniente de distintas fuentes institucionales, respetando las responsabilidades de cada organismo y publicando un modelo de información único, consistente y reutilizable.

Este producto constituye el primer MVP desarrollado sobre la infraestructura LocalAPI.

---

# Objetivo

Construir una única publicación institucional que concentre la información necesaria para:

- identificar establecimientos educativos;
- localizar sedes y anexos;
- consultar información territorial;
- publicar datos mediante API;
- exportar información en distintos formatos;
- servir como base para aplicaciones institucionales.

---

# Cobertura

| Campo | Valor |
|-------|-------|
| Jurisdicción | Ciudad Autónoma de Buenos Aires |
| Cobertura temática | Establecimientos educativos |
| Cobertura espacial | Toda la Ciudad Autónoma de Buenos Aires |
| Unidad de publicación | CUEANEXO |

---

# Unidad de publicación

Cada registro representa una localización (sede o anexo) de un establecimiento educativo.

La unidad de publicación se identifica mediante:

- CUE
- Anexo

cuya combinación constituye el identificador **CUEANEXO**.

Cada registro se encuentra enriquecido con la información edilicia correspondiente al edificio (CUI) donde funciona dicha localización.

---

# Fuentes de información

| Dominio | Fuente de verdad |
|---------|------------------|
| Identidad educativa | Padrón Nacional |
| Dirección postal | Padrón Nacional |
| Información territorial | UEICEE |
| Información geográfica | UEICEE |

LocalAPI integra estas fuentes sin reemplazar los procesos de administración de datos existentes.

---

# Frecuencia de actualización

El modelo integrado puede actualizarse cada vez que se dispone de una nueva versión de alguna de las fuentes institucionales.

No existe una frecuencia técnica obligatoria.

La actualización depende exclusivamente de la disponibilidad de nuevas versiones de las bases de origen.

---

# Publicación oficial

La publicación institucional del padrón se realiza mediante cortes oficiales.

Actualmente se prevén dos publicaciones por año:

- Marzo
- Noviembre

Cada publicación constituye una versión oficial del padrón correspondiente a una fecha determinada.

---

# Snapshots

Además de la versión vigente, el producto contempla la conservación de publicaciones históricas.

Cada snapshot representa una fotografía completa del producto en una fecha determinada.

Los snapshots permiten:

- reproducir publicaciones oficiales;
- comparar versiones del padrón;
- garantizar trazabilidad;
- respaldar informes e indicadores históricos.

Los snapshots forman parte del producto y no constituyen copias de respaldo de las bases de datos.

---

# Público destinatario

El producto se encuentra orientado a:

- áreas técnicas de la UEICEE;
- áreas de gestión;
- ciudadanía;
- desarrolladores;
- aplicaciones institucionales;
- procesos de integración.

---

# Formatos de publicación

El mismo modelo de información podrá publicarse mediante distintos formatos.

- API REST
- JSON
- CSV
- XLSX
- GeoJSON

Todos representan exactamente el mismo producto.

La diferencia radica únicamente en el mecanismo de consumo.

---

# Productos derivados

A partir del Producto 001 podrán desarrollarse, entre otros:

- visor web del padrón;
- mapas institucionales;
- consultas por establecimiento;
- consultas por edificio;
- exportaciones temáticas;
- indicadores;
- publicaciones estadísticas.

Todos estos recursos consumirán el mismo modelo de información.

---

# Licencia

Pendiente de definición institucional.

---

# Observaciones metodológicas

El Producto 001 integra información proveniente de múltiples sistemas institucionales.

Cada atributo conserva una única fuente de verdad y permanece bajo la responsabilidad del organismo que lo administra.

LocalAPI documenta el modelo de información, implementa su integración y publica el producto mediante distintos mecanismos, sin modificar las bases de origen.

El desarrollo del Producto 001 constituye la validación de la metodología propuesta por LocalAPI para la construcción de productos institucionales reutilizables.

---

# Estado del desarrollo

| Etapa | Estado |
|--------|--------|
| Definición conceptual | ✔ Finalizada |
| Metadatos | ✔ Finalizada |
| Hallazgos | ✔ Finalizada |
| Decisiones de modelo | ✔ Finalizada |
| Diccionario de datos | ✔ Finalizada |
| Modelo lógico | ✔ Finalizada |
| Vista SQL | En desarrollo |
| Endpoint | Pendiente |
| Aplicación de referencia | Pendiente |
| Snapshots | Pendiente |

---

# Estado esperado del MVP

El Producto 001 se considerará finalizado cuando permita:

- consultar el padrón mediante API;
- filtrar información;
- descargar el padrón en distintos formatos;
- visualizar los establecimientos sobre un mapa;
- conservar publicaciones históricas mediante snapshots oficiales.

En ese momento quedará demostrado el ciclo completo de construcción de un producto institucional utilizando LocalAPI.