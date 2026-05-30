# Backend Documentation

## 1. Introduction

The Budapesti backend is a RESTful API built with **Java 21** and **Spring Boot 3**. It is responsible for serving data to the frontend, managing business logic, and persisting information in a database. As the backbone of the application, it processes requests from the user's browser and returns structured responses.

---

## 2. Objective

The goal of the backend is to:

- Expose a clean REST API consumed by the frontend
- Manage domain entities such as Points of Interest (POIs)
- Apply business logic in a modular and testable way
- Persist and retrieve data from a relational database

---

## 3. Technologies Used

| Technology       | Purpose                                      |
|------------------|----------------------------------------------|
| Java 21          | Programming language (latest LTS version)    |
| Spring Boot 3    | Application framework — simplifies setup     |
| Spring Web       | Building REST endpoints                      |
| Spring Data JPA  | Database access using object-relational mapping |
| H2 Database      | In-memory database for development           |
| Maven            | Build tool and dependency manager            |

---

## 4. Project Structure Explanation

```
backend/
├── pom.xml                         # Maven build configuration and dependencies
└── src/
    └── main/
        ├── java/com/budapesti/
        │   ├── BudapestiApplication.java   # Entry point — starts the Spring Boot app
        │   ├── config/                     # Spring configuration beans (e.g. CORS, security)
        │   ├── controller/                 # REST controllers — handle HTTP requests
        │   ├── service/                    # Business logic layer
        │   ├── repository/                 # Database access layer (Spring Data JPA)
        │   ├── domain/                     # JPA entities (database table mappings)
        │   └── dto/                        # Data Transfer Objects (API request/response shapes)
        └── resources/
            └── application.yml            # Application configuration (port, database, etc.)
```

**Why this structure?**  
This follows the standard **layered architecture** pattern in Spring Boot:
- The **controller** receives the request and delegates to the **service**.
- The **service** contains business rules and calls the **repository**.
- The **repository** talks to the database and returns **domain** entities.
- **DTOs** decouple the internal domain model from what is exposed via the API.

---

## 5. How It Works (High-Level)

1. The application starts from `BudapestiApplication.java`, which triggers Spring Boot's auto-configuration.
2. Spring scans all classes annotated with `@RestController`, `@Service`, `@Repository`, etc.
3. When the frontend calls `GET /api/hello`, the request is handled by `HelloController`.
4. The controller returns a response, which Spring automatically serializes to JSON.
5. The H2 in-memory database is available during development at `/h2-console`.

---

## 6. Design Decisions

- **Java 21** is the current LTS (Long-Term Support) version — it is stable, fast, and widely used in production.
- **Spring Boot** reduces boilerplate configuration so you can focus on business logic.
- **H2 in-memory database** is used during development so you do not need to install a database locally. In production, it would be replaced by PostgreSQL or MySQL.
- **application.yml** is preferred over `application.properties` for its more readable, hierarchical format.
- **DTOs** are used to avoid exposing internal entity details directly through the API (separation of concerns).

---

## 7. Best Practices

- **Never expose JPA entities directly** through the API — always map them to DTOs.
- **Keep business logic in the service layer**, not in controllers or repositories.
- **Use constructor injection** instead of field injection (`@Autowired`) for better testability.
- **Validate input** at the controller level using `@Valid` and Bean Validation annotations.
- **Write unit tests** for service classes and integration tests for controllers.
- **Use meaningful HTTP status codes** (200, 201, 400, 404, 500) in your responses.
