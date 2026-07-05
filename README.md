# Backend Despachos - Innovatech Chile

API REST desarrollada en Spring Boot para gestión de despachos, desplegada en AWS EC2 mediante contenedor Docker y pipeline CI/CD con GitHub Actions.

## Descripción del Proyecto
Este repositorio forma parte de la plataforma central de Innovatech Chile, un sistema distribuido diseñado para la gestión eficiente de ventas y logística. El proyecto completo se compone de tres repositorios principales:
- **Frontend**: Interfaz de usuario desarrollada en React.
- **Backend Ventas**: Microservicio encargado del registro y control de ventas.
- **Backend Despachos**: Microservicio encargado de la coordinación y seguimiento de envíos (este repositorio).

Esta arquitectura permite una alta escalabilidad, mantenimiento simplificado y despliegues independientes en la infraestructura de AWS.

## Tecnologías
- Java 17
- Spring Boot 3.4.4
- MySQL 8.0
- Docker (multi-stage build)
- GitHub Actions (CI/CD)

## Endpoints
- `GET /api/v1/despachos` - Obtener todos los despachos
- `GET /api/v1/despachos/{id}` - Obtener despacho por ID
- `POST /api/v1/despachos` - Crear despacho
- `PUT /api/v1/despachos/{id}` - Actualizar despacho
- `DELETE /api/v1/despachos/{id}` - Eliminar despacho


## Pipeline CI/CD
El pipeline se activa con push en la rama `deploy`:
1. Construye imagen Docker multi-stage
2. Publica imagen en ECR
3. Despliega en EKS via kubectl 


