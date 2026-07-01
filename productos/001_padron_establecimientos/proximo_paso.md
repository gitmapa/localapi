# Próximo paso

> Documento transitorio de trabajo.
>
> Objetivo: retomar el desarrollo del Producto 001 exactamente desde el punto donde quedó.

---

# Estado actual

## Infraestructura

- PostgreSQL funcionando.
- Foreign Data Wrapper (FDW) configurado.
- PostgREST funcionando.
- Swagger UI funcionando.
- Repositorio documentado.

## Producto 001

Se encuentra definida la descripción conceptual del producto.

Documentación realizada:

- README.md
- metadatos.md
- hallazgos.md
- decisiones_modelo.md

---

# Hallazgos principales

Durante el análisis se identificaron los siguientes aspectos estructurales del producto.

## Unidad educativa

- CUE identifica un establecimiento educativo.
- Un establecimiento puede poseer uno o más anexos.

## Unidad de publicación

Cada registro representa un:

**CUE + Anexo**

(CUEANEXO)

## Unidad edilicia

El edificio se identifica mediante un:

**CUI**

Un edificio puede albergar varios establecimientos educativos.

## Integración

Se identificó el vínculo entre ambas fuentes.

```
padron_nacion.public.domicilio.cui
```

Este campo permite relacionar la identidad educativa con la identidad edilicia.

---

# Decisiones de modelo adoptadas

## Fuente de verdad

La información publicada deberá respetar las responsabilidades institucionales.

| Información | Fuente |
|-------------|--------|
| Identidad educativa | Padrón Nacional |
| Dirección postal | Padrón Nacional |
| Coordenadas | UEICEE |
| Barrio | UEICEE |
| Comuna | UEICEE |
| Distrito Escolar | UEICEE |

---

## Principio de integración

LocalAPI integra información.

No duplica procesos de administración.

Cada dato debe mantenerse únicamente en el sistema responsable de su actualización.

---

# Próxima etapa

A partir del próximo encuentro comenzará el diseño del modelo lógico del Producto 001.

El objetivo consiste en reconstruir completamente el proceso de generación de la publicación oficial.

No se implementará directamente una consulta SQL.

Primero se comprenderá completamente el modelo de información.

---

# Trabajo pendiente

## 1. Completar la consulta de origen

Finalizar el relevamiento de la consulta utilizada actualmente para generar la publicación institucional.

El objetivo no consiste en reutilizar dicha consulta.

Su objetivo es comprender:

- tablas utilizadas;
- relaciones;
- reglas de integración;
- campos calculados;
- transformaciones.

---

## 2. Construir el diccionario de datos

Para cada variable publicada documentar:

- nombre;
- descripción;
- tipo de dato;
- dominio;
- fuente institucional;
- tabla de origen;
- campo de origen;
- transformación aplicada;
- observaciones.

La hoja metodológica incluida en la publicación oficial constituye el punto de partida de este trabajo.

---

## 3. Diseñar el modelo lógico

Definir:

- entidades;
- relaciones;
- prioridades entre fuentes;
- reglas de integración;
- atributos heredados;
- campos calculados.

Todavía no se desarrollará SQL.

---

## 4. Implementar la vista

Una vez validado el modelo lógico comenzará la implementación de:

```
api.v_padron_establecimientos
```

Esta vista constituirá la base del primer endpoint desarrollado mediante LocalAPI.

---

# Objetivo inmediato

Obtener una vista integrada que reproduzca íntegramente la publicación oficial del Padrón de Establecimientos Educativos utilizando exclusivamente el modelo de información construido para LocalAPI.

---

# Regla de trabajo

El Producto 001 constituye el producto piloto del laboratorio.

Las decisiones metodológicas adoptadas durante su desarrollo servirán como patrón para los futuros productos construidos mediante LocalAPI.

No se desarrollarán nuevos productos hasta completar íntegramente el Producto 001.