# 07. Endpoints

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Este documento describe los criterios utilizados por LocalAPI para publicar productos de información mediante APIs REST.

Los endpoints no constituyen el objetivo del desarrollo.

Constituyen uno de los mecanismos mediante los cuales un producto institucional puede ser consumido por aplicaciones, sistemas o usuarios.

---

# El endpoint no es el producto

En LocalAPI el desarrollo nunca comienza diseñando un endpoint.

El recorrido correcto es:

```
Necesidad

↓

Producto

↓

Modelo lógico

↓

Vista SQL

↓

Endpoint
```

Por este motivo, un endpoint representa la publicación de un modelo previamente diseñado y documentado.

Nunca constituye una implementación aislada.

---

# ¿Qué publica un endpoint?

Cada endpoint publica exactamente un producto de información.

No publica tablas.

No publica consultas.

No publica estructuras internas de las bases de datos.

Publica un modelo de información construido para resolver una necesidad concreta.

---

# Productos y endpoints

La relación entre productos y endpoints es directa.

| Producto | Endpoint |
|----------|----------|
| Producto 001 – Padrón de Establecimientos | `/padron_establecimientos` |
| Producto 002 – Padrón de Ofertas | `/padron_ofertas` |
| ... | ... |

Cada producto puede tener uno o más formatos de publicación.

El endpoint REST es uno de ellos.

---

# Origen de los endpoints

Todos los endpoints publicados por LocalAPI se generan automáticamente a partir de vistas SQL ubicadas dentro del esquema:

```
api
```

Cada vista constituye una representación pública del modelo de información.

PostgREST transforma dichas vistas en recursos REST sin necesidad de desarrollar una capa adicional de software.

---

# Principios de publicación

## Un endpoint por producto

Cada endpoint representa un único producto institucional.

No debe mezclar dominios funcionales diferentes.

---

## Modelo estable

La estructura del endpoint debe mantenerse estable entre versiones.

Los consumidores dependen del modelo publicado y no de las estructuras internas de las bases de datos.

---

## Ocultar la complejidad

Las relaciones entre múltiples bases de datos, las transformaciones y las reglas de integración permanecen encapsuladas dentro de la vista SQL.

El consumidor del endpoint accede únicamente al resultado integrado.

---

## Independencia de las fuentes

Los consumidores desconocen:

- tablas de origen;
- esquemas;
- relaciones internas;
- transformaciones realizadas;
- cantidad de bases utilizadas.

Toda esa complejidad pertenece a LocalAPI.

---

# Capacidades

Los endpoints publicados mediante PostgREST ofrecen automáticamente:

- consultas HTTP GET;
- filtros por atributos;
- ordenamiento;
- paginación;
- selección de columnas;
- respuestas JSON;
- documentación OpenAPI.

Estas capacidades son provistas por la infraestructura y no requieren desarrollo adicional.

---

# Versionado

El versionado corresponde al producto de información.

Cuando un cambio modifica el modelo publicado, deberá evaluarse la necesidad de generar una nueva versión del producto.

Las modificaciones internas de implementación que no alteren el modelo no requieren nuevos endpoints.

---

# Documentación

Cada producto documenta su endpoint dentro de su propia carpeta.

Por ejemplo:

```
productos/
└── 001_padron_establecimientos/
    └── endpoint.md
```

Ese documento describe:

- recurso publicado;
- parámetros disponibles;
- filtros;
- ordenamientos;
- ejemplos de uso;
- formatos de respuesta.

La documentación general de LocalAPI únicamente define las reglas comunes de publicación.

---

# El Producto 001

El primer endpoint desarrollado mediante LocalAPI publicará el:

**Producto 001 – Padrón de Establecimientos Educativos.**

Su implementación tendrá como objetivo demostrar el ciclo completo de construcción de un producto institucional:

- integración de múltiples fuentes;
- modelo lógico documentado;
- vista SQL;
- publicación automática mediante PostgREST;
- consumo desde una aplicación de referencia.

---

# Filosofía

En LocalAPI los endpoints no se diseñan de manera independiente.

Cada endpoint es la expresión pública de un producto de información previamente definido.

La calidad del endpoint depende de la calidad del modelo de información que representa.

Por ese motivo, el esfuerzo principal del laboratorio se concentra en comprender el problema, diseñar el producto y documentar el modelo.

La publicación REST constituye la última etapa del proceso.