# Innovatech Backend

Backend del proyecto Innovatech, compuesto por servicios REST desarrollados con Spring Boot para gestionar ventas y despachos. La solucion esta preparada para ejecutarse localmente con Maven o mediante contenedores Docker conectados a una base de datos MySQL.

## Servicios

| Servicio | Descripcion | Puerto local sugerido | Ruta base |
| --- | --- | --- | --- |
| Ventas API | Gestiona ventas, fechas de compra, direccion, valor y estado de despacho generado. | `8082` | `/api/v1/ventas` |
| Despachos API | Gestiona despachos, fecha de despacho, camion, intentos, compra asociada y estado despachado. | `8081` | `/api/v1/despachos` |

## Stack tecnico

- Java 17
- Spring Boot 3.4.4
- Spring Web
- Spring Data JPA
- Spring Validation
- MySQL
- Maven Wrapper
- Springdoc OpenAPI / Swagger UI
- Docker

## Estructura esperada

```text
InnovatechBackend/
├── back-Ventas_SpringBoot/
│   └── Springboot-API-REST/
│       ├── src/
│       ├── pom.xml
│       └── Dockerfile
├── back-Despachos_SpringBoot/
│   └── Springboot-API-REST-DESPACHO/
│       ├── src/
│       ├── pom.xml
│       └── Dockerfile
├── docker-compose.yml
├── .env.example
├── GIT_FLOW.md
└── README.md
```

## Variables de entorno

Las aplicaciones usan variables para conectarse a MySQL:

| Variable | Descripcion | Ejemplo |
| --- | --- | --- |
| `DB_ENDPOINT` | Host o endpoint de MySQL. | `localhost` |
| `DB_PORT` | Puerto de MySQL. | `3306` |
| `DB_NAME` | Nombre de la base de datos. | `app_db` |
| `DB_USERNAME` | Usuario de base de datos. | `app_user` |
| `DB_PASSWORD` | Password del usuario. | `change_me` |

Para Docker Compose tambien se usan:

| Variable | Descripcion | Ejemplo |
| --- | --- | --- |
| `MYSQL_ROOT_PASSWORD` | Password del usuario root de MySQL. | `change_me_root` |
| `MYSQL_DATABASE` | Base de datos creada al iniciar MySQL. | `app_db` |
| `MYSQL_USER` | Usuario de aplicacion. | `app_user` |
| `MYSQL_PASSWORD` | Password del usuario de aplicacion. | `change_me` |
| `DESPACHOS_PORT` | Puerto expuesto para el servicio de despachos. | `8081` |
| `VENTAS_PORT` | Puerto expuesto para el servicio de ventas. | `8082` |

## Ejecucion local con Maven

### Ventas API

```powershell
cd back-Ventas_SpringBoot\Springboot-API-REST
$env:DB_ENDPOINT="localhost"
$env:DB_PORT="3306"
$env:DB_NAME="app_db"
$env:DB_USERNAME="app_user"
$env:DB_PASSWORD="change_me"
.\mvnw.cmd spring-boot:run
```

### Despachos API

```powershell
cd back-Despachos_SpringBoot\Springboot-API-REST-DESPACHO
$env:DB_ENDPOINT="localhost"
$env:DB_PORT="3306"
$env:DB_NAME="app_db"
$env:DB_USERNAME="app_user"
$env:DB_PASSWORD="change_me"
.\mvnw.cmd spring-boot:run
```

## Ejecucion con Docker Compose

Crear un archivo `.env` desde `.env.example` y ajustar los valores necesarios. Luego ejecutar:

```powershell
docker compose up -d --build
```

Ver logs:

```powershell
docker compose logs -f ventas-backend
docker compose logs -f despachos-backend
```

Detener el stack:

```powershell
docker compose down
```

## Endpoints principales

### Ventas

| Metodo | Endpoint | Descripcion |
| --- | --- | --- |
| `GET` | `/api/v1/ventas` | Lista todas las ventas. |
| `GET` | `/api/v1/ventas/{idVenta}` | Obtiene una venta por ID. |
| `POST` | `/api/v1/ventas` | Crea una venta. |
| `PUT` | `/api/v1/ventas/{idVenta}` | Actualiza una venta existente. |
| `DELETE` | `/api/v1/ventas/{idVenta}` | Elimina una venta. |

Ejemplo de payload:

```json
{
  "direccionCompra": "Av. Siempre Viva 742",
  "valorCompra": 25990,
  "fechaCompra": "2026-05-15",
  "despachoGenerado": false
}
```

### Despachos

| Metodo | Endpoint | Descripcion |
| --- | --- | --- |
| `GET` | `/api/v1/despachos` | Lista todos los despachos. |
| `GET` | `/api/v1/despachos/{idDespacho}` | Obtiene un despacho por ID. |
| `POST` | `/api/v1/despachos` | Crea un despacho. |
| `PUT` | `/api/v1/despachos/{idDespacho}` | Actualiza un despacho existente. |
| `DELETE` | `/api/v1/despachos/{idDespacho}` | Elimina un despacho. |

Ejemplo de payload:

```json
{
  "fechaDespacho": "2026-05-16",
  "patenteCamion": "ABCD12",
  "intento": 1,
  "idCompra": 10,
  "direccionCompra": "Av. Siempre Viva 742",
  "valorCompra": 25990,
  "despachado": false
}
```

## Documentacion Swagger

Cada servicio expone Swagger UI en:

```text
http://localhost:<PUERTO>/swagger-ui.html
```

Ejemplos:

```text
http://localhost:8081/swagger-ui.html
http://localhost:8082/swagger-ui.html
```

## Build y pruebas

Compilar un servicio:

```powershell
.\mvnw.cmd clean package
```

Ejecutar pruebas:

```powershell
.\mvnw.cmd test
```

## Flujo Git

La estrategia de ramas esta documentada en `GIT_FLOW.md`.

- `main`: version estable.
- `develop`: integracion de cambios.
- `deploy`: preparacion de despliegues.

Todo cambio debe ingresar mediante Pull Request y pasar validaciones antes de mergear.
