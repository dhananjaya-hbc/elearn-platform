# LMS Monorepo Guidelines for AI & Developers

## Repository Overview
This repository is an LMS (Learning Management System) application monorepo:
- `apps/api`: Backend REST API built with Spring Boot 3, Spring Security, and PostgreSQL.
- `apps/web`: Web application frontend (to be initialized).
- `docs/architecture`: Architecture diagrams, ADRs, and technical specifications.
- `.github/workflows`: Continuous integration and delivery workflows.

---

## Backend (`apps/api`)

### Tech Stack
- **Framework**: Spring Boot 3.2.x
- **Language**: Java 17
- **Security**: Spring Security + JWT
- **Database**: PostgreSQL
- **ORM**: Spring Data JPA + Hibernate
- **Validation**: Spring Validation (Jakarta)
- **Build Tool**: Maven (with Maven wrapper)
- **Utilities**: Lombok

### Code Style Rules
- Use Lombok annotations (`@Getter`, `@Setter`, `@Builder`, `@RequiredArgsConstructor`, `@Slf4j`)
- Use `@Valid` on all request body parameters
- All service methods should be `@Transactional` where data is modified
- Use constructor injection (via `@RequiredArgsConstructor`)
- No field injection (`@Autowired`)
- All endpoints return `ResponseEntity`
- Log important actions with `@Slf4j` logger
- Never return password field in any response
- Always encode passwords with `BCryptPasswordEncoder` before saving