# Producto 001 — Padrón de Establecimientos Educativos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

El Producto 001 reconstruye la publicación oficial del **Padrón de Establecimientos Educativos** de la Ciudad Autónoma de Buenos Aires utilizando un modelo de información integrado.

Su desarrollo constituye el primer Producto Mínimo Viable (MVP) de LocalAPI y tiene como objetivo demostrar que es posible construir un producto institucional completo a partir de múltiples fuentes de información, respetando las responsabilidades de cada organismo y publicándolo mediante una arquitectura abierta basada en PostgreSQL y PostgREST.

---

# Problema que resuelve

La información necesaria para construir el padrón oficial no reside en un único sistema.

Los datos educativos, postales, territoriales y geográficos son administrados por distintos organismos y aplicaciones, cada uno con responsabilidades específicas.

Históricamente, la construcción del padrón implicó consultas complejas, transformaciones manuales y procesos de integración difíciles de documentar y reutilizar.

El Producto 001 reemplaza ese proceso mediante un modelo de información único, documentado y reproducible.

---

# Alcance

El producto publica exclusivamente la información correspondiente al **Padrón de Establecimientos Educativos**.

Incluye:

- identidad educativa;
- identidad edilicia;
- dirección postal;
- información territorial;
- información geográfica.

No incluye:

- ofertas educativas;
- dependencia funcional;
- tipo de establecimiento;
- indicadores;
- estadísticas;
- información correspondiente a otros productos institucionales.

---

# Unidad de publicación

La unidad de publicación es el **CUEANEXO**.

Cada registro representa una localización (sede o anexo) de un establecimiento educativo.

Sobre esa unidad se integran los atributos provenientes de las distintas fuentes de información.

---

# Modelo conceptual

El producto integra tres conceptos fundamentales.

## Establecimiento

Representa la unidad institucional identificada mediante un **CUE**.

Un establecimiento puede poseer una o más localizaciones.

---

## Localización

Representa una sede o anexo.

Se identifica mediante:

**CUE + Anexo**

La combinación de ambos constituye el **CUEANEXO**, unidad de publicación del producto.

---

## Edificio

Representa la infraestructura física donde funcionan una o más localizaciones.

Se identifica mediante un **CUI**.

Cada edificio aporta los atributos territoriales y geográficos heredados por las localizaciones que contiene.

---

# Integración

El principal proceso realizado por el Producto 001 consiste en integrar la identidad educativa con la identidad edilicia.

La relación entre ambas fuentes se establece mediante:

```
padron_nacion.public.domicilio.cui
```

Este hallazgo constituye el punto de integración central del producto.

---

# Fuentes de verdad

Cada conjunto de información posee un único responsable institucional.

| Dominio | Fuente |
|---------|--------|
| Identidad educativa | Padrón Nacional |
| Dirección postal | Padrón Nacional |
| Información territorial | UEICEE |
| Información geográfica | UEICEE |

LocalAPI integra estas fuentes.

No administra información propia.

---

# Principios de diseño

El Producto 001 fue desarrollado respetando los siguientes principios.

## Una única fuente de verdad

Cada atributo publicado posee un único sistema responsable de su administración.

---

## No duplicar responsabilidades

Los procesos de carga permanecen en los sistemas que administran los datos.

LocalAPI reutiliza esa información para construir un producto integrado.

---

## El modelo precede a la implementación

Antes de escribir una vista SQL se documentan:

- hallazgos;
- decisiones de modelo;
- diccionario de datos;
- modelo lógico.

La implementación constituye la última etapa del proceso.

---

## El Excel valida

La publicación oficial constituye el mecanismo de validación del producto.

No define su modelo de información.

El modelo surge del análisis del dominio y de las responsabilidades institucionales.

---

# Documentación

El Producto 001 se documenta mediante los siguientes archivos.

| Documento | Finalidad |
|-----------|-----------|
| `README.md` | Presentación del producto |
| `metadatos.md` | Información descriptiva y administrativa |
| `hallazgos.md` | Conocimiento descubierto durante el análisis |
| `decisiones_modelo.md` | Decisiones funcionales adoptadas |
| `diccionario_de_datos.md` | Contrato público del producto |
| `modelo_logico.md` | Modelo conceptual |
| `vista_sql.md` | Implementación del modelo |
| `endpoint.md` | Publicación mediante API REST |
| `app.md` | Aplicación consumidora de referencia |
| `snapshots.md` | Publicaciones históricas del padrón |

---

# Estado del desarrollo

| Etapa | Estado |
|--------|--------|
| Definición conceptual | ✔ Finalizada |
| Hallazgos | ✔ Finalizada |
| Decisiones de modelo | ✔ Finalizada |
| Metadatos | ✔ Finalizada |
| Diccionario de datos | ✔ Finalizada |
| Modelo lógico | ✔ Finalizada |
| Vista SQL | En desarrollo |
| Endpoint | Pendiente |
| Aplicación de referencia | Pendiente |
| Snapshots | Pendiente |

---

# MVP

El Producto 001 estará finalizado cuando un usuario pueda abrir un navegador y:

- consultar el padrón;
- filtrarlo;
- descargarlo;
- consumirlo mediante API;
- visualizarlo sobre un mapa.

La infraestructura necesaria para ello ya se encuentra implementada.

El trabajo restante consiste exclusivamente en completar el producto.

---

# Productos futuros

El Producto 001 constituye la base metodológica para los desarrollos posteriores de LocalAPI.

Entre los productos previstos se encuentran:

- Padrón de Ofertas Educativas.
- Padrón de Edificios.
- Productos territoriales.
- Productos estadísticos.

Cada nuevo producto reutilizará la misma metodología, modificando únicamente el modelo de información correspondiente a su dominio.

---

# Resultado esperado

Al finalizar el MVP, el Producto 001 reemplazará el proceso actual de construcción del Padrón de Establecimientos Educativos mediante un modelo de información documentado, reproducible y reutilizable.

Su desarrollo constituye la primera demostración práctica de la metodología propuesta por LocalAPI y servirá como referencia para la construcción de los productos que lo sucedan.