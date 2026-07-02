# 09. Roadmap

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Este documento describe la evolución prevista de LocalAPI.

El roadmap no representa únicamente un cronograma de desarrollo.

Representa la evolución del laboratorio mediante la construcción progresiva de productos de información reutilizables.

---

# Estado actual

La infraestructura de LocalAPI se encuentra finalizada.

Actualmente el laboratorio dispone de:

- PostgreSQL;
- PostgreSQL Foreign Data Wrapper (FDW);
- PostGIS;
- PostgREST;
- Swagger UI;
- repositorio documentado;
- metodología de desarrollo.

A partir de este punto el crecimiento del proyecto no depende de incorporar nuevas tecnologías sino de desarrollar nuevos productos.

---

# Etapa 1 — Producto piloto

## Producto 001

**Padrón de Establecimientos Educativos**

Objetivo:

Demostrar el ciclo completo de construcción de un producto institucional.

Incluye:

- integración de fuentes;
- modelo lógico;
- diccionario de datos;
- vista SQL;
- endpoint REST;
- aplicación de referencia;
- validación contra la publicación oficial.

Esta etapa constituye el MVP de LocalAPI.

---

# Etapa 2 — Consolidación

Una vez finalizado el Producto 001 se completará la documentación metodológica del laboratorio.

El objetivo consiste en consolidar un método reproducible para desarrollar nuevos productos.

La experiencia obtenida durante el MVP quedará incorporada a la documentación general del proyecto.

---

# Etapa 3 — Nuevos productos

Con la metodología consolidada podrán desarrollarse nuevos productos reutilizando la infraestructura existente.

Entre los candidatos identificados se encuentran:

- Padrón de Ofertas Educativas.
- Padrón de Edificios.
- Productos territoriales.
- Productos estadísticos.
- Productos cartográficos.

Cada nuevo producto reutilizará:

- la arquitectura;
- la metodología;
- la documentación;
- la estrategia de publicación.

---

# Evolución de la infraestructura

La infraestructura actual fue diseñada para mantenerse estable.

No se prevén cambios significativos en:

- PostgreSQL;
- FDW;
- PostgREST;
- Swagger;
- arquitectura de publicación.

La evolución del proyecto ocurrirá principalmente en los modelos de información y no en la plataforma tecnológica.

---

# Evolución metodológica

Cada producto construido permitirá mejorar la metodología de trabajo.

Los principales componentes metodológicos son:

- definición del producto;
- identificación de las fuentes de verdad;
- documentación de hallazgos;
- decisiones de modelo;
- diseño del modelo lógico;
- construcción del diccionario de datos;
- implementación mediante vistas SQL;
- publicación;
- validación.

Cada nuevo desarrollo deberá recorrer este mismo proceso.

---

# Estado del MVP

## Julio

Objetivos:

- completar la documentación del Producto 001;
- implementar la vista SQL;
- publicar el endpoint REST;
- validar el resultado contra la publicación oficial.

Resultado esperado:

El Padrón de Establecimientos Educativos podrá consultarse mediante API.

---

## Agosto

Objetivos:

- desarrollar la aplicación de referencia;
- incorporar descarga de datos;
- incorporar visualización cartográfica;
- implementar el primer corte histórico;
- preparar la demostración institucional.

Resultado esperado:

Un usuario podrá abrir un navegador y:

- consultar el padrón;
- filtrarlo;
- descargarlo;
- consumirlo mediante API;
- visualizarlo sobre un mapa.

Con ello quedará demostrado el concepto de LocalAPI.

---

# Visión

El objetivo de LocalAPI no consiste en desarrollar una colección de APIs.

El objetivo consiste en construir una colección de productos de información institucionales, documentados, reutilizables y desacoplados de los sistemas que administran los datos.

Cada nuevo producto incrementará el conocimiento acumulado por el laboratorio y reducirá el esfuerzo necesario para desarrollar los siguientes.

---

# Resultado esperado

Al finalizar el MVP, LocalAPI habrá demostrado que una arquitectura simple basada en PostgreSQL puede utilizarse para:

- integrar múltiples fuentes institucionales;
- construir modelos de información;
- publicar productos mediante APIs REST;
- desarrollar aplicaciones consumidoras;
- mantener documentación técnica y metodológica consistente.

El Producto 001 constituirá la referencia para todos los desarrollos posteriores del laboratorio.