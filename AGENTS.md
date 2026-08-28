# AGENTS.md — Repository-Level AI Agent Guidelines

This document establishes the primary operating principles, repository architecture, coding rules, security guidelines, and verification workflows for AI coding agents operating on the `elearn-platform` LMS repository.

---

## 1. Project Overview

`elearn-platform` is a Learning Management System (LMS) designed for educational institutions, instructors, and students. It is structured as an application-based monorepo containing a modern Next.js web frontend and a Spring Boot REST API backend.

---

## 2. Repository Structure

```text
elearn-platform/
├── .github/
│   ├── workflows/               # CI/CD pipelines
│   └── PULL_REQUEST_TEMPLATE.md # PR submission template
│
├── apps/
│   ├── api/                     # Spring Boot 3 REST API backend
│   │   ├── .mvn/
│   │   ├── src/
│   │   ├── mvnw
│   │   ├── mvnw.cmd
│   │   └── pom.xml
│   │
│   └── web/                     # Next.js 16 (App Router) web frontend
│       ├── public/
│       ├── src/
│       │   └── app/
│       ├── package.json
│       ├── package-lock.json
│       ├── next.config.ts
│       ├── tsconfig.json
│       └── ...
│
├── docs/
│   ├── architecture/            # Architectural design & system boundaries
│   ├── decisions/               # Architecture Decision Records (ADRs)
│   ├── development/             # Setup, coding standards, testing, & git workflow
│   └── security/                # Security rules & governance
│
├── .gitattributes
├── .gitignore
├── AGENTS.md
├── CONTRIBUTING.md
└── README.md
```

---

## 3. Technology Stack

### Backend (`apps/api`)
- **Framework**: Spring Boot 3.2.x
- **Language**: Java 17
- **Security**: Spring Security + JWT
- **Database**: PostgreSQL
- **ORM / Persistence**: Spring Data JPA + Hibernate
- **Validation**: Jakarta Validation (`@Valid`, constraints)
- **Build Tool**: Maven (with `mvnw` wrapper)
- **Utilities**: Lombok

### Frontend (`apps/web`)
- **Framework**: Next.js 16.x (App Router)
- **Library**: React 19.x
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Linting**: ESLint
- **Package Manager**: npm

---

## 4. Architectural Boundaries

```text
Next.js Web Frontend (apps/web)
          │
          │  HTTP / REST API (JSON)
          ▼
Spring Boot Backend (apps/api)
          │
          │  JPA / SQL
          ▼
      Database
```

- **Frontend Responsibility**: UI rendering, client-side interaction, routing, presentation state, and communicating with the Spring Boot backend via HTTP/REST.
- **Backend Responsibility**: Core business logic, domain rules, authentication, authorization, input validation, transaction management, data persistence, and REST endpoints.
- **Strict Boundary**: The Next.js web application must **never** directly access the database. The Spring Boot application is the single source of truth for business logic and data persistence.
- **Monorepo Isolation**: Dependencies for `apps/web` live exclusively in `apps/web/package.json`. Backend dependencies live exclusively in `apps/api/pom.xml`. Do not add a root `package.json` or workspace manager.

---

## 5. Agent Action Classification

### Safe For Agents to Perform Autonomously
- Implementing assigned user stories, features, or bug fixes within scope.
- Writing unit, service, integration, and component tests.
- Updating or creating documentation and ADRs.
- Focused, small-scope refactorings that preserve public API contracts and behaviors.
- Code formatting, linting fixes, and type error resolutions.
- Running build and verification commands (`npm run build`, `.\mvnw.cmd clean compile`).

### Requires Explicit Human / Team Approval
- Modifying overall repository architecture or monorepo tools.
- Introducing new core frameworks or replacing existing ones.
- Adding major third-party dependencies or external service integrations.
- Modifying authentication/authorization paradigms or security architecture.
- Making breaking changes to REST API endpoints or request/response contracts.
- Destructive database migrations or irreversible schema modifications.
- Changing CI/CD deployment pipelines or cloud infrastructure.
- Deleting existing functional capabilities.

