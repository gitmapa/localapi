# Diccionario de datos

## Objetivo

Este documento define el esquema público del **Producto 001 – Padrón de Establecimientos Educativos**.

Su finalidad es describir cada uno de los atributos publicados por LocalAPI, independientemente de su implementación técnica.

El diccionario constituye el contrato funcional del producto y sirve como referencia para:

- construir la vista SQL;
- publicar el endpoint REST;
- desarrollar la aplicación consumidora;
- validar la correspondencia con el padrón oficial.

---

## Unidad de publicación

La unidad de publicación del Producto 001 es el **CUEANEXO**.

Cada registro representa una localización (sede o anexo) de un establecimiento educativo.

---

## Criterios generales

- La identidad educativa proviene del **Padrón Nacional**.
- La dirección postal proviene del **Padrón Nacional**.
- La información territorial y geográfica proviene de **UEICEE (RANIE)**.
- Los campos derivados son construidos por LocalAPI sin duplicar información de origen.
- Las transformaciones realizadas por LocalAPI tienen como objetivo normalizar la publicación y no modificar la información institucional.

---

## Diccionario de datos

| Orden | Columna Excel | Nombre API | Descripción | Fuente | Obligatoria | Observaciones |
|------:|---------------|------------|-------------|---------|-------------|---------------|
| 1 | estado_est | estado_est | Código del estado del establecimiento | padron_nacion | SI | 1=Activo, 2=Inactivo, 3=Baja, 4=Inactivo sin docentes |
| 2 | estado_est_desc | estado_est_desc | Descripción del estado del establecimiento | padron_nacion | SI | |
| 3 | sector | sector | Código del sector de gestión | padron_nacion | SI | |
| 4 | sector_desc | sector_desc | Descripción del sector de gestión | padron_nacion | SI | |
| 5 | cue | cue | Código Único de Establecimiento | padron_nacion | SI | |
| 6 | anexo | anexo | Código de anexo del establecimiento | padron_nacion | SI | |
| 7 | cueanexo | cueanexo | Identificador de la localización educativa | Derivado | SI | Construido mediante la concatenación de CUE + Anexo |
| 8 | cui | cui | Código Único de Infraestructura | padron_nacion | SI | Clave de integración con UEICEE |
| 9 | estado_loc | estado_loc | Código del estado de la localización | padron_nacion | SI | 1=Activo, 2=Inactivo, 3=Baja, 4=Inactivo sin docentes |
| 10 | estado_loc_desc | estado_loc_desc | Descripción del estado de la localización | padron_nacion | SI | |
| 11 | email | email | Correo electrónico institucional | padron_nacion | SI | |
| 12 | nombre_est | nombre_est | Nombre del establecimiento | padron_nacion | SI | |
| 13 | nombre_loc | nombre_loc | Nombre de la localización | padron_nacion | SI | |
| 14 | barrio | barrio | Barrio administrativo del edificio | ranie_app | SI | Información territorial provista por UEICEE |
| 15 | calle | calle | Calle del domicilio postal | padron_nacion | SI | |
| 16 | num | num | Altura del domicilio postal | padron_nacion | SI | |
| 17 | point_x | point_x | Coordenada X del edificio en GKBA | ranie_app | SI | Sistema oficial |
| 18 | point_y | point_y | Coordenada Y del edificio en GKBA | ranie_app | SI | Sistema oficial |
| 19 | latitud | latitud | Latitud del edificio en WGS84 | ranie_app | SI | Sistema de publicación |
| 20 | longitud | longitud | Longitud del edificio en WGS84 | ranie_app | SI | Sistema de publicación |
| 21 | de | de | Distrito Escolar del edificio | ranie_app | SI | Valor normalizado para publicación |
| 22 | nro | nro | Número de escuela | ranie_app | SI | Derivado del código jurisdiccional |
| 23 | comuna | comuna | Comuna del edificio | ranie_app | SI | Valor normalizado para publicación |
| 24 | mingob | mingob | Código de gestión ministerial | ranie_app | SI | Derivado del atributo "gestionado" |
| 25 | d_mingob | d_mingob | Descripción de la gestión ministerial | ranie_app | SI | Derivado del atributo "gestionado" |
| 26 | depfun | depfun | Código de dependencia funcional | — | NO | Excluido del Producto 001 |
| 27 | d_depfun | d_depfun | Descripción de dependencia funcional | ranie_app | NO | Evaluar incorporación en futuros productos |
| 28 | tipest | tipest | Código de tipo de establecimiento | — | NO | Excluido del Producto 001 |
| 29 | d_tipest | d_tipest | Descripción de tipo de establecimiento | ranie_app | NO | Evaluar incorporación en futuros productos |
| 30 | Oferta_CABA | Oferta_CABA | Descripción de las ofertas educativas | — | NO | Pertenece al Producto 002 – Padrón de Ofertas |
| 31 | Oferta_CABA_cod | Oferta_CABA_cod | Código de las ofertas educativas | — | NO | Pertenece al Producto 002 – Padrón de Ofertas |

---

## Transformaciones realizadas por LocalAPI

Durante la integración se realizan únicamente las siguientes transformaciones:

- Construcción del identificador **CUEANEXO** mediante la concatenación de **CUE + Anexo**.
- Normalización del Distrito Escolar a formato numérico de dos dígitos.
- Normalización de la Comuna a formato numérico de dos dígitos.
- Obtención del Número de Escuela a partir del código jurisdiccional.
- Derivación de los campos **mingob** y **d_mingob** a partir del atributo **gestionado** del edificio.

No se realizan modificaciones sobre los datos institucionales de origen.

---

## Principios de diseño aplicados

- La unidad de publicación es **CUEANEXO**.
- Cada atributo posee una única fuente de verdad.
- LocalAPI integra información; no administra ni replica procesos de carga.
- Las transformaciones son exclusivamente de publicación y normalización.
- Los atributos correspondientes a otros productos institucionales no forman parte del Producto 001.