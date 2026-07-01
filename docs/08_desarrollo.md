# 08. Desarrollo

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

LocalAPI constituye una metodología para diseñar, validar y publicar modelos de información antes de su implementación institucional.

El objetivo del desarrollo no consiste en construir APIs.

El objetivo consiste en construir modelos de información que resuelvan necesidades concretas de los usuarios.

La API es una consecuencia de ese proceso.

---

# Filosofía

En LocalAPI el desarrollo comienza con una pregunta.

Nunca comienza con una tabla.

Nunca comienza con una tecnología.

Nunca comienza con un endpoint.

La primera pregunta siempre es:

> ¿Qué información necesita el usuario?

A partir de esa respuesta comienza el diseño.

---

# Método de trabajo

Cada desarrollo sigue el mismo recorrido.

## 1. Identificar una necesidad

Existe un requerimiento funcional.

Por ejemplo:

- localizar establecimientos;
- descargar un padrón;
- visualizar información sobre un mapa;
- integrar información proveniente de distintas bases.

El requerimiento siempre pertenece al usuario.

Nunca pertenece a la tecnología.

---

## 2. Identificar las fuentes

Se analizan las bases institucionales disponibles.

Se determina:

- qué información existe;
- qué información falta;
- qué relaciones pueden establecerse;
- qué limitaciones presentan las fuentes.

---

## 3. Construir el modelo de información

La etapa más importante del proceso.

Aquí se decide:

- qué información publicar;
- cómo integrarla;
- cómo nombrarla;
- qué complejidad ocultar;
- qué reglas aplicar.

El resultado es una o más vistas SQL.

El modelo de información constituye el verdadero producto del desarrollo.

---

## 4. Publicar la API

Una vez validado el modelo de información, la publicación resulta inmediata mediante PostgREST.

No se desarrolla un backend específico.

La infraestructura transforma automáticamente las vistas en recursos REST.

---

## 5. Validar

El nuevo recurso se prueba utilizando Swagger UI.

Se verifica:

- estructura;
- nombres;
- filtros;
- resultados;
- utilidad.

Si el modelo requiere modificaciones, se ajusta la vista SQL.

---

## 6. Construir aplicaciones cliente

Una vez estabilizada la API pueden desarrollarse aplicaciones consumidoras.

Estas aplicaciones nunca acceden directamente a PostgreSQL.

Toda interacción ocurre mediante la API.

---

# Principios de diseño

---

## El modelo precede a la API

Nunca se diseña una API antes de comprender el problema.

La API refleja el modelo.

No lo reemplaza.

---

## Publicar datos es una decisión de diseño

La existencia de una tabla no implica que deba existir un endpoint.

Cada recurso publicado representa una decisión consciente sobre qué información resulta útil para los consumidores de la API.

Publicar información constituye una decisión de diseño, no una consecuencia técnica.

---

## Las bases pertenecen a sus responsables

LocalAPI únicamente los integra.

Nunca modifica información de origen.

---

## La complejidad permanece dentro de LocalAPI

Las aplicaciones cliente no necesitan conocer:

- estructuras internas;
- relaciones complejas;
- procesos de integración;
- normalizaciones;
- inconsistencias históricas.

Todo ello permanece encapsulado dentro del modelo de información.

---

## Los MVP reducen incertidumbre

El propósito principal de LocalAPI consiste en construir prototipos funcionales.

Estos prototipos permiten responder preguntas antes de iniciar desarrollos institucionales.

Por ejemplo:

- ¿La integración es posible?
- ¿La información resulta útil?
- ¿Qué campos deberían publicarse?
- ¿Qué consultas realizarán los usuarios?
- ¿Qué volumen de información se intercambiará?

Cuando estas preguntas ya poseen respuesta, la implementación institucional puede concentrarse en aspectos propios de una solución productiva.

---

# Rol de MAPA

MAPA actúa como laboratorio de integración y experimentación.

Su función consiste en:

- analizar requerimientos;
- comprender las fuentes de información;
- construir modelos;
- validar soluciones;
- demostrar su utilidad mediante MVP funcionales.

El resultado del trabajo constituye una referencia técnica para la Dirección de Sistemas.

---

## No duplicar responsabilidades

LocalAPI integra información.

No reemplaza los procesos de administración de datos existentes.

Cada conjunto de información debe mantenerse únicamente en el sistema responsable de su administración.

Cuando una fuente institucional administra correctamente un dato, LocalAPI debe consumirlo desde dicha fuente y evitar cualquier duplicación de carga o mantenimiento.

Este principio reduce el riesgo de inconsistencias, elimina tareas redundantes y permite que cada área continúe siendo responsable de la calidad de su propia información.

El modelo de información de LocalAPI integra estas fuentes para construir productos institucionales sin replicar sus procesos de gestión.

---

# Evolución

Cada nuevo proyecto desarrollado mediante LocalAPI amplía el conocimiento acumulado del laboratorio.

La infraestructura permanece estable.

Lo que evoluciona son los modelos de información construidos sobre ella.

---

# Resultado esperado

Cada MVP desarrollado mediante LocalAPI debe demostrar que un requerimiento puede resolverse, cómo debería resolverse y cuál es el valor que aporta a los usuarios antes de iniciar su desarrollo institucional.