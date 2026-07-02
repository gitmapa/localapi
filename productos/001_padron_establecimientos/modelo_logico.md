# Modelo lógico

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Definir el modelo conceptual del **Producto 001 – Padrón de Establecimientos Educativos**.

Este documento describe las entidades involucradas, sus relaciones, las responsabilidades institucionales y las reglas de integración que permiten construir el producto, independientemente de su implementación física.

El modelo lógico constituye la referencia funcional sobre la cual se implementará la vista SQL.

---

# Alcance

El Producto 001 publica exclusivamente el **Padrón de Establecimientos Educativos**.

Su objetivo consiste en integrar información educativa, edilicia, territorial y geográfica para construir una representación única de cada localización educativa.

No forman parte del modelo:

- ofertas educativas;
- dependencia funcional;
- tipologías institucionales;
- indicadores;
- estadísticas.

Estos dominios serán desarrollados como productos independientes.

---

# Unidad de publicación

La unidad de publicación es el **CUEANEXO**.

Cada registro representa una localización (sede o anexo) perteneciente a un establecimiento educativo.

Toda la información publicada se organiza alrededor de esta entidad.

---

# Entidades

El modelo se construye a partir de tres entidades principales.

---

## Establecimiento

Representa la unidad institucional de gestión educativa.

### Identificador

- CUE

### Atributos principales

- estado del establecimiento;
- sector de gestión;
- nombre.

### Fuente de verdad

Padrón Nacional.

---

## Localización

Representa la sede o anexo donde funciona un establecimiento.

### Identificador

- CUEANEXO

### Construcción

```
CUE + Anexo
```

### Atributos principales

- nombre de la localización;
- dirección postal;
- correo electrónico;
- estado de la localización.

### Fuente de verdad

Padrón Nacional.

---

## Edificio

Representa la infraestructura física donde funcionan una o más localizaciones.

### Identificador

- CUI

### Atributos principales

- barrio;
- comuna;
- distrito escolar;
- coordenadas;
- gestión ministerial.

### Fuente de verdad

UEICEE.

---

# Relaciones

## Establecimiento → Localización

Un establecimiento puede funcionar en una o más localizaciones.

```
Establecimiento (CUE)

        1
        │
        │
        └──────────── N

          Localización (CUEANEXO)
```

---

## Edificio → Localización

Un edificio puede contener una o más localizaciones.

Cada localización pertenece a un único edificio.

```
Edificio (CUI)

      1
      │
      │
      └──────────── N

        Localización (CUEANEXO)
```

---

# Integración

El modelo integra dos dominios institucionales.

```
Padrón Nacional
        │
        │
        │   CUI
        │──────────────┐
                       │
                       ▼
                  UEICEE
```

La integración se realiza mediante el atributo:

```
padron_nacion.public.domicilio.cui
```

que referencia al mismo edificio identificado por la UEICEE.

Este constituye el principal hallazgo estructural del Producto 001.

---

# Herencia de atributos

El edificio constituye la fuente de la información territorial y geográfica.

Por ese motivo, cada CUEANEXO hereda del edificio asociado:

- barrio;
- comuna;
- distrito escolar;
- coordenadas GKBA;
- coordenadas WGS84;
- gestión ministerial.

Estos atributos no dependen del establecimiento sino del edificio donde desarrolla sus actividades.

---

# Dominios funcionales

Los atributos publicados pueden agruparse en cinco dominios.

## Identidad educativa

Fuente:

Padrón Nacional.

Incluye:

- estado;
- sector;
- CUE;
- anexo;
- CUEANEXO;
- nombre.

---

## Localización postal

Fuente:

Padrón Nacional.

Incluye:

- calle;
- número;
- correo electrónico.

---

## Identidad edilicia

Fuente:

Padrón Nacional.

Incluye:

- CUI.

Este atributo constituye el vínculo entre ambos sistemas.

---

## Información territorial

Fuente:

UEICEE.

Incluye:

- barrio;
- comuna;
- distrito escolar;
- gestión ministerial.

---

## Información geográfica

Fuente:

UEICEE.

Incluye:

- coordenadas GKBA;
- coordenadas WGS84.

---

# Transformaciones

El modelo contempla únicamente transformaciones necesarias para la publicación.

Entre ellas:

- construcción del identificador CUEANEXO;
- normalización del Distrito Escolar;
- normalización de la Comuna;
- obtención del Número de Escuela;
- construcción de los atributos de gestión ministerial.

Estas transformaciones no alteran el significado institucional de los datos.

---

# Exclusiones

Durante el análisis se identificaron atributos pertenecientes a otros dominios funcionales.

Entre ellos:

- Oferta educativa.
- Dependencia funcional.
- Tipo de establecimiento.

Estos atributos no forman parte del Producto 001.

Su incorporación dará origen a nuevos productos desarrollados sobre la misma metodología.

---

# Resultado

El modelo lógico organiza el Producto 001 alrededor de una única unidad de publicación: el **CUEANEXO**.

Sobre esta entidad convergen:

- la identidad educativa;
- la identidad edilicia;
- la información territorial;
- la información geográfica.

Cada atributo conserva una única fuente de verdad y las relaciones entre sistemas permanecen encapsuladas dentro del modelo de integración.

---

# Implementación

La implementación del Producto 001 deberá respetar íntegramente este modelo.

La vista SQL, el endpoint REST y las aplicaciones consumidoras constituyen implementaciones de este diseño y no deberán introducir nuevas reglas funcionales.

Toda modificación del modelo deberá documentarse previamente antes de reflejarse en la implementación técnica.