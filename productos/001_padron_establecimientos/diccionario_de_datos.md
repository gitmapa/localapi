# Diccionario de datos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Este documento define el esquema público del **Producto 001 – Padrón de Establecimientos Educativos**.

Su finalidad es describir cada uno de los atributos publicados por LocalAPI, independientemente de su implementación técnica.

El diccionario constituye el contrato funcional del producto y sirve como referencia para:

- construir la vista SQL;
- publicar el endpoint REST;
- desarrollar la aplicación consumidora;
- validar la correspondencia con la publicación oficial.

---

# Alcance

El Producto 001 publica exclusivamente la información correspondiente al **Padrón de Establecimientos Educativos**.

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
- estadísticas.

Estos dominios darán origen a productos específicos en futuras etapas del laboratorio.

---

# Unidad de publicación

La unidad de publicación del Producto 001 es el **CUEANEXO**.

Cada registro representa una localización (sede o anexo) perteneciente a un establecimiento educativo.

Todos los atributos publicados se organizan alrededor de esta entidad.

---

# Dominios funcionales

Los atributos publicados se agrupan en los siguientes dominios.

| Dominio | Responsable |
|----------|-------------|
| Identidad educativa | Padrón Nacional |
| Localización postal | Padrón Nacional |
| Identidad edilicia | Padrón Nacional (CUI) |
| Información territorial | UEICEE |
| Información geográfica | UEICEE |
| Campos derivados | LocalAPI |

---

# Diccionario de datos

| Orden | Columna Excel | Nombre API | Descripción | Fuente | Publicado | Observaciones |
|------:|---------------|------------|-------------|---------|-----------|---------------|
| 1 | estado_est | estado_est | Código del estado del establecimiento | Padrón Nacional | SI | 1=Activo, 2=Inactivo, 3=Baja, 4=Inactivo sin docentes |
| 2 | estado_est_desc | estado_est_desc | Descripción del estado del establecimiento | Padrón Nacional | SI | |
| 3 | sector | sector | Código del sector de gestión | Padrón Nacional | SI | |
| 4 | sector_desc | sector_desc | Descripción del sector de gestión | Padrón Nacional | SI | |
| 5 | cue | cue | Código Único de Establecimiento | Padrón Nacional | SI | |
| 6 | anexo | anexo | Código de anexo del establecimiento | Padrón Nacional | SI | |
| 7 | cueanexo | cueanexo | Identificador de la localización educativa | Derivado | SI | Construido mediante la concatenación de CUE + Anexo |
| 8 | cui | cui | Código Único de Infraestructura | Padrón Nacional | SI | Clave de integración con UEICEE |
| 9 | estado_loc | estado_loc | Código del estado de la localización | Padrón Nacional | SI | 1=Activo, 2=Inactivo, 3=Baja, 4=Inactivo sin docentes |
| 10 | estado_loc_desc | estado_loc_desc | Descripción del estado de la localización | Padrón Nacional | SI | |
| 11 | email | email | Correo electrónico institucional | Padrón Nacional | SI | |
| 12 | nombre_est | nombre_est | Nombre del establecimiento | Padrón Nacional | SI | |
| 13 | nombre_loc | nombre_loc | Nombre de la localización | Padrón Nacional | SI | |
| 14 | barrio | barrio | Barrio administrativo del edificio | UEICEE | SI | Información territorial heredada del edificio |
| 15 | calle | calle | Calle del domicilio postal | Padrón Nacional | SI | |
| 16 | num | num | Altura del domicilio postal | Padrón Nacional | SI | |
| 17 | point_x | point_x | Coordenada X del edificio en GKBA | UEICEE | SI | Sistema oficial |
| 18 | point_y | point_y | Coordenada Y del edificio en GKBA | UEICEE | SI | Sistema oficial |
| 19 | latitud | latitud | Latitud del edificio en WGS84 | UEICEE | SI | Sistema de publicación |
| 20 | longitud | longitud | Longitud del edificio en WGS84 | UEICEE | SI | Sistema de publicación |
| 21 | de | de | Distrito Escolar del edificio | UEICEE | SI | Valor normalizado para publicación |
| 22 | nro | nro | Número de escuela | UEICEE | SI | Derivado del código jurisdiccional |
| 23 | comuna | comuna | Comuna del edificio | UEICEE | SI | Valor normalizado para publicación |
| 24 | mingob | mingob | Código de gestión ministerial | UEICEE | SI | Derivado del atributo `gestionado` |
| 25 | d_mingob | d_mingob | Descripción de la gestión ministerial | UEICEE | SI | Derivado del atributo `gestionado` |

---

# Campos excluidos

Los siguientes atributos fueron identificados durante el análisis de la publicación institucional, pero no forman parte del alcance del Producto 001.

| Campo | Motivo |
|--------|--------|
| depfun | No pertenece al Producto 001. |
| d_depfun | No pertenece al Producto 001. |
| tipest | No pertenece al Producto 001. |
| d_tipest | No pertenece al Producto 001. |
| Oferta_CABA | Pertenece al futuro Producto 002 – Padrón de Ofertas Educativas. |
| Oferta_CABA_cod | Pertenece al futuro Producto 002 – Padrón de Ofertas Educativas. |

La exclusión de estos campos no implica que carezcan de valor institucional.

Simplemente pertenecen a otro dominio funcional y deberán documentarse dentro de los productos correspondientes.

---

# Transformaciones realizadas por LocalAPI

Durante la integración únicamente se realizan transformaciones destinadas a normalizar la publicación.

Entre ellas:

- construcción del identificador **CUEANEXO** mediante la concatenación de **CUE + Anexo**;
- normalización del Distrito Escolar a formato numérico de dos dígitos;
- normalización de la Comuna a formato numérico de dos dígitos;
- obtención del Número de Escuela a partir del código jurisdiccional;
- construcción de los campos **mingob** y **d_mingob** a partir del atributo **gestionado**;
- adaptación de formatos para garantizar consistencia entre las distintas fuentes.

Ninguna transformación modifica el significado institucional de la información.

---

# Fuentes de verdad

Cada atributo publicado posee una única fuente de verdad.

| Dominio | Fuente de verdad |
|----------|------------------|
| Identidad educativa | Padrón Nacional |
| Dirección postal | Padrón Nacional |
| Identidad edilicia (CUI) | Padrón Nacional |
| Información territorial | UEICEE |
| Información geográfica | UEICEE |
| Campos derivados | LocalAPI |

Este criterio evita duplicaciones y mantiene claramente definidas las responsabilidades institucionales.

---

# Principios de diseño

Durante la construcción del diccionario se aplicaron los siguientes principios.

- La unidad de publicación es **CUEANEXO**.
- Cada atributo posee una única fuente de verdad.
- LocalAPI integra información; no administra datos.
- Las transformaciones responden únicamente a necesidades de publicación.
- El modelo de información precede a la implementación SQL.
- La publicación oficial constituye el mecanismo de validación del producto.
- Los dominios funcionales independientes se implementan como productos distintos.

---

# Resultado

El presente diccionario define el contrato público del Producto 001.

Toda implementación SQL, endpoint REST o aplicación consumidora deberá ajustarse a las definiciones aquí documentadas.

Cualquier modificación del modelo deberá reflejarse previamente en este documento antes de ser implementada en la infraestructura de LocalAPI.