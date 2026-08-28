# Testing Strategy & Guidelines

This document outlines the testing strategy, principles, and execution guidelines for `elearn-platform`.

---

## 1. Testing Philosophy

- **Test Behavior, Not Implementation**: Write tests that verify system outcomes and contracts rather than brittle internal implementation details.
- **Coverage of Critical Paths**: Core business logic (authentication, enrollments, course progression, grading) requires thorough test coverage.
- **Automated Regression Prevention**: Every bug fix should be accompanied by a regression test verifying that the issue cannot recur.
- **Never Disable Tests to Force Builds**: Tests must never be deleted, ignored (`@Disabled`), or bypassed simply to make a CI pipeline or build pass.

---

## 2. Backend Testing (`apps/api`)

The Spring Boot backend adopts a tiered testing approach:

### Unit Tests
- Test domain logic, utility classes, and service methods in complete isolation.
- Mock external dependencies (e.g., repositories or external clients) using Mockito (`@ExtendWith(MockitoExtension.class)`).
- Ensure fast feedback loops without starting the full Spring ApplicationContext.

### Service & Integration Tests
- Test service layer interactions with the database using `@DataJpaTest` or `@SpringBootTest`.
- Validate transactional behavior and cascade rules.

### Controller / API Tests
- Validate HTTP endpoints, request serialization/deserialization, validation errors, and response formatting using `@WebMvcTest` and `MockMvc`.
- Ensure proper status codes and error bodies are returned for invalid inputs.

### Running Backend Tests
```bash
cd apps/api
./mvnw clean test
```
*(Windows: `.\mvnw.cmd clean test`)*

---

## 3. Frontend Testing (`apps/web`)

As frontend features are implemented, testing will encompass:

### Component Tests
- Test reusable UI components in isolation (props rendering, user event triggers, conditional styles).

### Integration Tests
- Test complex form submissions, user journeys, client-side routing, and client-server interactions.

### End-to-End (E2E) Tests
- For critical user flows (e.g., student login, course registration, quiz submission), end-to-end tests will be added when an E2E framework is selected and introduced.

### Running Frontend Validation
```bash
cd apps/web
npm run lint
npm run build
```
*(Test execution commands will be documented here once testing dependencies are officially integrated).*
