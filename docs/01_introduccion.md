# 01. Introducción

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# ¿Por qué existe LocalAPI?

En los organismos públicos la información suele encontrarse distribuida entre múltiples sistemas, desarrollados por distintas áreas y con responsabilidades específicas.

Cada uno de estos sistemas administra correctamente su propio dominio de información, pero los productos institucionales que utilizan los usuarios suelen requerir integrar datos provenientes de varias fuentes.

Tradicionalmente esta integración se resuelve mediante:

- consultas SQL complejas;
- exportaciones a planillas de cálculo;
- procesos manuales de consolidación;
- desarrollos específicos para cada aplicación.

Estos mecanismos suelen ser difíciles de mantener, difíciles de documentar y poco reutilizables.

LocalAPI surge para abordar ese problema.

---

# ¿Qué es LocalAPI?

LocalAPI es un laboratorio para diseñar, integrar y publicar productos de información institucionales.

Su objetivo consiste en transformar información distribuida en distintos sistemas en productos documentados, reutilizables y fácilmente consumibles por personas y aplicaciones.

Para ello utiliza una arquitectura basada en PostgreSQL, PostgreSQL Foreign Data Wrapper (FDW) y PostgREST, evitando desarrollar capas adicionales de software cuando no son necesarias.

---

# Qué problema resuelve

LocalAPI desacopla los productos institucionales de los sistemas que administran los datos.

En lugar de construir aplicaciones que consultan directamente múltiples bases de datos, LocalAPI integra esas fuentes mediante un modelo de información único y publica dicho modelo como un producto reutilizable.

De esta manera:

- cada organismo continúa administrando sus propios datos;
- las responsabilidades institucionales permanecen claramente definidas;
- los consumidores acceden a un único modelo de información consistente.

---

# Qué no es LocalAPI

LocalAPI no reemplaza los sistemas institucionales existentes.

Tampoco administra información propia.

Su función consiste exclusivamente en:

- integrar información;
- construir modelos de información;
- publicar productos institucionales.

La administración y actualización de los datos continúa siendo responsabilidad de cada sistema de origen.

---

# Filosofía

El desarrollo en LocalAPI parte de una necesidad concreta.

No comienza escribiendo consultas SQL.

No comienza diseñando endpoints.

No comienza desarrollando aplicaciones.

El proceso comienza identificando qué producto necesita el usuario.

A partir de esa necesidad se construye un modelo de información que posteriormente podrá publicarse mediante distintos mecanismos.

La API constituye uno de ellos.

---

# Principios

El laboratorio se apoya sobre algunos principios fundamentales.

## Una única fuente de verdad

Cada atributo publicado posee un único sistema responsable de su administración.

---

## No duplicar responsabilidades

LocalAPI reutiliza la información administrada por otros sistemas.

No replica procesos de carga ni genera nuevas responsabilidades de mantenimiento.

---

## El modelo precede a la implementación

Antes de escribir una vista SQL es necesario comprender completamente el producto que se desea construir.

El modelo lógico constituye el verdadero diseño del producto.

---

## La API es una consecuencia

Una vez construido el modelo de información, la publicación mediante PostgREST resulta inmediata.

La API no constituye el objetivo del proyecto.

Constituye uno de sus mecanismos de publicación.

---

# Método

Todos los productos desarrollados mediante LocalAPI siguen el mismo proceso.

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

Validación contra publicación oficial
```

Cada etapa documenta decisiones que serán reutilizadas por los productos posteriores.

---

# MVP

La estrategia de desarrollo se basa en la construcción de Productos Mínimos Viables (MVP).

Cada MVP debe demostrar que una necesidad institucional puede resolverse mediante un modelo de información claro, documentado y reutilizable.

El primer MVP desarrollado en LocalAPI corresponde al:

**Producto 001 – Padrón de Establecimientos Educativos.**

Su objetivo consiste en demostrar el ciclo completo de construcción de un producto institucional, desde la integración de datos hasta una aplicación consumidora.

---

# Evolución

Una vez consolidado el primer producto, la misma metodología podrá aplicarse para construir nuevos productos de información.

La infraestructura permanecerá estable.

Lo que evolucionará serán los modelos de información construidos sobre ella.

De esta manera, cada nuevo producto ampliará el conocimiento acumulado por el laboratorio sin modificar los principios que dieron origen a LocalAPI.