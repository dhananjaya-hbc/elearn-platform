# Security Guidelines & Governance

This document defines core security practices, vulnerability prevention measures, and governance rules for `elearn-platform`.

---

## 1. Secrets & Sensitive Data Management

- **No Hardcoded Secrets**: Under no circumstances should passwords, API keys, JWT secret keys, cloud credentials, or TLS certificates be committed to Git.
- **Environment Variables**: Configure all secrets through environment variables or secure secret vaults.
- **Git Ignore Safeguards**: Keep `.env`, `.env.local`, and sensitive configuration files in `.gitignore`.
- **Review Requirement**: Any accidental commit containing secrets must be treated as a security incident; the secret must be immediately rotated and revoked.

---

## 2. Authentication & Authorization Governance

- **Centralized Security**: Authentication and role-based access control (RBAC) are owned and enforced exclusively by the Spring Boot backend (`apps/api`) via Spring Security.
- **Stateless Tokens**: Use signed JWT tokens with standard expiration and refresh policies.
- **Strict Endpoint Protection**: All API endpoints must be protected by default; public endpoints (e.g., login, registration, health checks) must be explicitly whitelisted.
- **Password Security**: Passwords must always be hashed with strong adaptive hashing algorithms (such as `BCryptPasswordEncoder`) with adequate work factor before persistence.

---

## 3. Input Validation & Data Sanitization

- **Controller Validation**: All incoming API payloads must be validated using Jakarta Validation (`@Valid` with `@NotBlank`, `@Size`, `@Pattern`, `@Email`, etc.).
- **Injection Prevention**: Use Spring Data JPA parameterized queries and ORM mappings to prevent SQL injection. Never concatenate raw SQL strings.
- **XSS & Content Security**: Sanitize and escape all user-generated content rendered in the Next.js frontend (`apps/web`).

---

## 4. API Security & Error Handling

- **Safe Error Responses**: Do not leak internal system details, stack traces, database schema details, or server infrastructure versions in error responses.
- **CORS Configuration**: Restrict Cross-Origin Resource Sharing (CORS) strictly to authorized frontend origins.
- **Rate Limiting**: Implement rate-limiting on sensitive endpoints (e.g., login, password reset) when in production environments.

---

## 5. Dependency Management

- **Audit Dependencies**: Regularly scan dependencies for known vulnerabilities (`npm audit`, `mvn dependency-check`).
- **Minimal Dependencies**: Only install well-maintained and necessary third-party packages to reduce supply chain risk.

---

## 6. Architecture Review Requirement

> [!IMPORTANT]
> Any proposed change affecting authentication mechanisms, session management, token handling, cryptographic algorithms, or authorization models requires human architecture/security review before implementation.
