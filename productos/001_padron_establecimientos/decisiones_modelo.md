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

# Decisión 009

## La unidad de publicación es CUEANEXO

El Producto 001 publica una única entidad.

Cada registro representa una localización de un establecimiento educativo identificada mediante la combinación:

- CUE;
- Anexo.

Todos los atributos publicados se organizan alrededor de esa unidad.

---

# Decisión 010

## Cada atributo posee una única fuente de verdad

Antes de incorporar un atributo al modelo debe identificarse el organismo responsable de administrarlo.

No se admiten atributos mantenidos simultáneamente por distintas fuentes.

Cuando exista más de una fuente para un mismo dato, el modelo deberá seleccionar una única fuente de verdad.

---

# Decisión 011

## LocalAPI publica productos, no estructuras internas

Las tablas, relaciones y consultas utilizadas para integrar la información constituyen detalles de implementación.

El modelo publicado representa un producto de información diseñado para resolver una necesidad concreta.

Las estructuras internas de las bases de datos no condicionan el diseño del producto.

---

# Decisión 012

## El modelo precede a la implementación

La implementación SQL no constituye una etapa de análisis.

Antes de desarrollar una vista deben encontrarse documentados:

- el objetivo del producto;
- la unidad de publicación;
- las fuentes de verdad;
- los hallazgos;
- las decisiones de modelo;
- el diccionario de datos;
- el modelo lógico.

La implementación se limita a materializar esas decisiones.

---

# Decisión 013

## El Excel oficial constituye la validación del producto

La publicación institucional vigente se utiliza para verificar que el producto construido reproduce correctamente el resultado esperado.

La estructura de la planilla no define el modelo de información.

El modelo surge del análisis del dominio y de las responsabilidades institucionales.

---

# Decisión 014

## Los dominios funcionales se publican como productos independientes

La presencia de distintos dominios de información dentro de una misma publicación institucional no implica que deban formar parte de un mismo producto.

El Producto 001 incorpora únicamente los atributos correspondientes al Padrón de Establecimientos Educativos.

Otros dominios, como las ofertas educativas, deberán implementarse como productos independientes reutilizando la misma metodología.

---

# Decisión 015

## Las transformaciones forman parte del modelo

Las transformaciones realizadas por LocalAPI no modifican la información institucional.

Su objetivo consiste en:

- normalizar valores;
- construir identificadores derivados;
- adaptar formatos de publicación;
- integrar información proveniente de distintas fuentes.

Toda transformación aplicada deberá quedar documentada en el modelo y en el diccionario de datos.

---

# Decisión 016

## La documentación forma parte del producto

Cada producto desarrollado mediante LocalAPI debe poder comprenderse independientemente de su implementación técnica.

La documentación constituye parte del producto y deberá mantenerse sincronizada con el modelo implementado.

Las vistas SQL, los endpoints y las aplicaciones consumidoras deberán derivarse de la documentación y no a la inversa.

---

# Estado

Las decisiones documentadas constituyen las reglas funcionales que deberán respetarse durante la implementación del Producto 001 y servirán como base metodológica para los productos que se desarrollen posteriormente mediante LocalAPI.