# Vista SQL

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Este documento describe la implementación del **Producto 001 – Padrón de Establecimientos Educativos** mediante una vista SQL.

La vista constituye la materialización del modelo lógico documentado previamente.

No introduce nuevas reglas funcionales.

Su única responsabilidad consiste en integrar la información proveniente de las distintas fuentes y publicarla respetando el contrato definido por el diccionario de datos.

---

# Principios

La implementación de la vista SQL debe respetar los siguientes principios.

## El modelo precede a la implementación

Toda decisión funcional fue documentada previamente.

La vista SQL únicamente implementa dichas decisiones.

---

## Una única fuente de verdad

Cada atributo publicado proviene de un único sistema responsable.

La vista integra información.

No reemplaza procesos de carga.

---

## No duplicar responsabilidades

La vista consume información existente.

No genera tablas auxiliares para mantener datos duplicados.

---

## Reproducibilidad

La ejecución de la vista debe producir siempre el mismo resultado para un mismo estado de las bases de origen.

---

# Producto publicado

La vista publica el **Producto 001 – Padrón de Establecimientos Educativos**.

Unidad de publicación:

```
CUEANEXO
```

Cada registro representa una localización educativa.

---

# Fuentes utilizadas

## Padrón Nacional

Responsable de:

- identidad educativa;
- localización;
- dirección postal;
- CUI.

---

## UEICEE

Responsable de:

- coordenadas;
- barrio;
- comuna;
- distrito escolar;
- gestión ministerial.

---

# Integración

La integración entre ambas fuentes se realiza mediante el atributo:

```
CUI
```

El vínculo corresponde a:

```
padron_nacion.public.domicilio.cui
```

↓

```
ranie.edificios.cui
```

Este constituye el único punto de integración entre ambos dominios.

---

# Dominios publicados

La vista integra cinco dominios funcionales.

| Dominio | Fuente |
|----------|--------|
| Identidad educativa | Padrón Nacional |
| Localización postal | Padrón Nacional |
| Identidad edilicia | Padrón Nacional |
| Información territorial | UEICEE |
| Información geográfica | UEICEE |

---

# Transformaciones

Durante la implementación únicamente se permiten transformaciones documentadas.

## Construcción de CUEANEXO

```
CUE + Anexo
```

---

## Distrito Escolar

Conversión de numeración romana al formato publicado de dos dígitos.

Ejemplo:

```
Distrito Escolar IX

↓

09
```

---

## Comuna

Normalización al formato:

```
01
02
03
...
15
```

---

## Número de escuela

Obtención a partir del código jurisdiccional.

---

## Gestión ministerial

Derivación de los campos:

- mingob
- d_mingob

a partir del atributo:

```
gestionado
```

---

# Orden de columnas

La vista deberá respetar exactamente el orden definido en:

```
diccionario_de_datos.md
```

Este orden constituye el contrato público del producto.

---

# Filtros

La vista publicará únicamente:

- establecimientos activos;
- localizaciones activas.

Los criterios de filtrado deberán mantenerse documentados y corresponder con la publicación oficial.

---

# Ordenamiento

La vista deberá generar resultados determinísticos.

El ordenamiento principal será:

```
CUE

↓

Anexo
```

En caso de ser necesario podrán incorporarse criterios secundarios para garantizar estabilidad.

---

# Exclusiones

La vista no publicará atributos pertenecientes a otros productos.

Entre ellos:

- dependencia funcional;
- tipo de establecimiento;
- ofertas educativas.

Su implementación corresponderá a futuros productos.

---

# Rendimiento

La vista deberá privilegiar:

- simplicidad;
- legibilidad;
- trazabilidad.

Las optimizaciones sólo deberán incorporarse cuando exista una necesidad comprobada.

El MVP prioriza claridad sobre microoptimizaciones.

---

# Validación

La vista será considerada correcta cuando reproduzca exactamente la publicación oficial.

La validación comprenderá:

- cantidad de registros;
- estructura;
- nombres de columnas;
- orden de columnas;
- contenido;
- transformaciones.

La publicación oficial constituye el mecanismo de validación del resultado.

---

# Publicación

Una vez validada, la vista será publicada mediante PostgREST.

No se desarrollarán capas intermedias.

La publicación REST será generada automáticamente a partir de la vista.

---

# Implementación

La implementación física utilizará el esquema:

```
api
```

Nombre previsto de la vista:

```
api.padron_establecimientos
```

Este nombre constituye el recurso público que será expuesto por PostgREST.

---

# Dependencias

La vista depende de:

- Padrón Nacional.
- UEICEE.
- postgres_fdw.
- Diccionario de datos.
- Modelo lógico.

Cualquier modificación en estas dependencias deberá analizarse antes de modificar la implementación.

---

# Resultado esperado

La implementación deberá producir una vista SQL que:

- reproduzca el Padrón de Establecimientos Educativos;
- respete el modelo lógico;
- cumpla el diccionario de datos;
- mantenga una única fuente de verdad para cada atributo;
- pueda publicarse directamente mediante PostgREST;
- sirva como base para la aplicación de referencia y para los futuros snapshots del producto.

La vista constituye el primer artefacto técnico derivado directamente del modelo de información documentado para el Producto 001.