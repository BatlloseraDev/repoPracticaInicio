# Nombre del Proyecto

Una breve descripción de qué hace este proyecto y para quién es. Aquí puedes detallar el propósito principal, las tecnologías clave utilizadas y el problema que resuelve.

## Requisitos Previos

Antes de comenzar, asegúrate de tener instaladas las siguientes herramientas en tu sistema:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Cómo levantar la aplicación

Sigue estos pasos para poner en marcha el entorno de desarrollo local:

1.  **Clona el repositorio:**
    ```bash
    git clone <URL_DEL_REPOSITORIO>
    cd <NOMBRE_DEL_PROYECTO>
    ```

2.  **Configura las variables de entorno:**
    Copia el archivo de ejemplo `.env.example` a un nuevo archivo llamado `.env` y ajústalo con tu configuración local.
    ```bash
    cp .env.example .env
    ```

3.  **Levanta los servicios:**
    Usa Docker Compose para construir las imágenes y levantar los contenedores.
    ```bash
    docker compose up --build
    ```
    La aplicación estará disponible en `http://localhost:8000` (o el puerto que hayas configurado en tus variables de entorno).

## Entorno de Desarrollo

Para ejecutar comandos dentro del contenedor de la aplicación (por ejemplo, comandos de `manage.py` si usas Django, o comandos de `npm` si es un proyecto Node.js), utiliza `docker compose run`.

El comando `run` iniciará un nuevo contenedor efímero usando la configuración del servicio especificado en `docker-compose.yml`.

**Ejemplos:**

```bash
# Ejecutar migraciones de la base de datos (ejemplo con Django)
docker compose run --rm web python manage.py migrate

# Abrir un shell interactivo dentro del contenedor 'web'
docker compose run --rm web /bin/bash
```

> **Nota:** El flag `--rm` es útil para eliminar el contenedor automáticamente después de que el comando se haya ejecutado, manteniendo tu sistema limpio.

## Tests y Formateo de Código

### Ejecutar Tests

Para ejecutar la suite de tests, utiliza el siguiente comando. Esto asegurará que el código funciona como se espera.

```bash
docker compose run --rm web pytest
```

### Formateo de Código

Mantenemos un estilo de código consistente usando herramientas como `black` e `isort`. Para formatear tus archivos, ejecuta:

```bash
docker compose run --rm web black .
docker compose run --rm web isort .
```

## Pre-commit

Este proyecto utiliza `pre-commit` para asegurar que el código cumpla con los estándares de calidad y formato antes de ser incluido en el historial de Git.

El hook de pre-commit se ejecuta automáticamente cada vez que intentas hacer un `git commit`. Realizará las siguientes acciones:
-   Formateará el código con `black` e `isort`.
-   Verificará si hay errores de sintaxis o estilo con `flake8`.

Si `pre-commit` encuentra algún problema, modificará los archivos para corregirlo (si es posible) y cancelará el commit. Simplemente necesitarás revisar los cambios, agregarlos al "stage" (`git add .`) y volver a intentar el `git commit`. Esto garantiza que todo el código en el repositorio principal mantenga una alta calidad.
