# Próximos pasos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Estado general

El Producto 001 ya completó su etapa de análisis y diseño.

La infraestructura de LocalAPI también se encuentra finalizada.

A partir de este punto el trabajo consiste exclusivamente en implementar el producto documentado.

---

# Estado de la documentación

## Documentación general

| Documento | Estado |
|-----------|--------|
| README | ✔ |
| Introducción | ✔ |
| Arquitectura | ✔ |
| Instalación | ✔ |
| PostgREST | ✔ |
| Swagger | ✔ |
| Seguridad | ✔ |
| Endpoints | ✔ |
| Desarrollo | ✔ |
| Roadmap | ✔ |

---

## Documentación del Producto 001

| Documento | Estado |
|-----------|--------|
| README | ✔ |
| Metadatos | ✔ |
| Hallazgos | ✔ |
| Decisiones de modelo | ✔ |
| Diccionario de datos | ✔ |
| Modelo lógico | ✔ |
| Vista SQL | ⏳ |
| Endpoint | ⏳ |
| Aplicación | ⏳ |
| Snapshots | ⏳ |

---

# Estado del diseño

## Definido

- Objetivo del producto.
- Alcance.
- Unidad de publicación.
- Modelo conceptual.
- Fuentes de verdad.
- Dominios funcionales.
- Hallazgos.
- Decisiones de modelo.
- Diccionario de datos.

No deberían aparecer nuevas decisiones conceptuales durante la implementación.

---

# Implementación inmediata

La siguiente etapa consiste en construir la implementación del modelo.

Orden de trabajo:

1. Vista SQL.
2. Validación contra la publicación oficial.
3. Endpoint REST.
4. Aplicación consumidora.
5. Snapshots.

---

# Vista SQL

Objetivo:

Construir una vista que reproduzca exactamente el contenido publicado por el Padrón de Establecimientos Educativos.

La vista deberá respetar íntegramente:

- el modelo lógico;
- el diccionario de datos;
- las fuentes de verdad;
- las transformaciones documentadas.

---

# Validación

Una vez implementada la vista SQL deberá compararse contra la publicación oficial.

La validación comprenderá:

- cantidad de registros;
- estructura;
- columnas;
- contenido;
- transformaciones.

El objetivo consiste en garantizar que el producto reproduce exactamente la publicación institucional.

---

# Endpoint

Una vez validada la vista SQL se publicará mediante PostgREST.

No deberán desarrollarse componentes adicionales.

La infraestructura ya se encuentra disponible.

---

# Aplicación de referencia

La aplicación tendrá como objetivo demostrar el consumo del producto.

El MVP contempla una interfaz extremadamente simple con dos pestañas.

## Padrón

Permitirá:

- consultar;
- filtrar;
- ordenar;
- descargar.

## Mapa

Permitirá visualizar geográficamente los registros publicados utilizando las coordenadas integradas por el producto.

La aplicación constituye una demostración del producto y no un sistema de gestión.

---

# Snapshots

El producto deberá permitir conservar publicaciones históricas del padrón.

Cada snapshot representará una versión oficial correspondiente a una fecha determinada.

Inicialmente se prevé conservar las publicaciones de:

- Marzo.
- Noviembre.

El mecanismo de implementación será definido una vez concluida la vista SQL.

---

# MVP

El Producto 001 se considerará terminado cuando un usuario pueda abrir un navegador y:

- consultar el padrón;
- filtrar registros;
- descargar la información;
- consumir el producto mediante API;
- visualizar el padrón sobre un mapa.

---

# Lo que NO forma parte del MVP

Para mantener el alcance controlado, el MVP no incluye:

- Docker.
- Kubernetes.
- OAuth.
- CI/CD.
- Autenticación avanzada.
- Nuevos productos.

Estas capacidades podrán evaluarse una vez validado el Producto 001.

---

# Productos posteriores

Una vez concluido el Producto 001, la metodología desarrollada permitirá construir nuevos productos reutilizando prácticamente toda la infraestructura y gran parte del modelo documental.

El candidato natural para continuar el laboratorio será el:

**Producto 002 – Padrón de Ofertas Educativas.**

Este producto reutilizará:

- la infraestructura;
- la metodología;
- la arquitectura documental;
- el modelo de integración;
- gran parte de las fuentes de información utilizadas por el Producto 001.

---

# Estado actual

La etapa de arquitectura del Producto 001 puede considerarse finalizada.

El próximo hito del proyecto consiste en implementar y validar la vista SQL que materializará el modelo de información documentado.