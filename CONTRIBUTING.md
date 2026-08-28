# Contributing to elearn-platform

Thank you for contributing to the `elearn-platform` LMS repository. This guide covers our monorepo structure, development workflow, branching model, commit conventions, pull request standards, and security policies.

---

## 1. Getting Started & Monorepo Structure

The repository is organized into independent application directories:

```text
elearn-platform/
├── apps/
│   ├── api/   # Spring Boot 3 REST API backend (Java 17 / Maven)
│   └── web/   # Next.js 16 web frontend (React 19 / TypeScript / Tailwind CSS)
├── docs/      # Architecture, development, security, and ADR documentation
└── .github/   # PR templates and workflows
```

Each application operates independently with its own build tools and dependencies. Navigate into the specific application folder to run tasks:

- **Backend development**: Work in `apps/api/` using Maven wrapper (`./mvnw` or `.\mvnw.cmd`).
- **Frontend development**: Work in `apps/web/` using `npm`.

For full environment setup details, see [docs/development/setup.md](docs/development/setup.md).

---

## 2. Branching Strategy

All work should be performed on descriptive feature or fix branches created from the base branch (`dev` or `main` depending on repository setup). Do not push directly to primary branches.

### Branch Naming Conventions
- `feature/<feature-name>` (e.g., `feature/course-enrollment`, `feature/student-dashboard`)
- `fix/<issue-name>` (e.g., `fix/login-validation`, `fix/course-permission`)
- `refactor/<scope>` (e.g., `refactor/course-service`)
- `docs/<topic>` (e.g., `docs/api-guidelines`, `docs/architecture-update`)
- `test/<scope>` (e.g., `test/enrollment-tests`)
- `chore/<task>` (e.g., `chore/dependency-update`)

---

## 3. Commit Conventions

We follow Conventional Commits format to keep git history clean, readable, and structured:

```text
<type>(<optional scope>): <description>

[optional body]

[optional footer(s)]
```

### Types
- `feat`: A new user-facing or API feature
- `fix`: A bug fix
- `refactor`: Code refactoring that neither fixes a bug nor adds a feature
- `test`: Adding or updating tests
- `docs`: Documentation changes only
- `chore`: Build tasks, configuration, or minor maintenance

### Examples
- `feat(api): add course enrollment REST endpoint`
- `fix(web): validate assignment submission form inputs`
- `refactor(api): simplify course lookup in CourseService`
- `test(api): add unit tests for JWT authentication filter`
- `docs: update developer setup and architecture guidelines`

---

## 4. Pull Request (PR) Workflow

1. **Keep PRs Focused**: One feature or bug fix per PR. Avoid combining unrelated refactoring into functional PRs.
2. **Use PR Template**: Complete the [.github/PULL_REQUEST_TEMPLATE.md](.github/PULL_REQUEST_TEMPLATE.md) including summary, changes, testing performed, and breaking changes.
3. **Verify Locally First**: Ensure all tests, linters, and production builds pass before requesting review.
4. **Highlight Breaking Changes**: Clearly call out any schema alterations, configuration updates, or API endpoint contract shifts.

---

## 5. Code Review Expectations

### For Authors
- Provide clear context and reproduction steps if fixing an issue.
- Respond promptly and constructively to review feedback.
- Keep commits organized and readable.

### For Reviewers
- Review for adherence to [Coding Standards](docs/development/coding-standards.md) and [Security Guidelines](docs/security/security-guidelines.md).
- Verify tests cover both happy paths and edge cases.
- Focus on correctness, performance, maintainability, and clean architecture.

---

## 6. Testing & Quality Verification

Before submitting code:

### Backend (`apps/api`)
```bash
cd apps/api
./mvnw clean test
```
*(Windows: `.\mvnw.cmd clean test`)*

### Frontend (`apps/web`)
```bash
cd apps/web
npm run lint
npm run build
```

---

## 7. Security Policy

- **Never Commit Secrets**: Do not commit API keys, database passwords, JWT secrets, credentials, certificates, or private keys.
- **Environment Variables**: Use `.env.example` templates for local configuration and inject actual secrets via environment variables.
- **Input Validation**: Validate all inputs at controller and DTO boundaries.
- For complete security guidance, refer to [docs/security/security-guidelines.md](docs/security/security-guidelines.md).

---

## 8. Documentation Updates

If your pull request alters:
- API endpoints or payload contracts
- System architecture or data flow
- Database schema or entity relationships
- Security configuration or authentication flow
- Developer setup procedures

You **must** update the corresponding documentation under `docs/` as part of the same PR.
