# Contributing Guidelines

Thank you for contributing to the Learning Management System (LMS) platform.

## Repository Structure

This repository is structured as a monorepo:
- `apps/api`: Spring Boot REST API backend
- `apps/web`: Web frontend application
- `docs/`: System documentation and architecture decisions
- `.github/workflows`: CI/CD pipelines

## Development Workflow

1. Create a feature branch from `dev` (e.g., `feature/feature-name` or `fix/issue-name`).
2. Make targeted changes within the relevant application (`apps/api` or `apps/web`).
3. Ensure all tests and build commands pass before opening a Pull Request.
4. Keep PRs focused and well-documented.
