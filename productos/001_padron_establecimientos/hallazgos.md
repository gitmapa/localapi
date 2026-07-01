# Hallazgos

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Documentar los principales hallazgos obtenidos durante el análisis del Producto 001.

Este documento registra conocimiento funcional descubierto durante el desarrollo y servirá como referencia para el diseño del modelo lógico y la implementación SQL.

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

# Estado

Los hallazgos documentados hasta el momento permiten iniciar el diseño del modelo lógico del Producto 001.