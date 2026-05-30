# DevOps Documentation

## 1. Introduction

The DevOps setup for Budapesti defines how the application is containerised and run in a reproducible way across different environments (developer machines, CI/CD pipelines, staging, production). It uses **Docker** and **Docker Compose** to manage the backend and frontend services together.

---

## 2. Objective

The goal of the DevOps configuration is to:

- Ensure every developer runs the application in the same environment
- Eliminate "it works on my machine" problems
- Provide a simple single command to start the whole stack
- Prepare the project for deployment to any cloud platform

---

## 3. Technologies Used

| Technology       | Purpose                                                    |
|------------------|------------------------------------------------------------|
| Docker           | Containerises each service (backend, frontend)             |
| Docker Compose   | Orchestrates multiple containers as a single application   |
| `.env` files     | Manage environment-specific configuration (ports, secrets) |

---

## 4. Project Structure Explanation

```
docker/
├── docker-compose.yml   # Defines all services, networks, and port mappings
└── .env.example         # Template for environment variables (copy to .env)
```

**docker-compose.yml** describes the full application stack:
- The `backend` service builds and runs the Spring Boot JAR.
- The `frontend` service builds and serves the React app.
- Both services are connected through a shared Docker network (`budapesti-net`) so they can communicate internally.

**.env.example** lists all required environment variables with safe default values. Developers copy this file to `.env` (which is git-ignored) and customise it for their environment.

---

## 5. How It Works (High-Level)

1. A developer copies `.env.example` to `.env` and adjusts values if needed.
2. Running `docker compose up --build` from the `docker/` folder:
   - Builds the backend Docker image using the `backend/Dockerfile`.
   - Builds the frontend Docker image using the `frontend/Dockerfile`.
   - Starts both containers and connects them to the shared network.
3. The backend is available at `http://localhost:8080`.
4. The frontend is available at `http://localhost:3000`.
5. Environment variables defined in `.env` are injected into each service at startup.

---

## 6. Design Decisions

- **Docker Compose** is used instead of running services manually because it allows the entire stack to be started with a single command and ensures consistent configuration.
- **Environment variables** are externalised using `.env` files so that secrets and configuration are never hard-coded in source files.
- **`.env.example`** is committed to git so developers know which variables are required, while the actual `.env` is git-ignored to prevent secrets from being committed.
- **A shared Docker network** (`budapesti-net`) allows containers to communicate using service names (e.g. `http://backend:8080`) rather than `localhost`, which only works within the same container.

---

## 7. Best Practices

- **Never commit `.env` to git** — add it to `.gitignore`. Only commit `.env.example`.
- **Use specific image versions** in `docker-compose.yml` (e.g. `postgres:16`) instead of `latest` to ensure reproducible builds.
- **Keep `docker-compose.yml` for development** — use a separate `docker-compose.prod.yml` for production overrides.
- **Separate build-time and runtime configuration** — environment variables injected at runtime are more secure than baked into the image.
- **Add health checks** to services so Docker knows when a container is ready before routing traffic to it.
- **Use multi-stage Docker builds** for production images to reduce image size (build in one stage, copy only the output to the final stage).
