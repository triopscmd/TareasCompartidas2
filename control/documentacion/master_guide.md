# Guía Maestra del "Organizador de Tareas Compartidas"

Bienvenido a la guía maestra del proyecto "Organizador de Tareas Compartidas". Este documento proporciona una visión general de alto nivel de las funcionalidades clave de la aplicación, su arquitectura y cómo se organiza el desarrollo. Es el punto de partida para cualquier persona que desee comprender la visión general del proyecto.

## 1. Visión General del Proyecto

El "Organizador de Tareas Compartidas" es una aplicación web diseñada para facilitar la colaboración en equipo. Permite a los usuarios crear, organizar y gestionar tareas dentro de grupos compartidos, asignarlas a miembros específicos, establecer fechas límite y seguir su progreso. El objetivo es proporcionar una plataforma intuitiva para mejorar la productividad y la comunicación dentro de equipos y grupos de trabajo.

## 2. Funcionalidades Principales

A continuación, se describen las características fundamentales de la aplicación:

### 2.1. Autenticación y Gestión de Perfil de Usuario
*   **Registro e Inicio de Sesión Seguro**: Los usuarios pueden crear una cuenta y acceder a la aplicación de forma segura utilizando credenciales (email y contraseña). Se implementa un sistema de tokens para mantener las sesiones activas.
*   **Gestión de Perfil**: Cada usuario tiene la capacidad de ver y actualizar su información personal, incluyendo nombre, correo electrónico y contraseña, a través de una página de perfil dedicada.

### 2.2. Gestión de Grupos y Equipos
*   **Creación y Unión a Grupos**: Los usuarios pueden formar nuevos grupos o ser invitados a unirse a grupos existentes. Cada grupo actúa como un espacio de trabajo colaborativo.
*   **Gestión de Miembros**: Dentro de cada grupo, se pueden añadir, remover y gestionar los miembros, posiblemente con roles definidos (ej. administrador del grupo, miembro regular).

### 2.3. Gestión de Tareas Colaborativas
*   **Creación y Edición de Tareas**: Los miembros de un grupo pueden crear nuevas tareas, definiendo su título, descripción y otros detalles relevantes.
*   **Asignación de Tareas**: Las tareas pueden ser asignadas a uno o varios miembros específicos dentro del grupo, clarificando las responsabilidades.
*   **Fechas Límite y Estados**: Cada tarea puede tener una fecha límite definida y un estado que refleje su progreso (ej. Pendiente, En Progreso, Completada).

### 2.4. Notificaciones y Recordatorios
*   **Recordatorios Automáticos**: La aplicación incluye un sistema de recordatorios automáticos que notifica a los miembros asignados cuando una tarea se acerca a su fecha límite o ya está atrasada, ayudando a mantener el progreso y evitar olvidos.

### 2.5. Interfaz de Usuario Intuitiva
*   **Lista de Tareas Principal**: Una vista centralizada que muestra todas las tareas relevantes para el usuario, con opciones de filtrado (por grupo, por asignación, por estado) y ordenación para facilitar la navegación.
*   **Detalle de Tarea**: Una página dedicada para cada tarea que muestra todos sus atributos, incluyendo miembros asignados, progreso, y comentarios, permitiendo una visión completa y la posibilidad de edición.

## 3. Arquitectura y Tecnologías Clave

La aplicación está construida con un stack moderno y robusto:

*   **Frontend**: Desarrollado con **React y TypeScript**, utilizando **Vite** para un desarrollo rápido y eficiente, y **Tailwind CSS** para un diseño responsivo y consistente.
*   **Backend**: Implementado con **Node.js y Express**, también en **TypeScript**, proporcionando una API RESTful para la interacción con la base de datos y la lógica de negocio.
*   **Base de Datos**: Se utiliza **PostgreSQL** como sistema de gestión de bases de datos relacionales, gestionado a través de **TypeORM** (Object-Relational Mapper) para una interacción segura y tipada.
*   **Metodología de Desarrollo**: El proyecto sigue estrictamente el **Desarrollo Guiado por Pruebas (TDD)** y un ciclo de **Integración Continua (CI)** para asegurar la alta calidad y fiabilidad del código.

## 4. Estructura del Repositorio

El repositorio está organizado para separar claramente las responsabilidades del frontend, backend, pruebas y documentación:

*   `src/client/`: Contiene todo el código de la aplicación de React (frontend).
*   `src/server/`: Contiene el código del servidor Node.js/Express (backend).
*   `src/shared/`: Guarda tipos, interfaces y utilidades compartidas entre frontend y backend.
*   `test/`: Almacena todas las pruebas (unitarias y de integración).
*   `control/`: Contiene la documentación interna del proyecto y archivos de gobernanza (como esta guía).

## 5. Próximos Pasos

Este documento proporciona una base. Para detalles específicos sobre decisiones de arquitectura, configuración del proyecto o procesos de desarrollo, por favor consulte los siguientes documentos en la carpeta `control/documentacion/`:

*   **`decisiones_arquitectura.md`**: Detalla las elecciones tecnológicas y de diseño fundamentales.
*   **`configuracion.md`**: Explica cómo se configuran las diversas partes del proyecto (entorno, base de datos, build).
*   **`tdd_guide.md`**: Guía detallada sobre cómo aplicar TDD en el proyecto.
*   **`ci_cd_guide.md`**: Información sobre el pipeline de Integración/Despliegue Continuo.

Gracias por su interés en el "Organizador de Tareas Compartidas". Esperamos que esta guía le sea útil.