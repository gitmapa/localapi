# 001. Padrón de Establecimientos Educativos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

El Padrón de Establecimientos Educativos constituye la publicación oficial del listado de establecimientos educativos de la Ciudad.

Integra información proveniente de distintos sistemas institucionales para ofrecer una representación única, consistente y reutilizable de cada establecimiento y sus localizaciones.

Este producto constituye el primer MVP desarrollado sobre la infraestructura LocalAPI.

---

# Problema que resuelve

La información necesaria para construir el padrón no reside en un único sistema.

Actualmente intervienen diferentes fuentes de datos, administradas por áreas distintas, con responsabilidades específicas.

LocalAPI integra dichas fuentes y genera una única publicación institucional, desacoplada de los sistemas que originan la información.

---

# Conceptos fundamentales

## Establecimiento Educativo

Unidad institucional identificada por un **CUE**.

Un establecimiento puede funcionar en una o más localizaciones.

---

## Localización

Unidad identificada por la combinación:

- CUE
- Anexo

La combinación de ambos constituye un **CUEANEXO**.

Cada fila publicada por este producto representa una localización.

---

## Edificio

Unidad edilicia identificada por un **CUI**.

Un edificio puede albergar uno o más establecimientos educativos.

Un establecimiento puede desarrollar sus actividades en uno o más edificios.

La relación entre establecimientos y edificios constituye uno de los principales procesos de integración realizados por MAPA.

---

# Unidad de publicación

Cada registro publicado representa:

> **Una localización de un establecimiento educativo (CUE + Anexo), enriquecida con la información edilicia correspondiente (CUI).**

Esta unidad de publicación coincide con la utilizada en la publicación institucional vigente.

---

# Fuentes de información

## Padrón Nacional

Aporta la identidad educativa del establecimiento.

Entre otros datos:

- CUE
- Anexo
- Nombre
- Gestión
- Nivel
- Modalidad
- Oferta educativa

La información es incorporada mediante actualizaciones periódicas realizadas sobre una copia local.

---

## RANIE

Aporta la identidad edilicia.

Entre otros datos:

- CUI
- Coordenadas
- Dirección
- Barrio
- Comuna
- Distrito Escolar
- Información de infraestructura

MAPA es responsable de la administración de esta información.

---

# Modelo de integración

LocalAPI unifica ambas fuentes para construir un único modelo de información.

El consumidor desconoce el origen de cada dato.

La integración ocurre íntegramente dentro de PostgreSQL mediante vistas SQL.

---

# Publicación vigente

El producto mantiene permanentemente una versión actualizada que refleja el último estado conocido de las fuentes de información disponibles.

Esta versión constituye la base para:

- consultas;
- aplicaciones;
- mapas;
- exportaciones;
- servicios API.

---

# Publicaciones históricas

Durante el ciclo anual se realizan cortes oficiales del padrón en fechas acordadas entre las áreas usuarias.

Cada corte genera una publicación inmutable que preserva exactamente el estado del padrón en ese momento.

Estas publicaciones permiten:

- realizar comparaciones temporales;
- reproducir informes oficiales;
- garantizar trazabilidad;
- mantener consistencia estadística entre áreas.

Los cortes históricos forman parte del producto y no constituyen copias de respaldo.

Constituyen publicaciones oficiales.

---

# Consumidores

Este producto podrá ser consumido por:

- aplicaciones web;
- visores cartográficos;
- procesos estadísticos;
- tableros de control;
- sistemas institucionales;
- procesos de integración;
- usuarios externos autorizados.

Todos ellos consumirán el mismo modelo de información.

---

# Formatos de publicación

El mismo producto podrá publicarse mediante distintos formatos.

- API REST
- JSON
- CSV
- XLSX
- GeoJSON

Los formatos de salida no modifican el modelo de información.

Únicamente representan distintas formas de consumir el mismo producto.

---

# MVP

La primera implementación tendrá como objetivo demostrar que es posible generar íntegramente este producto utilizando LocalAPI.

El MVP deberá reemplazar el proceso actual de generación del listado publicado, manteniendo la misma calidad de información e incorporando las ventajas propias de una arquitectura basada en APIs.

---

# Evolución prevista

Una vez consolidado este producto podrán desarrollarse recursos derivados, entre ellos:

- consultas por establecimiento;
- consultas por edificio;
- mapas interactivos;
- indicadores;
- series históricas;
- servicios para otras aplicaciones.

Todos ellos reutilizarán el mismo modelo de información construido para este producto.

---

# Estado

**En diseño.**

La definición conceptual del producto se encuentra finalizada.

La siguiente etapa consiste en diseñar el modelo de información que permitirá implementarlo mediante LocalAPI.