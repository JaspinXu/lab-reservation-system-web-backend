# Laboratory Reservation System — Backend

A Spring Boot REST API for laboratory scheduling and administration, with token-based access checks, granular operator privileges, MyBatis persistence, and OpenAPI documentation.

This repository is the backend half of a full-stack course project. The matching React frontend is available at [lab-reservation-system-web-frontend](https://github.com/JaspinXu/lab-reservation-system-web-frontend).

## Highlights

- Laboratory, semester, and schedule management.
- Administrator accounts with module-level privileges.
- Token validation through request filters and AOP-based permission checks.
- Login-log and online-user tracking.
- Paginated query DTOs and consistent response models.
- Excel import/export utilities built with Apache POI.
- Interactive API documentation through Springdoc OpenAPI.

## Tech stack

| Area | Technology |
|---|---|
| Runtime | Java 21 |
| Framework | Spring Boot 3.2 |
| Persistence | MyBatis 3, MySQL |
| API docs | Springdoc OpenAPI 3 |
| Build | Gradle Wrapper |
| Utilities | Lombok, Fastjson2, Apache POI |

## Architecture

```text
HTTP request
    ↓
TokenFilter / TokenCheckAspect
    ↓
Controller → Service → Mapper → MySQL
    ↓
ResponseData / view object
```

The codebase separates transport DTOs, persistence models, view objects, service interfaces, implementations, and MyBatis mappers.

## Getting started

### Prerequisites

- JDK 21
- MySQL 8

### 1. Create the database

Create a database named `demo`, then import the sample schema and data:

```bash
mysql -u root -p demo < data/demo.sql
```

### 2. Configure the connection

Update the datasource values in `src/main/resources/application.properties` for your local MySQL instance. Do not use the example credentials in a deployed environment.

### 3. Start the API

On macOS or Linux:

```bash
./gradlew bootRun
```

On Windows:

```powershell
.\gradlew.bat bootRun
```

The service starts on `http://localhost:9311`. OpenAPI documentation is available at:

- Swagger UI: `http://localhost:9311/swagger-ui/index.html`
- OpenAPI JSON: `http://localhost:9311/v3/api-docs`

## Main API areas

| Controller | Responsibility |
|---|---|
| `AuthenticationController` | Login, token creation, and session checks |
| `LabController` | Laboratory records |
| `SemesterController` | Academic-term configuration |
| `ScheduleController` | Reservation schedule workflows |
| `AdminController` | Administrators and privileges |
| `LoginLogController` | Authentication audit records |
| `OnlineUserController` | Active-user monitoring |

Use Swagger UI for the exact routes and request/response schemas generated from the current code.

## Useful commands

```bash
./gradlew test              # run tests
./gradlew build             # build the application
./gradlew mybatisGenerate   # regenerate mapper/model scaffolding
```

## Project structure

```text
src/main/java/redlib/backend/
  controller/     REST endpoints
  service/        Domain services and implementations
  dao/            MyBatis mapper interfaces
  dto/            Request and query objects
  model/          Persistence and shared response models
  vo/             API response views
  filter/         Request wrapping and token filtering
  annotation/     Privilege annotations
  config/         Web, OpenAPI, AOP, and exception configuration
src/main/resources/
  mapper/         MyBatis XML mappings
  application.properties
data/demo.sql     Sample database
```

## Project context

Developed for a software-engineering practicum at Shandong University. It is preserved as a portfolio and learning project; before production use, move secrets to environment variables, replace the original authentication scheme with a maintained security framework, and add deployment-specific hardening.

## License

[Apache-2.0](LICENSE)

