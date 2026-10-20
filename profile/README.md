# Parking Lima

### Plataforma de Reservas de Estacionamientos | Microservicios y DevOps

**Parking Lima** es una plataforma de reservas de estacionamientos basada en una arquitectura de microservicios, diseñada para Lima, Perú.

El proyecto demuestra la implementación de un ciclo de vida moderno de desarrollo y entrega de software, integrando desarrollo backend, frontend, contenedorización, pruebas automatizadas, integración y despliegue continuos (CI/CD) e infraestructura como código (IaC).

## Características

- Explorar estacionamientos en diferentes distritos de Lima.
- Consultar estacionamientos y sus espacios habilitados.
- Registrar y consultar usuarios.
- Crear reservas de estacionamiento por periodos de tiempo.
- Prevenir reservas con horarios superpuestos mediante validaciones en el backend.
- Consultar el historial y estado de las reservas.
- Ejecutar la plataforma localmente mediante Docker Compose.
- Desplegar los contenedores de la aplicación en AWS utilizando flujos de trabajo automatizados.

## Arquitectura

Parking Lima está compuesto por tres microservicios backend, una aplicación frontend desarrollada con React y una base de datos PostgreSQL.

| Componente | Tecnologías | Responsabilidad |
|---|---|---|
| Frontend | React, TypeScript, Vite, Nginx | Interfaz de usuario |
| Parking Service | Python, FastAPI, SQLAlchemy | Gestión de distritos, estacionamientos y espacios |
| Users Service | Java, Spring Boot | Gestión de usuarios |
| Booking Service | Node.js | Gestión de reservas y validación de conflictos |
| Base de datos | PostgreSQL 17 | Persistencia de datos |
| Infraestructura | Terraform, AWS EC2, IAM, S3, SSM | Aprovisionamiento y gestión de infraestructura en la nube |
| CI/CD | GitHub Actions, Docker, GHCR | Pruebas, publicación de imágenes y despliegues |

### Flujo de la aplicación

```text
                 ┌─────────────────────┐
                 │   Frontend React    │
                 │  TypeScript / Vite  │
                 └──────────┬──────────┘
                            │
                         HTTP / API
                            │
             ┌──────────────┼──────────────┐
             │              │              │
       ┌─────▼─────┐  ┌─────▼─────┐  ┌─────▼─────┐
       │  Parking  │  │   Users   │  │  Booking  │
       │  Python   │  │   Java    │  │  Node.js  │
       │  FastAPI  │  │Spring Boot│  │           │
       └─────┬─────┘  └─────┬─────┘  └─────┬─────┘
             │              │              │
             └──────────────┼──────────────┘
                            │
                     ┌──────▼──────┐
                     │ PostgreSQL  │
                     └─────────────┘
```

## DevOps y Automatización

El proyecto implementa un flujo de integración y entrega de software utilizando GitHub y AWS.

1. El desarrollo de funcionalidades se realiza en ramas independientes (*feature branches*).
2. Los cambios se integran mediante solicitudes de incorporación (*Pull Requests*).
3. GitHub Actions ejecuta verificaciones automáticas de calidad.
4. Las imágenes Docker se publican en GitHub Container Registry (GHCR).
5. Terraform administra la infraestructura en AWS.
6. Los flujos de despliegue actualizan los contenedores de la aplicación en Amazon EC2 mediante AWS Systems Manager (SSM).

El proceso de despliegue utiliza etiquetas de imágenes Docker basadas en el identificador SHA de los commits, lo que permite identificar las versiones publicadas y realizar despliegues reproducibles.

## Aseguramiento de la Calidad

El frontend cuenta con **41 pruebas automatizadas**, que abarcan:

- Navegación entre páginas.
- Exploración y búsqueda de distritos.
- Consulta de estacionamientos y selección de espacios.
- Registro y consulta de usuarios.
- Creación de reservas y validación de formularios.
- Visualización del historial de reservas.
- Manejo de errores de los servicios.

Las herramientas utilizadas para verificar la calidad del frontend incluyen:

- **ESLint:** análisis estático del código.
- **Vitest:** ejecución de pruebas automatizadas.
- **React Testing Library:** pruebas de componentes e interacciones.
- **TypeScript:** verificación de tipos y compilación.
- **Vite:** generación de versiones optimizadas para producción.

Además, se han realizado pruebas de integración de extremo a extremo utilizando los microservicios ejecutados localmente mediante Docker.

## Repositorios

El proyecto está organizado en cinco repositorios independientes dentro de la organización de GitHub.

| Repositorio | Descripción |
|---|---|
| [parking-lima-frontend](https://github.com/parking-lima/parking-lima-frontend) | Aplicación web desarrollada con React y TypeScript |
| [parking-lima-parking-service](https://github.com/parking-lima/parking-lima-parking-service) | API para la gestión de distritos, estacionamientos y espacios |
| [parking-lima-users-service](https://github.com/parking-lima/parking-lima-users-service) | API para la gestión de usuarios |
| [parking-lima-booking-service](https://github.com/parking-lima/parking-lima-booking-service) | API para la gestión y validación de reservas |
| [parking-lima-infrastructure](https://github.com/parking-lima/parking-lima-infrastructure) | Configuración de Docker Compose, Terraform y automatización de despliegues |

## Despliegue en la Nube

El entorno de demostración utiliza Amazon EC2 y Docker Compose para ejecutar los componentes de la aplicación.

El aprovisionamiento y la administración de la infraestructura se realizan mediante las siguientes herramientas:

- **Terraform:** definición y aprovisionamiento de infraestructura como código.
- **Amazon EC2:** ejecución de los contenedores de la aplicación.
- **Amazon S3:** almacenamiento remoto del estado de Terraform.
- **AWS IAM:** gestión de roles y permisos.
- **AWS Systems Manager:** ejecución remota de comandos y despliegues sin necesidad de acceso SSH.
- **GitHub Actions:** automatización de validaciones, publicación y despliegue.
- **GitHub Container Registry:** almacenamiento y distribución de imágenes Docker.

**Nota:** El entorno público de demostración puede encontrarse temporalmente deshabilitado cuando la instancia EC2 está detenida para optimizar los costos de infraestructura.

## Objetivos del Proyecto

Parking Lima es un proyecto educativo y de portafolio orientado a poner en práctica conceptos de ingeniería de software y DevOps.

Sus principales objetivos son:

- Aplicar una arquitectura de microservicios a un caso de uso relacionado con la gestión de estacionamientos.
- Desarrollar componentes de software utilizando diferentes lenguajes de programación y tecnologías.
- Implementar procesos de integración continua y entrega continua.
- Automatizar la construcción, validación y publicación de aplicaciones mediante GitHub Actions.
- Administrar infraestructura en la nube mediante código.
- Aplicar prácticas de contenedorización y despliegue automatizado.
- Integrar frontend, backend y persistencia de datos en una solución funcional.
- Implementar un flujo completo desde el desarrollo local hasta el despliegue en AWS.

## Ubicación

Lima, Perú.

---

**Parking Lima** — Proyecto de ingeniería de software orientado al aprendizaje, la automatización y la aplicación de prácticas modernas de DevOps.
