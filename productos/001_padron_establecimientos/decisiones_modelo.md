# Decisiones de modelo

> Producto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Registrar las decisiones de diseño adoptadas durante la construcción del Producto 001.

Estas decisiones forman parte del modelo de información y deberán respetarse durante la implementación.

---

# Decisión 001

## Fuente de verdad de la identidad educativa

Toda la información correspondiente a la identidad educativa del establecimiento proviene del Padrón Nacional.

Entre otros:

- CUE;
- Anexo;
- CUEANEXO;
- Nombre del establecimiento;
- Nombre de la localización;
- Estado;
- Sector;
- Email.

---

# Decisión 002

## Fuente de verdad de la identidad edilicia

Toda la información correspondiente a la ubicación territorial y geográfica del edificio proviene de la UEICEE.

Entre otros:

- coordenadas;
- comuna;
- barrio;
- distrito escolar.

---

# Decisión 003

## Dirección postal

Los campos:

- calle;
- número.

serán publicados utilizando la información proveniente del Padrón Nacional.

La UEICEE actualiza estas direcciones dentro del sistema que administra el Padrón Nacional.

No corresponde duplicar este proceso dentro de la infraestructura administrada por MAPA.

---

# Decisión 004

## No duplicación de procesos

LocalAPI no reemplaza procesos de carga existentes.

Cuando una fuente institucional administra correctamente un conjunto de datos, dichos datos deberán consumirse directamente desde esa fuente.

La integración tiene como objetivo evitar duplicaciones y reducir la posibilidad de errores humanos.

---

# Decisión 005

## Integración de fuentes

La integración del Producto 001 se realiza utilizando:

- identidad educativa desde el Padrón Nacional;
- identidad edilicia desde la UEICEE.

El vínculo entre ambas fuentes se establece mediante el CUI.

---

# Decisión 006

## Herencia de atributos territoriales

Cada CUEANEXO hereda del edificio asociado (CUI):

- comuna;
- barrio;
- distrito escolar;
- coordenadas.

Estos atributos no dependen del establecimiento sino del edificio donde funciona.

---

# Decisión 007

## Publicación oficial

El objetivo del Producto 001 consiste en reconstruir íntegramente la publicación oficial del Padrón de Establecimientos Educativos utilizando un modelo de información integrado.

La API constituye uno de los formatos posibles de publicación.

El producto no se diseña a partir de una consulta SQL.

La consulta SQL deberá implementarse a partir del modelo de información definido.

---

# Decisión 008

## Evolución del proceso

Históricamente la consistencia entre el Padrón Nacional y la información territorial administrada por MAPA se verificaba mediante comparaciones manuales entre planillas y archivos geográficos.

La implementación del Producto 001 reemplaza ese proceso por una integración directa entre bases de datos, reduciendo tareas manuales y eliminando la necesidad de mantener información duplicada.

---

# Estado

Las decisiones documentadas hasta el momento constituyen las reglas funcionales que deberán respetarse durante la construcción del modelo lógico y la implementación del Producto 001.