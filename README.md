# Backend Despachos - Innovatech Chile

API REST desarrollada en Spring Boot para gestión de despachos, desplegada en AWS EC2 mediante contenedor Docker y pipeline CI/CD con GitHub Actions.

## Tecnologías
- Java 17
- Spring Boot 3.4.4
- MySQL 8.0
- Docker (multi-stage build)
- GitHub Actions (CI/CD)

## Arquitectura
- EC2 privada (subnet-privada 10.0.2.0/24)
- Puerto: 8081
- Base de datos: MySQL en ec2-data (3306)

Este repositorio incluye el `docker-compose.yml` que levanta **ambos backends** (ventas y despachos) en la misma EC2 privada.

## Endpoints
- `GET /api/v1/despachos` - Obtener todos los despachos
- `GET /api/v1/despachos/{id}` - Obtener despacho por ID
- `POST /api/v1/despachos` - Crear despacho
- `PUT /api/v1/despachos/{id}` - Actualizar despacho
- `DELETE /api/v1/despachos/{id}` - Eliminar despacho

## Pipeline CI/CD
El pipeline se activa con push en la rama `deploy`:
1. Construye imagen Docker multi-stage
2. Publica imagen en Docker Hub
3. Despliega en EC2 via AWS SSM usando `docker-compose` (levanta ventas + despachos)

En el deploy se crea un `.env` en la EC2 con las variables de base de datos, se ajusta el plugin de autenticacion de MySQL en la EC2 data y se ejecuta `docker-compose up -d`.

## Docker Compose
- `docker-compose.yml` define los servicios `backend-ventas` y `backend-despachos`.
- Incluye volúmenes nombrados para persistencia a nivel de contenedor.
- Define una red interna para aislar la comunicación entre servicios.

## Persistencia
La base de datos corre en la EC2 de datos usando un volumen Docker **named**  montado en `/var/lib/mysql`, lo que permite mantener la informacion al reiniciar o recrear el contenedor.

## Variables de entorno
| Variable | Descripción |
|----------|-------------|
| DB_ENDPOINT | IP del servidor MySQL |
| DB_PORT | Puerto MySQL (3306) |
| DB_NAME | Nombre de la base de datos |
| DB_USERNAME | Usuario MySQL |
| DB_PASSWORD | Contraseña MySQL |