---

## 6. General Development Principles & Code Rules

1. **Inspect Before Modifying**: Always read and understand existing files, directory structures, and conventions before editing or generating code.
2. **Follow Existing Patterns**: Maintain established directory layouts, naming schemes, and design patterns.
3. **No Unnecessary Abstractions**: Do not introduce excessive layers, design patterns, or boilerplate unless they solve a concrete, immediate problem.
4. **Focused Diffs**: Keep changes minimal and directly relevant to the task. Do not touch unrelated files or execute opportunistic large-scale formatting sweeps.
5. **Preserve Integrity**: Do not rewrite working code simply for personal preference or stylistic variants.
6. **No Placeholder Code**: Avoid inserting dummy `TODO: implement later` blocks in production paths without explicit agreement.

---

## 7. Backend (`apps/api`) Specific Rules

- **Package Structure**: Follow standard layer conventions (`controller`, `service`, `repository`, `dto`, `entity`, `exception`, `config`).
- **Lombok Usage**: Use annotations (`@Getter`, `@Setter`, `@Builder`, `@RequiredArgsConstructor`, `@Slf4j`).
- **Dependency Injection**: Use constructor injection via `@RequiredArgsConstructor`. Avoid field injection (`@Autowired`).
- **Validation**: Place `@Valid` on request bodies and define constraints on DTOs.
- **Transactions**: Annotate mutating service methods with `@Transactional`.
- **Controllers**: Controllers must delegate business logic to services and return `ResponseEntity<T>`.
- **Security & Passwords**: Never return raw or hashed passwords in API responses. Always hash passwords with `BCryptPasswordEncoder` before persistence.
- **Logging**: Use `@Slf4j` logger for informative and error logging. Avoid `System.out.println`.

---

## 8. Frontend (`apps/web`) Specific Rules

- **Component Boundaries**: Default to React Server Components (RSC) where possible. Only mark components with `'use client'` when state, event handlers, or browser APIs are required.
- **Type Safety**: Avoid `any`. Define clear TypeScript interfaces and types for API responses and component props.
- **Styling**: Use Tailwind CSS utility classes and design tokens consistent with the UI.
- **Path Aliases**: Use `@/*` imports mapped to `./src/*`.
- **Next.js Conventions**: Follow Next.js App Router file-system conventions (`page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`, `not-found.tsx`).

---

## 9. Dependency & Database Governance

- **Adding Dependencies**: Do not install libraries without clear justification and alignment with the project architecture.
- **Database Schema Changes**: Schema changes must be backward compatible, well-documented, and coordinated with entity mapping definitions.
- **No Direct DB Access from Web**: All database operations must go through Spring Data JPA in `apps/api`.

---

## 10. Security Rules

- **Zero Secrets in Code**: Never hardcode or commit credentials, API keys, JWT secrets, passwords, or private keys.
- **Environment Configuration**: Reference environment variables for secret configuration (`application.properties` with environment substitutions, `.env.local` for Next.js).
- **Input Sanitization**: Validate all inputs at the API gateway / controller layer.
- **Safe Logging**: Never log sensitive user credentials, tokens, or PII.

---

## 11. Verification & Quality Assurance

Before concluding any task or declaring completion, agents must:

1. **Verify Backend**: Run the Maven compilation and test suite from `apps/api`:
   ```bash
   cd apps/api
   ./mvnw clean compile test
   ```
   *(On Windows: `.\mvnw.cmd clean compile test`)*

2. **Verify Frontend**: Run linting and production build from `apps/web`:
   ```bash
   cd apps/web
   npm run lint
   npm run build
   ```

3. **Check Monorepo Cleanliness**: Run `git status` to ensure no temporary artifacts, untracked debris, or unintended file modifications remain.
4. **Report Findings**: Transparently report compilation results, test outputs, architectural assumptions, and any potential edge cases to the user.