# 08. Desarrollo

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

LocalAPI constituye una metodología para diseñar, construir y publicar productos de información institucionales.

El objetivo del desarrollo no consiste en construir APIs.

El objetivo consiste en comprender un problema, diseñar un modelo de información que lo resuelva y publicarlo mediante una arquitectura simple, documentada y reutilizable.

La API representa únicamente uno de los mecanismos de publicación de dicho modelo.

---

# Filosofía

Todo desarrollo comienza con una necesidad concreta.

Nunca comienza con:

- una consulta SQL;
- una tabla;
- una tecnología;
- un endpoint;
- una aplicación.

La primera pregunta siempre es:

> **¿Qué producto necesita el usuario?**

A partir de esa respuesta comienza todo el proceso de diseño.

---

# El producto como unidad de trabajo

En LocalAPI el desarrollo se organiza alrededor de productos de información.

Cada producto representa una necesidad institucional concreta y posee:

- un objetivo;
- una unidad de publicación;
- un modelo lógico;
- un diccionario de datos;
- una implementación SQL;
- uno o más mecanismos de publicación.

El producto constituye la verdadera unidad de desarrollo.

---

# Método de trabajo

Todos los productos desarrollados mediante LocalAPI siguen el mismo recorrido.

## 1. Identificar la necesidad

Todo desarrollo comienza con una necesidad funcional.

Por ejemplo:

- publicar un padrón;
- integrar información;
- localizar establecimientos;
- construir un mapa;
- ofrecer una API.

La necesidad pertenece al usuario.

Nunca pertenece a la tecnología.

---

## 2. Definir el producto

La necesidad se transforma en un producto de información.

En esta etapa se responde:

- ¿qué problema resuelve?
- ¿quién lo utilizará?
- ¿qué información publicará?
- ¿qué información no publicará?
- ¿cuál será su unidad de publicación?

Una buena definición del producto evita rediseños posteriores.

---

## 3. Identificar las fuentes de verdad

Se analizan las fuentes institucionales disponibles.

Para cada atributo se determina:

- quién lo administra;
- cuál es su fuente de verdad;
- cuál es su nivel de actualización;
- si requiere integración con otras fuentes.

Uno de los principios fundamentales de LocalAPI establece que cada atributo posee una única fuente de verdad.

---

## 4. Comprender el dominio

Antes de implementar cualquier consulta se estudia el dominio de información.

Durante esta etapa se documentan:

- hallazgos;
- relaciones;
- restricciones;
- responsabilidades institucionales;
- reglas de negocio.

El objetivo consiste en comprender completamente el problema antes de comenzar la implementación.

---

## 5. Diseñar el modelo lógico

Una vez comprendido el dominio se construye el modelo lógico.

Aquí se definen:

- entidades;
- relaciones;
- atributos;
- herencias;
- transformaciones;
- dominios funcionales.

El modelo lógico constituye el verdadero diseño del producto.

---

## 6. Construir el diccionario de datos

Cada atributo publicado debe quedar documentado.

Como mínimo se registra:

- nombre;
- descripción;
- fuente;
- obligatoriedad;
- observaciones.

El diccionario constituye el contrato funcional del producto.

---

## 7. Implementar la vista SQL

Recién cuando el producto se encuentra completamente definido comienza la implementación.

La vista SQL traduce el modelo lógico a una implementación concreta dentro de PostgreSQL.

No introduce nuevas decisiones funcionales.

Su única responsabilidad consiste en materializar el modelo previamente documentado.

---

## 8. Validar

El resultado obtenido se compara contra la publicación institucional vigente.

La publicación oficial constituye el mecanismo de validación del producto.

No constituye la definición del modelo.

Las diferencias detectadas permiten:

- corregir errores;
- completar atributos;
- ajustar reglas de integración.

---

## 9. Publicar

Una vez validada la vista SQL el producto puede publicarse mediante distintos mecanismos.

Entre ellos:

- API REST;
- JSON;
- CSV;
- XLSX;
- GeoJSON.

Todos representan exactamente el mismo modelo de información.

---

## 10. Construir aplicaciones consumidoras

Las aplicaciones no consultan directamente las bases de datos.

Consumen exclusivamente los productos publicados por LocalAPI.

De esta forma:

- se desacopla la implementación;
- se reutiliza el mismo modelo;
- se evita duplicar lógica de integración.

---

# Principios de diseño

## El producto precede al SQL

Las consultas SQL implementan decisiones previamente documentadas.

Nunca definen el producto.

---

## El modelo precede a la API

Los endpoints representan modelos de información.

No representan tablas.

No representan consultas.

No representan estructuras internas de las bases.

---

## Una única fuente de verdad

Cada atributo publicado posee un único responsable institucional.

LocalAPI integra esa información.

No la administra.

---

## No duplicar responsabilidades

Cada organismo continúa siendo responsable de los datos que administra.

LocalAPI reutiliza esas fuentes para construir productos institucionales.

---

## La documentación forma parte del desarrollo

Todo conocimiento adquirido durante el análisis debe quedar documentado.

Entre otros:

- hallazgos;
- decisiones;
- modelos;
- diccionarios;
- transformaciones.

La documentación constituye parte del producto.

No un complemento.

---

## El Excel valida, no diseña

Las publicaciones institucionales existentes constituyen una referencia de validación.

El diseño del producto surge del análisis del dominio de información y no de la estructura de una planilla.

---

## El MVP reduce incertidumbre

Cada Producto Mínimo Viable tiene como objetivo responder preguntas antes de iniciar un desarrollo institucional.

Un MVP debe demostrar:

- que la integración es posible;
- que el modelo resulta útil;
- que la documentación es suficiente;
- que la arquitectura es adecuada.

Una vez respondidas esas preguntas, el desarrollo institucional puede concentrarse en aspectos operativos.

---

# Rol de MAPA

MAPA actúa como laboratorio de integración y diseño de productos de información.

Su función consiste en:

- comprender problemas;
- analizar fuentes;
- integrar información;
- diseñar modelos;
- validar resultados;
- construir MVP.

El laboratorio no reemplaza a los sistemas existentes.

Construye productos que reutilizan la información administrada por dichos sistemas.

---

# Evolución

Cada nuevo producto incrementa el conocimiento acumulado por LocalAPI.

La infraestructura permanece estable.

La metodología permanece estable.

Lo que evoluciona son los modelos de información construidos sobre ellas.

De esta manera, cada nuevo desarrollo reduce el esfuerzo necesario para construir los siguientes.

---

# Resultado esperado

Todo producto desarrollado mediante LocalAPI debe permitir que un usuario pueda consumir información institucional sin conocer:

- dónde se almacenan los datos;
- cuántas bases intervienen;
- cómo se integran;
- qué transformaciones fueron necesarias.

El usuario accede únicamente a un producto consistente, documentado y reutilizable.

Ese constituye el objetivo principal de LocalAPI.