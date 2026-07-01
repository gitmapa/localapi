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
| Fecha de creación | Pendiente |
| Última actualización | Pendiente |

---

# Descripción

El Padrón de Establecimientos Educativos constituye la publicación oficial del listado de establecimientos educativos de la Ciudad.

Integra información proveniente de distintas fuentes institucionales para ofrecer una representación única, consistente y reutilizable de cada establecimiento educativo y sus localizaciones.

---

# Objetivo

Producir una única publicación institucional que concentre la información necesaria para identificar, localizar y consultar los establecimientos educativos de la Ciudad.

El producto constituye la referencia oficial utilizada por la UEICEE y sirve como base para publicaciones, consultas, análisis y futuras aplicaciones.

---

# Responsable

| Campo | Valor |
|-------|-------|
| Organismo responsable | UEICEE |
| Desarrollo e integración | MAPA |

---

# Cobertura

| Campo | Valor |
|-------|-------|
| Jurisdicción | Ciudad Autónoma de Buenos Aires |
| Cobertura temática | Establecimientos educativos |
| Cobertura espacial | Toda la Ciudad |

---

# Unidad de publicación

Cada registro representa una **localización de un establecimiento educativo**, identificada por la combinación:

- CUE
- Anexo

y enriquecida con la información edilicia correspondiente (CUI).

---

# Fuentes de información

| Fuente | Finalidad |
|---------|-----------|
| Padrón Nacional | Identidad educativa del establecimiento |
| UEICEE | Información edilicia y geográfica |

---

# Actualización

La incorporación de información proveniente de las fuentes no posee una frecuencia fija.

Las actualizaciones se realizan cada vez que se dispone de una nueva versión de las bases de origen.

---

# Publicación

La publicación oficial del producto se realiza **dos veces por año**, mediante cortes institucionales.

Meses previstos:

- Marzo
- Noviembre

Cada publicación constituye una fotografía oficial del padrón correspondiente a esa fecha.

---

# Público destinatario

El producto se encuentra orientado a:

- áreas internas de la UEICEE;
- ciudadanía;
- desarrolladores;
- procesos de integración de información.

---

# Formatos de publicación

El mismo producto podrá publicarse mediante distintos formatos.

- API REST
- JSON
- CSV
- XLSX
- GeoJSON

Todos ellos representan el mismo modelo de información.

---

# Productos derivados

A partir del Padrón de Establecimientos Educativos podrán desarrollarse, entre otros:

- mapas;
- aplicaciones web;
- consultas por establecimiento;
- indicadores;
- publicaciones estadísticas.

---

# Licencia

Pendiente de definición institucional.

---

# Observaciones metodológicas

El producto integra información proveniente de múltiples sistemas institucionales.

La implementación mediante LocalAPI desacopla la publicación oficial de los sistemas de origen, permitiendo reconstruir el producto a partir de un modelo de información único, documentado y reutilizable.

Las publicaciones semestrales constituyen versiones oficiales del padrón y deberán preservarse como cortes históricos para garantizar la trazabilidad de la información y la reproducibilidad de análisis e informes.

---

# Estado del desarrollo

| Etapa | Estado |
|--------|--------|
| Definición conceptual | ✔ Finalizada |
| Metadatos | ✔ Finalizada |
| Diccionario de datos | Pendiente |
| Modelo lógico | Pendiente |
| Vista SQL | Pendiente |
| Endpoint | Pendiente |
| Aplicación de referencia | Pendiente |