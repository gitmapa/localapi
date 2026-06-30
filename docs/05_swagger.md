# 05. Swagger UI

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Swagger UI constituye la interfaz de exploración y prueba de las APIs publicadas por LocalAPI.

Su función es facilitar el descubrimiento, validación y documentación de los recursos disponibles sin necesidad de desarrollar aplicaciones cliente.

Swagger UI no publica información.

Únicamente consume el documento OpenAPI generado automáticamente por PostgREST.

---

# Arquitectura

```
PostgreSQL

      │

      ▼

PostgREST

      │

      ▼

OpenAPI

      │

      ▼

Swagger UI

      │

      ▼

Usuario
```

---

# ¿Qué permite hacer?

Swagger UI permite:

- visualizar todos los endpoints disponibles;
- conocer los parámetros aceptados por cada recurso;
- ejecutar consultas desde el navegador;
- inspeccionar respuestas;
- validar cambios sobre las vistas SQL.

Todo ello sin escribir una sola línea de código.

---

# Organización recomendada

La implementación actual utiliza la siguiente estructura.

```
C:\postgrest

    swagger-ui

        index.html
```

El archivo `index.html` constituye una aplicación web extremadamente simple cuyo único objetivo es cargar Swagger UI y conectarlo con PostgREST.

---

# Iniciar Swagger UI

Abrir una nueva ventana de **Símbolo del sistema (CMD)**.

Ir a:

```cmd
cd C:\postgrest\swagger-ui
```

Ejecutar:

```cmd
python -m http.server 8080
```

La consola permanecerá abierta mientras el servidor web se encuentre funcionando.

---

# Abrir la interfaz

Ingresar desde el navegador:

```
http://127.0.0.1:8080
```

Si PostgREST se encuentra funcionando correctamente, Swagger mostrará automáticamente todos los endpoints publicados.

---

# Relación con PostgREST

Swagger UI depende completamente de PostgREST.

La secuencia correcta siempre es:

1. Iniciar PostgreSQL.
2. Iniciar PostgREST.
3. Verificar `http://127.0.0.1:3000`.
4. Iniciar Swagger UI.
5. Abrir `http://127.0.0.1:8080`.

Si PostgREST no está disponible, Swagger continuará cargando la interfaz pero no podrá obtener la documentación de la API.

---

# Flujo de trabajo recomendado

Durante el desarrollo de nuevas vistas SQL se recomienda trabajar siempre con Swagger abierto.

El ciclo habitual es:

1. Modificar una vista SQL.
2. Guardar los cambios.
3. Actualizar Swagger.
4. Probar el nuevo endpoint.
5. Validar filtros y resultados.
6. Ajustar la vista si fuera necesario.

No es necesario escribir código adicional ni reiniciar la aplicación.

---

# Casos de uso

Swagger UI resulta especialmente útil para:

- validar nuevos modelos de información;
- revisar nombres de campos;
- verificar filtros disponibles;
- comprobar permisos;
- compartir la API con otros equipos;
- documentar el funcionamiento de un MVP.

---

# Alcance

Swagger UI forma parte del laboratorio de desarrollo de LocalAPI.

No constituye una aplicación destinada a usuarios finales.

Las aplicaciones consumidoras utilizarán directamente los endpoints REST publicados por PostgREST.

Swagger únicamente facilita su exploración y validación.

---

# Resultado esperado

Cuando Swagger UI se encuentra funcionando, cualquier nueva vista publicada dentro del schema `api` aparece automáticamente documentada y disponible para pruebas, sin necesidad de realizar configuraciones adicionales.