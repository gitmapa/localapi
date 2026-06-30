# 09. Roadmap

> Proyecto desarrollado por **MAPA (UEICEE) + IA**

---

# Objetivo

Este documento identifica posibles líneas de evolución para LocalAPI.

No constituye un cronograma de desarrollo.

Representa una visión de crecimiento de la infraestructura a medida que se incorporen nuevos proyectos, nuevas fuentes de información y nuevos consumidores.

---

# Estado actual

Actualmente LocalAPI permite:

- integrar múltiples bases PostgreSQL;
- construir modelos de información mediante vistas SQL;
- publicar automáticamente APIs REST;
- generar documentación OpenAPI;
- validar recursos utilizando Swagger UI.

La primera implementación se desarrolló sobre información proveniente del dominio RANIE.

---

# Evolución de las fuentes

La infraestructura fue diseñada para incorporar nuevas fuentes de información sin modificar su arquitectura.

Posibles incorporaciones:

- nuevas bases PostgreSQL;
- servicios institucionales;
- archivos de intercambio;
- servicios geoespaciales;
- otras fuentes compatibles con el modelo de integración.

---

# Evolución de los modelos de información

Cada nuevo proyecto incorporará nuevos recursos especializados.

Por ejemplo:

- establecimientos;
- edificios;
- organismos;
- programas;
- personas;
- capas geográficas;
- indicadores;
- estadísticas.

La incorporación de nuevos modelos no requiere modificar los existentes.

---

# Evolución de las APIs

La API podrá crecer mediante nuevos endpoints organizados por dominio funcional.

Cada recurso continuará publicándose a partir de vistas SQL dentro del schema `api`.

La documentación OpenAPI continuará generándose automáticamente.

---

# Aplicaciones consumidoras

Las aplicaciones cliente constituirán proyectos independientes de LocalAPI.

Ejemplos posibles:

- visor cartográfico;
- descarga de listados;
- tableros de control;
- aplicaciones móviles;
- herramientas de análisis;
- integraciones con otros sistemas.

Todas ellas consumirán exclusivamente la API publicada por LocalAPI.

---

# Calidad de los datos

A medida que se incorporen nuevas fuentes podrán desarrollarse procesos destinados a:

- normalizar información;
- validar consistencia;
- enriquecer registros;
- unificar dominios;
- documentar reglas de integración.

Estas tareas continuarán implementándose dentro del modelo de información.

---

# Comunidad de desarrollo

La documentación, los modelos de información y los scripts SQL deberán mantenerse organizados para facilitar:

- incorporación de nuevos integrantes;
- reutilización de componentes;
- revisión técnica;
- transferencia de conocimiento.

La documentación constituye un componente fundamental del proyecto.

---

# Visión

LocalAPI busca consolidarse como una infraestructura liviana para diseñar, validar y publicar modelos de información reutilizables.

Cada nuevo proyecto desarrollado sobre esta plataforma incrementará el conocimiento disponible y ampliará las capacidades del laboratorio sin alterar sus principios de funcionamiento.

---

# Resultado esperado

LocalAPI deberá evolucionar incorporando nuevos dominios de información y nuevas aplicaciones consumidoras, manteniendo siempre la misma filosofía:

- comprender el problema;
- construir el modelo de información;
- validar el resultado mediante un MVP;
- publicar una API clara, estable y reutilizable.