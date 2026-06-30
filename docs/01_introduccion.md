# 01. Introducción

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

## ¿Qué es LocalAPI?

LocalAPI es un laboratorio de integración y publicación de datos desarrollado en UEICEE para construir rápidamente APIs funcionales sobre PostgreSQL.

Su objetivo es validar requerimientos, demostrar su utilidad y entregar a la Dirección de Sistemas un MVP completamente operativo que sirva como referencia para una implementación productiva.

El proyecto no busca reemplazar el desarrollo institucional. Busca reducir la incertidumbre técnica antes de iniciar ese desarrollo.

---

# Objetivos

LocalAPI persigue cuatro objetivos principales.

## 1. Integrar fuentes de datos

Permitir consultar información proveniente de múltiples bases institucionales sin modificar las bases originales.

Cada fuente continúa siendo administrada por su responsable.

---

## 2. Construir un modelo de información

La integración no consiste únicamente en unir tablas.

El objetivo es construir vistas que representen información útil para responder necesidades concretas de los usuarios.

La lógica de integración vive en SQL.

---

## 3. Publicar APIs rápidamente

Una vez construido un modelo de información consistente, las vistas son publicadas automáticamente como endpoints REST mediante PostgREST.

Esto permite disponer de una API funcional sin desarrollar un backend específico.

---

## 4. Validar requerimientos

Antes de solicitar desarrollos productivos a la Dirección de Sistemas, LocalAPI permite responder preguntas como:

- ¿La información existe?
- ¿Puede integrarse?
- ¿Qué campos deberían publicarse?
- ¿Qué estructura debería tener la API?
- ¿Qué utilidad aporta al usuario?

Cuando esas respuestas ya fueron validadas mediante un MVP funcional, el desarrollo institucional comienza con mucha menor incertidumbre.

---

# Filosofía del proyecto

LocalAPI se apoya sobre algunos principios simples.

## Las bases fuente no se modifican

Toda integración se realiza desde una base independiente mediante PostgreSQL Foreign Data Wrapper (FDW).

---

## La lógica pertenece a la base de datos

La transformación, normalización e integración de los datos se implementan mediante vistas SQL.

No se replica lógica de negocio en aplicaciones cliente.

---

## La API es una consecuencia del modelo de información

Primero se diseña el modelo.

Después se publica la API.

Nunca al revés.

---

## Las aplicaciones consumen la API

Las aplicaciones cliente no acceden directamente a las bases de datos.

Toda consulta debe realizarse utilizando los endpoints publicados por LocalAPI.

Esto desacopla las aplicaciones de las estructuras internas de cada base institucional.

---

# Alcance

LocalAPI no es una aplicación.

LocalAPI no es un sistema de gestión.

LocalAPI no reemplaza a un backend institucional.

LocalAPI constituye una infraestructura de integración, experimentación y publicación de datos que permite construir prototipos funcionales con muy bajo costo de desarrollo.

---

# Estado actual

Actualmente el proyecto integra información proveniente de distintas bases institucionales utilizando PostgreSQL, PostGIS, PostgreSQL Foreign Data Wrapper (FDW), PostgREST y Swagger UI.

La primera implementación se desarrolló sobre datos de RANIE, pero la arquitectura fue diseñada para incorporar nuevas fuentes de información sin modificar el modelo general.

---

# Evolución esperada

La infraestructura podrá utilizarse para construir nuevas APIs sobre diferentes dominios de información, manteniendo siempre la misma arquitectura de integración y publicación.

Las aplicaciones que consuman estas APIs constituirán proyectos independientes de LocalAPI.