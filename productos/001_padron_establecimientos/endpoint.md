# Endpoint

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Este documento define la publicación REST del **Producto 001 – Padrón de Establecimientos Educativos**.

El endpoint constituye el mecanismo mediante el cual el modelo de información documentado podrá ser consumido por aplicaciones, sistemas y usuarios.

No define el producto.

Publica el producto.

---

# Producto publicado

Producto:

**001 – Padrón de Establecimientos Educativos**

Unidad de publicación:

```
CUEANEXO
```

Cada recurso representa una localización educativa enriquecida con información territorial y geográfica.

---

# Implementación

La publicación se realizará mediante:

- PostgreSQL
- PostgREST

No se desarrollará una capa adicional de software.

El endpoint será generado automáticamente a partir de una vista SQL ubicada en el esquema:

```
api
```

---

# Recurso

Nombre previsto:

```
/padron_establecimientos
```

Vista SQL asociada:

```
api.padron_establecimientos
```

Este recurso constituye la publicación oficial del Producto 001.

---

# Formato

El endpoint publicará información en formato:

```
JSON
```

La estructura de cada registro corresponderá exactamente al contrato definido en:

```
diccionario_de_datos.md
```

---

# Campos publicados

El endpoint publicará exclusivamente los atributos definidos para el Producto 001.

Entre ellos:

- estado_est
- estado_est_desc
- sector
- sector_desc
- cue
- anexo
- cueanexo
- cui
- estado_loc
- estado_loc_desc
- email
- nombre_est
- nombre_loc
- barrio
- calle
- num
- point_x
- point_y
- latitud
- longitud
- de
- nro
- comuna
- mingob
- d_mingob

No se publicarán atributos correspondientes a otros productos.

---

# Consulta completa

Ejemplo conceptual:

```
GET

/padron_establecimientos
```

Devuelve la totalidad del padrón.

---

# Consulta por CUE

Ejemplo:

```
GET

/padron_establecimientos?cue=eq.1234567
```

Devuelve todas las localizaciones correspondientes al establecimiento.

---

# Consulta por CUEANEXO

Ejemplo:

```
GET

/padron_establecimientos?cueanexo=eq.123456700
```

Devuelve una única localización.

---

# Consulta por CUI

Ejemplo:

```
GET

/padron_establecimientos?cui=eq.200984
```

Devuelve todas las localizaciones que funcionan en un mismo edificio.

---

# Consulta por Comuna

Ejemplo:

```
GET

/padron_establecimientos?comuna=eq.05
```

---

# Consulta por Barrio

Ejemplo:

```
GET

/padron_establecimientos?barrio=eq.PALERMO
```

---

# Ordenamiento

El endpoint permitirá utilizar los mecanismos estándar de PostgREST.

Ejemplo:

```
?order=cue,anexo
```

---

# Selección de columnas

Ejemplo:

```
?select=cue,nombre_est,cui
```

---

# Paginación

El endpoint utilizará la paginación provista por PostgREST.

No se implementarán mecanismos específicos para el Producto 001.

---

# Filtrado

El endpoint permitirá utilizar los operadores estándar de PostgREST.

Entre ellos:

- eq
- neq
- lt
- lte
- gt
- gte
- like
- ilike
- in
- is

No se implementarán operadores específicos.

---

# Orden de las columnas

El orden publicado corresponderá exactamente al definido en:

```
diccionario_de_datos.md
```

---

# Versionado

El endpoint representa una versión del Producto 001.

Mientras el modelo de información permanezca estable, el endpoint conservará el mismo recurso.

Las modificaciones internas de implementación no alterarán la interfaz pública.

---

# Documentación

La documentación OpenAPI será generada automáticamente por PostgREST.

Swagger UI permitirá:

- explorar el recurso;
- ejecutar consultas;
- visualizar respuestas;
- validar filtros.

No se desarrollará documentación duplicada.

---

# Consumo

El endpoint constituye el punto de acceso para:

- aplicación de referencia;
- mapas;
- exportaciones;
- integraciones;
- consultas institucionales.

Todas las aplicaciones consumirán el mismo recurso.

---

# Seguridad

Durante el MVP el endpoint será de lectura.

No permitirá:

- inserciones;
- modificaciones;
- eliminaciones.

La administración de la información continuará realizándose en los sistemas responsables de cada fuente de datos.

---

# Relación con el modelo

El endpoint publica directamente la vista SQL.

No incorpora:

- lógica de negocio;
- transformaciones;
- validaciones funcionales.

Todas esas responsabilidades pertenecen al modelo implementado en la base de datos.

---

# Validación

El endpoint será considerado correcto cuando:

- publique exactamente el contenido de la vista SQL;
- respete el diccionario de datos;
- reproduzca la publicación oficial del padrón;
- mantenga la unidad de publicación definida para el Producto 001.

---

# Resultado esperado

El endpoint permitirá que cualquier consumidor pueda acceder al Padrón de Establecimientos Educativos mediante una interfaz REST estandarizada, sin necesidad de conocer la estructura de las bases de datos, las relaciones entre fuentes o las reglas de integración implementadas por LocalAPI.

El endpoint constituye el mecanismo oficial de publicación del Producto 001 y el punto de acceso utilizado por todas las aplicaciones desarrolladas sobre este producto.