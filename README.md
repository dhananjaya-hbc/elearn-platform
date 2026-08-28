# Learning Management System (LMS) - Monorepo

A modern, scalable Learning Management System (LMS) designed for educational institutions, instructors, and students.

## Monorepo Architecture

This repository is organized as a lightweight application monorepo:

```text
elearn-platform/
├── apps/
│   ├── api/                  # Spring Boot 3 REST API backend
│   │   ├── .mvn/
│   │   ├── src/
│   │   ├── mvnw
│   │   ├── mvnw.cmd
│   │   └── pom.xml
│   └── web/                  # Web application frontend (to be initialized)
│
├── docs/
│   └── architecture/         # Architectural documentation and design records
│
├── .github/
│   └── workflows/            # CI/CD automated pipelines
│
├── .gitignore
├── AGENT.md
├── CONTRIBUTING.md
├── README.md
└── docker-compose.yml
```

## Applications

- **[apps/api](apps/api)**: Spring Boot 3 REST API backend providing authentication, course management, enrollments, and core business services.
- **[apps/web](apps/web)**: Web frontend interface for students, instructors, and administrators (pending initialization).

## Getting Started

### Backend (`apps/api`)

To build and run the Spring Boot API locally:

```bash
cd apps/api
./mvnw clean package
./mvnw spring-boot:run
```

On Windows (PowerShell / Command Prompt):
```powershell
cd apps\api
.\mvnw.cmd clean package
.\mvnw.cmd spring-boot:run
```
