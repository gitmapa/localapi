# 04. PostgREST

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

PostgREST es el componente encargado de publicar automáticamente como API REST las vistas definidas dentro de PostgreSQL.

En LocalAPI no existe un backend desarrollado en PHP, Java, .NET o Python.

La propia base de datos constituye el backend y PostgREST expone su modelo de información mediante HTTP.

---

# ¿Cómo funciona?

PostgREST establece una conexión permanente con PostgreSQL.

Toda vista publicada dentro del schema configurado queda automáticamente disponible como un endpoint REST.

Por ejemplo:

```
api.v_cui
```

se publica como

```
GET /v_cui
```

sin necesidad de escribir código adicional.

---

# Arquitectura

```
PostgreSQL

api.v_cui
api.v_cueanexos
api.v_...

        │

        ▼

PostgREST

        │

        ▼

REST API

GET /v_cui

GET /v_cueanexos

GET /...
```

---

# Archivo de configuración

PostgREST se configura mediante un único archivo.

En la implementación actual:

```
C:\postgrest\ranie_dev.conf
```

Este archivo define:

- la base de datos a utilizar;
- el usuario de conexión;
- el schema publicado;
- el rol anónimo;
- el puerto HTTP;
- la configuración CORS.

---

# Organización recomendada

```
C:\postgrest

    postgrest.exe

    ranie_dev.conf

    swagger-ui\
```

Esta carpeta constituye únicamente la infraestructura necesaria para publicar la API.

No forma parte del repositorio Git.

---

# Iniciar PostgREST

Abrir una ventana de **Símbolo del sistema (CMD)**.

Ir a la carpeta:

```cmd
cd C:\postgrest
```

Ejecutar:

```cmd
postgrest.exe ranie_dev.conf
```

Si la configuración es correcta, la consola permanecerá abierta esperando conexiones.

No debe cerrarse mientras la API esté en funcionamiento.

---

# Verificar funcionamiento

Abrir un navegador.

Ingresar:

```
http://127.0.0.1:3000/
```

Debe visualizarse un documento OpenAPI en formato JSON.

Esto confirma que PostgREST se encuentra conectado correctamente a PostgreSQL.

---

# Probar un endpoint

Ejemplo:

```
http://127.0.0.1:3000/v_cui?limit=5
```

o

```
http://127.0.0.1:3000/v_cueanexos?limit=5
```

Si la consulta devuelve registros, la publicación de la API es correcta.

---

# ¿Qué ocurre al crear una nueva vista?

Supongamos que se crea:

```
api.v_establecimientos
```

No es necesario reiniciar PostgREST.

El nuevo recurso queda inmediatamente disponible como:

```
GET /v_establecimientos
```

La documentación OpenAPI también se actualiza automáticamente.

---

# Ventajas

El uso de PostgREST permite:

- eliminar el desarrollo de un backend para consultas simples;
- mantener una única fuente de verdad;
- publicar rápidamente nuevos recursos;
- generar documentación automáticamente;
- facilitar la validación de modelos de información.

---

# Alcance

PostgREST constituye la infraestructura de publicación de LocalAPI.

No reemplaza un backend institucional.

Su función es acelerar el desarrollo de MVP, validar contratos de datos y demostrar el funcionamiento de nuevas APIs antes de su implementación definitiva.

---

# Resolución de problemas

## No abre el puerto 3000

Verificar que PostgREST se encuentre ejecutándose.

---

## Error de autenticación

Revisar el archivo:

```
ranie_dev.conf
```

y comprobar:

- usuario;
- contraseña;
- nombre de la base.

---

## No aparecen los endpoints

Verificar que las vistas existan dentro del schema:

```
api
```

---

## La API responde pero una vista no aparece

Confirmar que la vista pertenece al schema publicado por PostgREST y que el rol `api_anon` posee permisos de lectura sobre ella.

---

# Resultado esperado

Cuando PostgREST está funcionando, cualquier modificación realizada sobre las vistas públicas de LocalAPI queda disponible inmediatamente mediante una API REST documentada automáticamente.