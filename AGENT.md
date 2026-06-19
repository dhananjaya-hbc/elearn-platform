# AGENT.md - Backend (Spring Boot)

## Project Overview
This is the backend REST API built with Spring Boot 3, Spring Security, and PostgreSQL.
It serves both the web frontend (Next.js) and mobile app (React Native).

## Tech Stack
- **Framework**: Spring Boot 3.2.x
- **Language**: Java 17
- **Security**: Spring Security + JWT
- **Database**: PostgreSQL
- **ORM**: Spring Data JPA + Hibernate
- **Validation**: Spring Validation (Jakarta)
- **Build Tool**: Maven
- **Utilities**: Lombok

## Project Setup

### Generate Project
Go to https://start.spring.io and configure:
```
Project:      Maven
Language:     Java
Spring Boot:  3.2.x
Packaging:    Jar
Java:         17

Dependencies:
- Spring Web
- Spring Security
- Spring Data JPA
- Spring Validation
- PostgreSQL Driver
- Lombok
- Spring Boot DevTools
```
Download and extract the project.

## Code Style Rules
- Use Lombok annotations (@Getter, @Setter, @Builder, @RequiredArgsConstructor, @Slf4j)
- Use @Valid on all request body parameters
- All service methods should be @Transactional where data is modified
- Use constructor injection (via @RequiredArgsConstructor)
- No field injection (@Autowired)
- All endpoints return ResponseEntity
- Log important actions with @Slf4j logger
- Never return password field in any response
- Always encode passwords with BCryptPasswordEncoder before saving