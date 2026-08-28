# Architecture Overview

This document describes the high-level architecture, component boundaries, and technology structure of the `elearn-platform` Learning Management System (LMS).

---

## 1. High-Level System Architecture

The LMS is designed as a decoupled, multi-tier application contained within a single application monorepo:

```text
┌─────────────────────────────────────────────────────────┐
│               Web Frontend (`apps/web`)                 │
│         Next.js 16 (App Router) • React 19 • TS         │
└────────────────────────────┬────────────────────────────┘
                             │
                             │ HTTPS / REST API (JSON)
                             │ JWT Bearer Tokens
                             ▼
┌─────────────────────────────────────────────────────────┐
│               REST API Backend (`apps/api`)             │
│            Spring Boot 3.2.x • Java 17 • Maven          │
└────────────────────────────┬────────────────────────────┘
                             │
                             │ SQL / Spring Data JPA
                             ▼
┌─────────────────────────────────────────────────────────┐
│                   Database Layer                        │
│                     PostgreSQL                          │
└─────────────────────────────────────────────────────────┘
```

---

## 2. Component Responsibilities

### Web Frontend (`apps/web`)
- **User Interface & UX**: Responsive web interfaces for students, instructors, and administrators.
- **Client Routing & Navigation**: Managed through the Next.js App Router.
- **Presentation State**: Client-side state handling, UI form state, and optimistic updates.
- **API Communication**: Communicates with the Spring Boot backend using standard HTTP/REST endpoints.
- **Server Rendering**: Leveraging React Server Components (RSC) for initial page renders and SEO optimization.
- **Constraint**: The Next.js application **must not** connect directly to the application database.

### API Backend (`apps/api`)
- **Domain Business Logic**: Central authority for core business rules (course progression, grading, access rules, enrollments).
- **Authentication & Authorization**: Identity verification, role-based access control (RBAC), and JWT token management via Spring Security.
- **Data Validation**: Strict payload validation using Jakarta Validation (`@Valid`, custom validators) on DTOs.
- **REST Endpoints**: Secure, standardized JSON API endpoints.
- **Data Persistence**: Managed database interactions via Spring Data JPA and Hibernate entities.
- **Transactional Integrity**: Managing database transactions with `@Transactional`.

### Database Layer
- **Persistent Data Store**: Relational database (PostgreSQL) storing users, courses, modules, assignments, enrollments, and system records.

---

## 3. Monorepo Organization

The codebase is organized into independent application modules:

```text
elearn-platform/
├── apps/
│   ├── api/             # Backend Spring Boot application
│   └── web/             # Frontend Next.js application
├── docs/
│   ├── architecture/    # Architecture overviews & data models
│   ├── decisions/       # Architecture Decision Records (ADRs)
│   ├── development/     # Developer guides, coding standards, testing
│   └── security/        # Security principles & governance
└── .github/
    └── workflows/       # Continuous Integration / Deployment automation
```

### Monorepo Boundaries
- **No Direct Coupling**: The frontend does not import code directly from `apps/api`, and the backend does not depend on `apps/web`.
- **Independent Package Management**: `apps/web` uses `npm` for dependency resolution; `apps/api` uses Maven wrapper (`mvnw`).
- **Separation of Concerns**: Business logic is not duplicated between frontend and backend. The backend defines and enforces all domain invariants.
