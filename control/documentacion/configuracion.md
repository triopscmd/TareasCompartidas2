# Configuración del Proyecto

Este documento detalla los archivos y configuraciones clave que rigen el comportamiento y el desarrollo de la aplicación "Organizador de Tareas Compartidas". Comprender estos archivos es fundamental para cualquier desarrollador que trabaje en el proyecto.

## 1. `package.json`

El archivo `package.json` es el corazón de la configuración del proyecto Node.js/TypeScript. Define metadatos del proyecto, dependencias y scripts esenciales.

*   **`name`, `version`, `description`**: Información básica del proyecto.
*   **`scripts`**: Contiene comandos para diversas tareas de desarrollo y producción:
    *   `start`: Inicia la aplicación en modo de producción (normalmente después de un build).
    *   `dev`: Inicia el servidor de desarrollo (usando `vite` para el frontend y `nodemon` para el backend en desarrollo).
    *   `build`: Compila la aplicación para producción.
    *   `test`: Ejecuta las pruebas unitarias y de integración (`jest`, `react-testing-library`).
    *   `lint`: Ejecuta herramientas de linting para mantener la consistencia del código (`eslint`).
    *   `typeorm`: Comandos específicos para TypeORM (migraciones, etc.).
*   **`dependencies`**: Listado de paquetes necesarios para que la aplicación funcione en producción (ej. `express`, `react`, `typeorm`, `bcryptjs`, `jsonwebtoken`).
*   **`devDependencies`**: Paquetes necesarios solo durante el desarrollo y las pruebas (ej. `typescript`, `vite`, `jest`, `nodemon`, `eslint`, `tailwindcss`, `@types/*`).

## 2. `vite.config.ts`

Este archivo configura Vite, el bundler utilizado para el frontend de React. Es crucial para el proceso de construcción y desarrollo del lado del cliente.

*   **`plugins`**: Define los plugins de Vite en uso, como `@vitejs/plugin-react` para habilitar el soporte de React y HMR (Hot Module Replacement).
*   **`resolve.alias`**: Permite definir alias para rutas de importación, facilitando las importaciones absolutas y organizando el código (ej. `@/components` en lugar de `../../components`).
*   **`server.proxy`**: Configura un proxy para redirigir las solicitudes API del frontend de desarrollo al backend, evitando problemas de CORS durante el desarrollo.
*   **`build.outDir`**: Especifica el directorio de salida para los archivos de frontend compilados.

## 3. `.env` y `.env.example`

Los archivos `.env` (y su contraparte `.env.example` para la plantilla) son esenciales para gestionar variables de entorno, que contienen información sensible o configuraciones que varían entre entornos (desarrollo, producción, testing).

*   **`PORT`**: Puerto en el que el servidor backend escuchará.
*   **`DATABASE_URL`**: Cadena de conexión a la base de datos (incluyendo usuario, contraseña, host, puerto, nombre de la DB).
*   **`JWT_SECRET`**: Clave secreta utilizada para firmar y verificar JSON Web Tokens.
*   **`NODE_ENV`**: Indica el entorno de ejecución (development, production, test).
*   **`EMAIL_SERVICE_API_KEY`**: Clave para servicios de envío de correos, si se implementan notificaciones por email.

**Importante**: El archivo `.env` nunca debe ser subido al control de versiones. `.env.example` debe contener todas las variables necesarias con valores de marcador de posición para que otros desarrolladores puedan configurar su entorno fácilmente.

## 4. `src/config/index.ts` y `src/config/database.ts`

Estos archivos en la carpeta `src/config` centralizan las configuraciones de la aplicación de manera programática.

*   **`src/config/index.ts`**: Contiene configuraciones generales que pueden ser accedidas desde cualquier parte de la aplicación, cargando valores del `.env` o usando valores por defecto. Puede incluir configuraciones como el puerto del servidor, prefijos de API, etc.
*   **`src/config/database.ts`**: Gestiona la configuración de la conexión a la base de datos, inicializando el ORM (ej. TypeORM DataSource) con las credenciales y modelos adecuados.

## 5. `ormconfig.json` (o similar si se usa TypeORM/Sequelize CLI)

Si se utiliza un ORM como TypeORM, este archivo (o configuración similar en `package.json` o `tsconfig.json`) define las configuraciones específicas del ORM para la CLI, como la ubicación de las entidades, migraciones y sus configuraciones de ejecución.

## 6. `.github/workflows/main.yml` (o equivalente de CI/CD)

Este archivo define el pipeline de Integración Continua y Despliegue Continuo (CI/CD) para GitHub Actions (o la herramienta de CI/CD elegida). Describe los pasos automatizados que se ejecutan en cada push o Pull Request:

*   **Activadores**: Cuándo se ejecuta el workflow (ej. `on: push`, `on: pull_request`).
*   **Trabajos (`jobs`)**: Conjunto de pasos a ejecutar, como:
    *   `build`: Instalar dependencias, compilar el código TypeScript, construir el frontend.
    *   `test`: Ejecutar las pruebas unitarias y de integración.
    *   `lint`: Verificar la calidad del código.
    *   `deploy`: (Opcional) Desplegar la aplicación a un entorno de staging o producción si todas las etapas anteriores son exitosas.

## 7. `tailwind.config.js` y `postcss.config.js`

Estos archivos son cruciales para la configuración de Tailwind CSS, el framework de CSS utilitario.

*   **`tailwind.config.js`**: Permite personalizar Tailwind, definiendo colores, fuentes, espaciados, extensiones de temas, y, lo más importante, configurando la propiedad `content` para que Tailwind sepa qué archivos escanear en busca de clases utilitarias para generar el CSS final.
*   **`postcss.config.js`**: Configura PostCSS, que Tailwind utiliza. Asegura que los plugins de PostCSS (como `tailwindcss` y `autoprefixer`) se apliquen correctamente a su CSS.

Comprender cómo interactúan estos archivos es clave para depurar, extender y mantener la aplicación de manera efectiva.