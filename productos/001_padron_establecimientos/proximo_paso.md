# Próximo paso

> Documento transitorio de trabajo.
>
> Objetivo: retomar el desarrollo del Producto 001 exactamente desde el punto donde quedó.

---

# Estado actual

## Infraestructura

- PostgreSQL funcionando.
- postgres_fdw configurado.
- PostgREST funcionando.
- Swagger funcionando.
- Repositorio documentado.

## Producto

Se encuentra definida la descripción conceptual del producto:

**Padrón de Establecimientos Educativos**

La documentación inicial ya fue creada.

---

# Objetivo de la próxima etapa

Antes de escribir la primera vista SQL se documentará completamente el producto.

El objetivo es conocer el origen, significado y tratamiento de cada dato publicado.

La implementación deberá surgir de esa documentación y no al revés.

---

# Principio metodológico

En LocalAPI ningún producto se considera terminado si únicamente publica datos.

Todo producto deberá incluir:

- documentación conceptual;
- metadatos;
- diccionario de datos;
- modelo lógico;
- implementación SQL;
- endpoint;
- aplicación de referencia.

La documentación forma parte del producto.

No constituye documentación adicional.

---

# Trabajo a realizar

## 1. Analizar la publicación oficial

Tomar como referencia el archivo oficial publicado por UEICEE.

Analizar columna por columna.

No escribir SQL.

---

## 2. Construir los metadatos

Definir la información descriptiva del producto.

Como mínimo:

- nombre;
- descripción;
- organismo responsable;
- área responsable;
- frecuencia de actualización;
- frecuencia de publicación;
- unidad de publicación;
- cobertura geográfica;
- formato(s) de publicación;
- licencia;
- versión;
- fecha de creación;
- fecha de actualización;
- fuente(s) de información;
- observaciones metodológicas.

Este documento permitirá comprender el producto sin necesidad de conocer la implementación.

---

## 3. Construir el diccionario de datos

Para cada campo publicado documentar:

- nombre del campo;
- descripción;
- tipo de dato;
- dominio o catálogo (si corresponde);
- fuente oficial;
- tabla de origen;
- campo de origen;
- transformación aplicada;
- observaciones.

No importa todavía cómo se implementará.

Importa conocer exactamente de dónde proviene cada dato.

---

## 4. Detectar reglas de integración

Durante la construcción del diccionario identificar:

- joins necesarios;
- prioridades entre fuentes;
- reglas de resolución de conflictos;
- campos calculados;
- campos derivados;
- reglas metodológicas propias de MAPA.

Estas reglas formarán parte del modelo lógico.

---

## Resultado esperado

Al finalizar esta etapa deberá ser posible responder, para cualquier columna publicada:

- qué significa;
- quién es responsable del dato;
- de dónde proviene;
- cómo se obtiene;
- por qué forma parte del producto.

Una vez completado este trabajo comenzará la implementación SQL.

---

# Regla de trabajo

Todavía no se desarrollarán:

- vistas;
- endpoints;
- consultas SQL;
- aplicación PHP.

La prioridad absoluta es comprender completamente el producto antes de implementarlo.

El Producto 001 será el patrón metodológico que utilizarán los futuros productos desarrollados mediante LocalAPI.