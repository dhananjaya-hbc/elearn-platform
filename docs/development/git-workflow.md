# Git Workflow & Collaboration

This document describes the branch strategy, pull request rules, and commit standards for the `elearn-platform` repository.

---

## 1. Branching Strategy

We use a simple, trunk-adjacent branching model designed for continuous collaboration:

```text
main (or dev)
  │
  ├── feature/course-enrollment
  │
  ├── fix/login-validation
  │
  └── refactor/course-service
```

### Primary Branches
- `main` / `dev`: Stable development branch. Direct pushes to primary branches are prohibited for regular feature development.

### Feature & Fix Branches
Create short-lived branches off the main development branch using descriptive names:
- `feature/<feature-name>`: New capabilities or functional enhancements
- `fix/<bug-name>`: Defect repairs and regression fixes
- `refactor/<scope>`: Code refactoring without behavior modification
- `docs/<topic>`: Documentation updates
- `test/<scope>`: Adding or improving tests
- `chore/<task>`: Dependency or toolchain updates

---

## 2. Commit Message Standards

Commits must follow the Conventional Commits specification:

```text
<type>(<scope>): <summary>

[optional description]
```

### Common Types
- `feat`: New feature or endpoint
- `fix`: Bug fix
- `refactor`: Internal restructure without API or functional change
- `docs`: Documentation addition or edit
- `test`: Adding or modifying automated test suites
- `chore`: Toolchain, build configuration, or dependency maintenance

---

## 3. Pull Request Process

1. **Branch Preparation**: Keep your local branch up to date with the target branch before opening a PR (`git rebase` or `git merge`).
2. **Open PR**: Create a PR targeting the development branch.
3. **Template Completion**: Fill out all sections in the [PR Template](../../.github/PULL_REQUEST_TEMPLATE.md).
4. **Peer Review**: At least one code review is required before merging.
5. **No Force-Pushes on Shared Branches**: Never perform force-pushes (`git push --force`) on shared or main branches.
