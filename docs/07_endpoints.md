# 07. Endpoints

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Los endpoints constituyen la interfaz pública de LocalAPI.

Cada endpoint representa un recurso de información construido para responder una necesidad concreta de los usuarios.

Los endpoints no representan tablas.

Representan modelos de información.

---

# Principios

Cada endpoint debe cumplir los siguientes principios.

## Responder una necesidad

Un endpoint debe existir porque resuelve una consulta real.

Nunca se publica información únicamente porque se encuentra disponible en una base de datos.

---

## Ocultar la complejidad

El consumidor no necesita conocer:

- de qué base provienen los datos;
- cómo se relacionan las tablas;
- qué normalizaciones fueron necesarias;
- cómo se resolvieron inconsistencias.

Toda esa complejidad pertenece a LocalAPI.

---

## Mantener estabilidad

Las aplicaciones cliente dependen de los nombres publicados por la API.

La estructura de un endpoint debe modificarse únicamente cuando exista una justificación funcional.

---

## Publicar información útil

Cada campo publicado debe aportar valor.

No deben exponerse identificadores internos, estructuras técnicas o información irrelevante para el consumidor.

---

# Tipos de endpoints

En LocalAPI los recursos pueden clasificarse según su objetivo.

---

## Recursos de consulta

Devuelven información tabular.

Ejemplos:

- establecimientos;
- personas;
- edificios;
- organismos;
- localidades.

---

## Recursos geográficos

Devuelven información espacial.

Pueden incluir:

- coordenadas;
- geometrías;
- áreas;
- puntos;
- líneas.

Estos recursos están destinados principalmente a aplicaciones SIG y visualizadores cartográficos.

---

## Recursos de detalle

Devuelven toda la información asociada a un único elemento.

Ejemplo conceptual:

```
GET /v_cui_detalle?cui=eq.200187
```

Su objetivo es alimentar paneles de información o fichas descriptivas.

---

## Recursos auxiliares

Ofrecen información utilizada para construir interfaces.

Ejemplos:

- listados de provincias;
- departamentos;
- tipos;
- categorías;
- dominios.

---

# Convenciones

Se recomienda utilizar nombres simples.

Ejemplos:

```
v_establecimientos

v_edificios

v_personas

v_localidades
```

Evitar nombres que reflejen la implementación interna.

Por ejemplo:

```
v_join_edificios_padron_tmp
```

---

# Filtros

Siempre que sea posible, los endpoints deben permitir filtrar información mediante los mecanismos ofrecidos por PostgREST.

Ejemplos:

```
?cui=eq.200187
```

```
?provincia=eq.Buenos Aires
```

```
?limit=100
```

```
?select=cui,nombre
```

No deben desarrollarse mecanismos propios para tareas ya resueltas por PostgREST.

---

# Evolución

La incorporación de nuevos endpoints no requiere modificar aplicaciones existentes.

Cada nuevo recurso se publica mediante una nueva vista SQL dentro del schema:

```
api
```

Una vez creada y autorizada, PostgREST la incorpora automáticamente a la API.

---

# Endpoints actuales

La implementación inicial publica recursos orientados al dominio RANIE.

Entre ellos:

- establecimientos;
- edificios;
- localizaciones.

Estos recursos constituyen el punto de partida del proyecto y podrán ampliarse incorporando nuevas fuentes institucionales.

---

# Evolución esperada

A medida que LocalAPI incorpore nuevas bases de información, la API crecerá mediante nuevos recursos especializados.

Ejemplos posibles:

- establecimientos educativos;
- edificios;
- organismos;
- programas;
- personas;
- gobiernos locales;
- capas geográficas;
- estadísticas;
- indicadores.

Todos ellos compartirán la misma arquitectura de integración y publicación.

---

# Resultado esperado

Cada endpoint publicado por LocalAPI debe representar un recurso de información claro, estable y útil para las aplicaciones consumidoras, ocultando la complejidad de integración existente en las bases institucionales.