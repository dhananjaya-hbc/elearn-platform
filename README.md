# elearn-platform

A modern, scalable Learning Management System (LMS) developed as an application monorepo with a Next.js web frontend and a Spring Boot REST API backend.

---

## 1. Architecture

```text
┌─────────────────────────┐
│       Next.js Web       │
│       (apps/web)        │
└────────────┬────────────┘
             │
             │ HTTP / REST API (JSON)
             ▼
┌─────────────────────────┐
│     Spring Boot API     │
│       (apps/api)        │
└────────────┬────────────┘
             │
             │ SQL / JPA
             ▼
┌─────────────────────────┐
│        Database         │
│      (PostgreSQL)       │
└─────────────────────────┘
```

For complete architectural details, see [Architecture Overview](docs/architecture/overview.md).

---

## 2. Repository Structure

```text
elearn-platform/
├── .github/
│   ├── workflows/               # CI/CD automated pipelines
│   └── PULL_REQUEST_TEMPLATE.md # Pull request submission template
│
├── apps/
│   ├── api/                     # Spring Boot 3 REST API backend
│   │   ├── .mvn/
│   │   ├── src/
│   │   ├── mvnw
│   │   ├── mvnw.cmd
│   │   └── pom.xml
│   │
│   └── web/                     # Next.js 16 (App Router) frontend
│       ├── public/
│       ├── src/
│       │   └── app/
│       ├── package.json
│       ├── next.config.ts
│       ├── tsconfig.json
│       └── ...
│
├── docs/
│   ├── architecture/            # Architecture overview and design
│   ├── decisions/               # Architecture Decision Records (ADRs)
│   ├── development/             # Developer setup, coding standards, testing, and git workflow
│   └── security/                # Security governance and policies
│
├── .gitattributes
├── .gitignore
├── AGENTS.md                    # Repository guidelines for AI coding agents
├── CONTRIBUTING.md              # Contribution guidelines for developers
└── README.md
```

---

## 3. Technology Stack

### Frontend (`apps/web`)
- **Framework**: Next.js 16.x (App Router)
- **Library**: React 19.x
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Linting**: ESLint

### Backend (`apps/api`)
- **Framework**: Spring Boot 3.2.x
- **Language**: Java 17
- **Security**: Spring Security + JWT
- **Database**: PostgreSQL
- **ORM**: Spring Data JPA + Hibernate
- **Validation**: Jakarta Validation
- **Build Tool**: Maven (with wrapper `mvnw`)

---

## 4. Getting Started

Refer to the [Developer Setup Guide](docs/development/setup.md) for full prerequisites and environment configuration.

### Quick Start

#### Run Backend
```bash
cd apps/api
./mvnw spring-boot:run
# Windows: .\mvnw.cmd spring-boot:run
```

#### Run Frontend
```bash
cd apps/web
npm install
npm run dev
```

---

## 5. Contributing & Workflow

- Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting code.
- Follow our [Git Workflow](docs/development/git-workflow.md) and [Coding Standards](docs/development/coding-standards.md).
- AI coding agents must adhere to [AGENTS.md](AGENTS.md).

---

## 6. Documentation Hub

- **[Architecture Overview](docs/architecture/overview.md)**: System design and component boundaries.
- **[Developer Setup](docs/development/setup.md)**: Local machine setup and build instructions.
- **[Coding Standards](docs/development/coding-standards.md)**: Backend and frontend conventions.
- **[Testing Guidelines](docs/development/testing.md)**: Unit, integration, and E2E testing strategies.
- **[Git Workflow](docs/development/git-workflow.md)**: Branching, commit conventions, and PR flow.
- **[Security Guidelines](docs/security/security-guidelines.md)**: Secrets, auth, validation, and vulnerability management.
- **[Architecture Decisions (ADRs)](docs/decisions/README.md)**: Formal record of architectural decisions.
