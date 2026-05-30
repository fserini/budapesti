# Budapesti

A mobile-first web application for tourists visiting Budapest. Explore points of interest, plan your visits with a personal checklist, and navigate around the city.

---

## Project Overview

| Layer    | Technology                         |
|----------|------------------------------------|
| Backend  | Java 21, Spring Boot 3, Maven      |
| Frontend | React 18, TypeScript, Vite         |
| DevOps   | Docker, Docker Compose             |

The project uses a **monorepo** structure:

```
budapesti/
├── backend/    # Spring Boot REST API
├── frontend/   # React + TypeScript web app
├── docker/     # Docker Compose and environment configuration
└── docs/       # Educational documentation
```

---

## How to Start the Backend

**Prerequisites:** Java 21, Maven 3.9+

```bash
cd backend
./mvnw spring-boot:run
```

The API will be available at `http://localhost:8080`.  
The H2 console (development only) is at `http://localhost:8080/h2-console`.

---

## How to Start the Frontend

**Prerequisites:** Node.js 20+, npm

```bash
cd frontend
npm install
npm run dev
```

The app will be available at `http://localhost:3000`.

---

## How to Start with Docker Compose

**Prerequisites:** Docker Desktop (or Docker + Docker Compose)

```bash
cd docker
cp .env.example .env
docker compose up --build
```

- Backend: `http://localhost:8080`
- Frontend: `http://localhost:3000`

---

## Documentation

Detailed educational documentation for each part of the stack:

- [Backend](docs/backend.md)
- [Frontend](docs/frontend.md)
- [DevOps](docs/devops.md)