# Decisiones de Arquitectura Clave

Este documento registra las decisiones arquitectónicas fundamentales tomadas durante la fase de diseño y configuración inicial del proyecto "Organizador de Tareas Compartidas". Estas decisiones definen el stack tecnológico, la estructura y las metodologías que guían el desarrollo de la aplicación.

## 1. Stack Tecnológico General

*   **Frontend**: React con TypeScript
*   **Backend**: Node.js con Express y TypeScript
*   **Base de Datos**: PostgreSQL
*   **ORM**: TypeORM
*   **Estilos**: Tailwind CSS
*   **Build Tool (Frontend)**: Vite

**Justificación**: Esta combinación proporciona un stack moderno, robusto y escalable. React ofrece una interfaz de usuario reactiva y eficiente. Node.js/Express con TypeScript en el backend asegura consistencia de lenguaje y tipos de extremo a extremo. PostgreSQL es una base de datos relacional potente y fiable. TypeORM facilita la interacción con la base de datos de manera orientada a objetos. Tailwind CSS acelera el desarrollo de UI con un enfoque utilitario. Vite ofrece una experiencia de desarrollo frontend excepcionalmente rápida.

## 2. Estructura del Repositorio (Monorepo Lógico)

El proyecto se organiza en una estructura de monorepo *lógico*, donde el código del frontend (`src/client`) y el backend (`src/server`) coexisten en la misma base de código principal, pero con una clara separación de responsabilidades a nivel de carpetas.

*   **`src/`**: Contiene todo el código fuente de la aplicación.
    *   **`src/client/`**: Código del frontend (React, Vite).
    *   **`src/server/`**: Código del backend (Node.js, Express, TypeORM).
    *   **`src/shared/`**: Contiene interfaces, tipos o utilidades que pueden ser compartidas entre el frontend y el backend para evitar duplicación y asegurar consistencia.
*   **`test/`**: Contiene todas las pruebas (unitarias, integración, e2e).
*   **`control/`**: Documentación y configuraciones de gobernanza del proyecto.

**Justificación**: Facilita la colaboración y la consistencia. Permite compartir tipos (interfaces de API) entre frontend y backend. Simplifica la configuración de CI/CD. Sin embargo, se mantiene una clara separación para permitir una posible futura división en microservicios o repositorios separados si la complejidad lo demanda.

## 3. Desarrollo Guiado por Pruebas (TDD)

El TDD es una metodología fundamental adoptada en este proyecto. Ninguna línea de código de implementación debe escribirse sin una prueba que falle primero.

**Justificación**: Asegura la calidad del código, fomenta un diseño modular y desacoplado, facilita la refactorización y reduce la aparición de regresiones. Las pruebas son una forma de documentación viva y fiable.

## 4. Integración Continua (CI)

Se ha configurado un pipeline de CI (utilizando GitHub Actions) para automatizar el build, las pruebas de unidad e integración, y el linting en cada `push` y `Pull Request`.

**Justificación**: Garantiza que el código base esté siempre en un estado funcional, detecta errores tempranamente y mantiene un alto estándar de calidad. Imprescindible para la colaboración en equipo y la entrega frecuente.

## 5. Manejo de Estado de Frontend

*   **Context API de React** (o una librería ligera como Zustand/Jotai)

**Justificación**: Para la mayoría de las necesidades de gestión de estado global, el Context API de React es suficiente y evita añadir una dependencia pesada como Redux para proyectos de este tamaño. Si la complejidad crece, se considerará una opción más robusta. Se prioriza la simplicidad inicial.

## 6. Autenticación y Autorización

*   **Autenticación**: JSON Web Tokens (JWT) basados en un sistema de autenticación de credenciales (email/contraseña).
*   **Autorización**: Middleware basado en roles y pertenencia a grupos.

**Justificación**: JWTs son un estándar de facto para la autenticación sin estado en APIs RESTful, permitiendo escalabilidad y facilidad de implementación. La autorización granular a través de middleware y roles/grupos asegura que los usuarios solo accedan a los recursos y realicen acciones para las que tienen permiso, lo cual es crítico en una aplicación de tareas compartidas.

## 7. Manejo de Errores Estándar

Implementación de un middleware de manejo de errores global en el backend y una estructura de respuestas API estandarizadas (ej. `ApiResponse` utilitario) para asegurar un manejo consistente y predecible de errores y respuestas en toda la API.

**Justificación**: Mejora la experiencia del desarrollador de frontend y la capacidad de depuración al proporcionar mensajes de error claros y formatos consistentes. Aumenta la robustez de la aplicación.

## 8. Migraciones de Base de Datos

Se utilizarán las capacidades de migración de TypeORM para gestionar los cambios en el esquema de la base de datos de manera controlada y versionada.

**Justificación**: Es fundamental para el desarrollo evolutivo del esquema de la base de datos, permitiendo añadir o modificar tablas y columnas de forma segura y reproducible en diferentes entornos de desarrollo y producción.