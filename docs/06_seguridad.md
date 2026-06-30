# 06. Seguridad

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

La seguridad en LocalAPI tiene como objetivo controlar qué información puede ser publicada mediante la API sin afectar las bases institucionales de origen.

La arquitectura separa claramente:

- acceso a las bases fuente;
- integración de datos;
- publicación de información.

---

# Principios

## Las bases fuente permanecen protegidas

LocalAPI nunca publica directamente tablas pertenecientes a las bases institucionales.

Toda publicación se realiza mediante vistas construidas específicamente para ese fin.

---

## Las aplicaciones no acceden a PostgreSQL

Las aplicaciones cliente consumen exclusivamente la API REST.

Nunca deben conectarse directamente a la base de datos.

---

## El contrato es la vista

Cada vista representa un recurso público.

Los consumidores desconocen cómo se obtuvieron los datos.

La implementación interna puede modificarse sin afectar a quienes utilizan la API.

---

# Roles

La implementación actual utiliza dos roles principales.

## api_authenticator

Es el usuario utilizado por PostgREST para conectarse a PostgreSQL.

Posee permisos suficientes para acceder a las vistas publicadas.

No debe utilizarse desde aplicaciones cliente.

---

## api_anon

Representa al usuario anónimo de la API.

Los permisos otorgados a este rol determinan qué recursos serán visibles públicamente.

Toda nueva vista publicada debe otorgar explícitamente permisos de lectura a este rol.

---

# Publicación de recursos

Para publicar un nuevo endpoint deben cumplirse las siguientes condiciones.

## 1. Crear la vista

La vista debe crearse dentro del schema:

```
api
```

---

## 2. Otorgar permisos

Debe concederse permiso de lectura al rol:

```
api_anon
```

Ejemplo conceptual:

```
GRANT SELECT
ON api.v_nueva_vista
TO api_anon;
```

---

## 3. Verificar publicación

Una vez otorgados los permisos, PostgREST publicará automáticamente el nuevo recurso.

No es necesario modificar configuraciones adicionales.

---

# Buenas prácticas

Se recomienda:

- publicar únicamente vistas;
- ocultar claves internas innecesarias;
- publicar nombres de campos comprensibles;
- evitar exponer estructuras propias de las bases fuente;
- limitar la información al objetivo funcional del endpoint.

---

# Información sensible

No toda la información disponible en las bases institucionales debe exponerse mediante la API.

Cada vista constituye una decisión de publicación.

Antes de construir un nuevo recurso debe evaluarse:

- quién utilizará la información;
- con qué finalidad;
- qué campos resultan necesarios;
- qué datos deben permanecer internos.

---

# Evolución

La implementación actual utiliza un único perfil de acceso anónimo.

En futuras versiones podrán incorporarse mecanismos adicionales como:

- autenticación JWT;
- perfiles diferenciados;
- permisos por recurso;
- permisos por usuario;
- auditoría de accesos.

---

# Alcance

La seguridad implementada por LocalAPI está orientada al desarrollo y validación de MVP.

La incorporación de mecanismos avanzados de autenticación y autorización forma parte de la implementación institucional que podrá realizar posteriormente la Dirección de Sistemas.

---

# Resultado esperado

Toda información publicada por LocalAPI debe encontrarse controlada mediante vistas específicas y permisos explícitos, garantizando que únicamente se exponga la información necesaria para cada caso de uso.