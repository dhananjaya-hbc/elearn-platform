# Coding Standards & Guidelines

This document outlines the coding standards, structure conventions, and architectural best practices for both `apps/api` (Spring Boot) and `apps/web` (Next.js).

---

## 1. General Principles

- **Clarity Over Cleverness**: Write readable, maintainable code rather than obscure one-liners.
- **Single Responsibility Principle**: Classes, services, functions, and components should have a single well-defined purpose.
- **Avoid Premature Abstraction**: Do not invent generic frameworks or deep inheritance hierarchies before multiple concrete use cases exist.
- **No Unused Code or Dead Imports**: Keep files clean; remove obsolete variables, functions, and commented-out code blocks.
- **Consistent Naming**: Use clear, descriptive names that reflect business domains.

---

## 2. Backend Standards (`apps/api` — Spring Boot)

### Layered Architecture & Responsibilities

```text
Controller Layer  (HTTP endpoints, request mapping, validation)
      │
Service Layer     (Business logic, domain rules, transaction control)
      │
Repository Layer  (Spring Data JPA queries, database interactions)
```

1. **Controllers**:
   - Must not contain business logic or entity transformation algorithms.
   - Must validate incoming requests using `@Valid` on request bodies.
   - Return standardized `ResponseEntity<T>` responses with appropriate HTTP status codes (e.g., `200 OK`, `201 Created`, `204 No Content`, `400 Bad Request`, `404 Not Found`).

2. **Services**:
   - Enforce domain rules, coordinate repository queries, and map between entities and DTOs.
   - Annotate mutating methods with `@Transactional`.
   - Throw typed business exceptions when invariant violations occur.

3. **Repositories**:
   - Extend Spring Data JPA interfaces (`JpaRepository<T, ID>`).
   - Use derived query methods or JPQL queries (`@Query`) for complex data retrieval.

4. **DTOs (Data Transfer Objects)**:
   - Always decouple external API contracts from internal database `@Entity` models.
   - Do not expose JPA entities directly in controller return types.
   - Use Jakarta Validation annotations (`@NotBlank`, `@NotNull`, `@Size`, `@Email`, `@Min`, `@Max`).

5. **Dependency Injection**:
   - Use constructor injection via Lombok's `@RequiredArgsConstructor`.
   - Do not use `@Autowired` field injection.

6. **Error & Exception Handling**:
   - Centralize API exception handling using `@RestControllerAdvice` and `@ExceptionHandler`.
   - Return structured error responses containing timestamp, status code, error message, and validation details.

7. **Logging**:
   - Use `@Slf4j` for logging.
   - Use appropriate log levels (`DEBUG` for diagnostic info, `INFO` for significant events, `WARN` for recoverable issues, `ERROR` for unexpected failures).
   - Never log passwords, tokens, or personal identifiable information (PII).

---

## 3. Frontend Standards (`apps/web` — Next.js & React)

### Component Boundaries & App Router

1. **Server vs. Client Components**:
   - Default to **React Server Components (RSC)** for data fetching, static layout rendering, and SEO performance.
   - Mark components with `'use client'` only when they require React hooks (`useState`, `useEffect`, `useCallback`), event listeners, or browser-only APIs.
   - Push client component boundaries as far down the component tree as possible.

2. **TypeScript Best Practices**:
   - Always define types or interfaces for props, API responses, and state models.
   - Avoid using `any`; prefer `unknown` with type guards if the type is truly dynamic.
   - Place shared types in a dedicated `types/` directory under `src/`.

3. **Directory & File Conventions**:
   - Use Next.js App Router conventions:
     - `page.tsx`: Page entry point for a route
     - `layout.tsx`: Persistent layout wrapping child pages
     - `loading.tsx`: Loading skeleton state using React Suspense
     - `error.tsx`: Client-side error boundary
     - `not-found.tsx`: 404 page representation
   - Use path aliases: `@/*` mapped to `./src/*`.

4. **UI & Styling**:
   - Use Tailwind CSS utility classes.
   - Group styling cleanly and avoid huge inline style strings where reusable component abstractions are appropriate.
   - Maintain accessibility (semantic HTML elements, `aria-*` attributes, focus outlines, keyboard navigability).

5. **Asynchronous Handling & UX**:
   - Always account for loading, empty, and error states in UI workflows.
   - Avoid unhandled promise rejections.
