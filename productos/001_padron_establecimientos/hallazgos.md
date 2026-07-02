# Hallazgos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Documentar los principales hallazgos obtenidos durante el análisis del Producto 001.

Este documento registra conocimiento funcional descubierto durante el desarrollo y servirá como referencia para el diseño del modelo lógico y la implementación SQL.

Los hallazgos representan conocimiento adquirido.

No constituyen decisiones de diseño.

---

# Hallazgo 001

## Unidad educativa

El **CUE** identifica un establecimiento educativo.

Un establecimiento puede poseer uno o más anexos.

Los anexos pueden encontrarse ubicados en distintos edificios.

---

# Hallazgo 002

## Unidad de publicación

La unidad de publicación del producto es el **CUEANEXO**.

Cada registro publicado representa una localización de un establecimiento educativo.

Esta decisión coincide con la publicación oficial actualmente difundida por la UEICEE.

---

# Hallazgo 003

## Unidad edilicia

El **CUI** identifica un edificio.

Un edificio puede albergar uno o más establecimientos educativos.

Por lo tanto, la relación entre CUEANEXO y CUI es de muchos a uno.

---

# Hallazgo 004

## Relación entre CUEANEXO y CUI

La relación entre la identidad educativa (CUEANEXO) y la identidad edilicia (CUI) se encuentra en:

```
padron_nacion.public.domicilio.cui
```

Este campo constituye el vínculo principal entre las fuentes de información utilizadas por el Producto 001.

Su identificación permite integrar el Padrón Nacional con la información edilicia administrada por la UEICEE.

---

# Hallazgo 005

## Grano de las fuentes

Las fuentes utilizadas poseen distintas unidades de información.

| Fuente | Unidad |
|---------|--------|
| Padrón Nacional | Localización (CUE + Anexo) |
| UEICEE | Edificio (CUI) |

La integración del producto consiste en relacionar ambas unidades.

---

# Hallazgo 006

## Ubicación territorial

Cada edificio pertenece a una única:

- comuna;
- barrio;
- distrito escolar.

Estas variables son atributos del edificio y, por lo tanto, deben ser heredadas por cada CUEANEXO asociado.

---

# Hallazgo 007

## Direcciones

Un edificio puede poseer más de una dirección asociada.

Las distintas direcciones corresponden al mismo CUI.

La dirección postal publicada forma parte de la información administrativa del establecimiento y no modifica la identidad edilicia.

---

# Hallazgo 008

## La publicación oficial reúne múltiples dominios de información

Durante el análisis de la publicación institucional se observó que una misma planilla incorpora atributos pertenecientes a distintos dominios funcionales.

Entre ellos:

- identidad educativa;
- localización;
- infraestructura;
- ofertas educativas;
- dependencia funcional;
- tipologías institucionales.

La existencia de estos atributos en una misma publicación no implica que todos pertenezcan al mismo producto de información.

---

# Hallazgo 009

## El Producto 001 representa un subconjunto conceptual de la publicación oficial

El objetivo del Producto 001 no consiste en publicar todas las columnas presentes en la planilla institucional.

Su objetivo consiste en reconstruir el **Padrón de Establecimientos Educativos**.

Como consecuencia, algunos atributos presentes en la publicación fueron identificados como pertenecientes a futuros productos, particularmente al **Padrón de Ofertas Educativas**.

---

# Hallazgo 010

## La definición del producto precede a la implementación

Durante el desarrollo se comprobó que la implementación SQL no constituye el punto de partida adecuado.

El análisis resultó significativamente más consistente cuando el trabajo comenzó por:

- comprender el dominio;
- identificar la unidad de publicación;
- definir las fuentes de verdad;
- documentar los atributos;
- construir el modelo lógico.

La implementación pasó a ser una consecuencia del diseño.

---

# Hallazgo 011

## El Excel oficial constituye un mecanismo de validación

Inicialmente la publicación institucional fue utilizada como referencia para comprender el producto.

Una vez construido el modelo conceptual se observó que la planilla resulta más útil como mecanismo de validación que como especificación funcional.

El modelo del producto surge del análisis del dominio y de las responsabilidades institucionales.

La publicación oficial permite verificar que dicho modelo reproduce correctamente el resultado esperado.

---

# Hallazgo 012

## El diseño del Producto 001 constituye una metodología reutilizable

Durante el desarrollo se observó que gran parte del trabajo realizado no corresponde exclusivamente al Padrón de Establecimientos.

Las etapas recorridas:

- identificación de la necesidad;
- definición del producto;
- documentación;
- modelo lógico;
- diccionario de datos;
- implementación;
- validación;

constituyen un método aplicable a futuros productos desarrollados mediante LocalAPI.

---

# Hallazgo 013

## Los productos comparten un núcleo común de información

El análisis permitió identificar un conjunto importante de atributos reutilizables entre distintos productos institucionales.

Por ejemplo:

- identidad educativa;
- localización;
- infraestructura;
- información territorial;
- georreferencia.

Los futuros productos podrán reutilizar estos componentes incorporando únicamente los atributos propios de su dominio específico.

---

# Estado

Los hallazgos documentados hasta el momento permiten considerar finalizada la etapa de análisis conceptual del Producto 001.

Las etapas siguientes consisten en implementar la vista SQL, validar el resultado contra la publicación oficial y completar los mecanismos de publicación definidos para el MVP.