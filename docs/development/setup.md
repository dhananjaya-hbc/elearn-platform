# Developer Setup Guide

This guide describes how to configure your local development environment and run both the Spring Boot backend (`apps/api`) and the Next.js frontend (`apps/web`).

---

## 1. Prerequisites

Ensure you have the following installed on your machine:

- **Git**: `>= 2.30`
- **Java Development Kit (JDK)**: `17` (e.g., Eclipse Temurin, OpenJDK, or Amazon Corretto)
- **Node.js**: `>= 20.9.0` (LTS recommended)
- **npm**: `>= 10.0.0`
- **Database**: PostgreSQL (when running backend with a local database)

> Note: A global Maven installation is not strictly required because the backend includes the official Maven wrapper (`./mvnw` / `.\mvnw.cmd`).

---

## 2. Setting Up the Backend (`apps/api`)

### Running the Backend

Navigate to the `apps/api` directory:

#### Linux / macOS
```bash
cd apps/api
./mvnw spring-boot:run
```

#### Windows (PowerShell / Command Prompt)
```powershell
cd apps\api
.\mvnw.cmd spring-boot:run
```

### Compiling & Packaging the Backend

#### Linux / macOS
```bash
cd apps/api
./mvnw clean compile
./mvnw clean package
```

#### Windows (PowerShell / Command Prompt)
```powershell
cd apps\api
.\mvnw.cmd clean compile
.\mvnw.cmd clean package
```

---

## 3. Setting Up the Frontend (`apps/web`)

### Installing Dependencies

Navigate to the `apps/web` directory:

```bash
cd apps/web
npm install
```

### Running the Development Server

```bash
cd apps/web
npm run dev
```

The application will be accessible at [http://localhost:3000](http://localhost:3000).

### Building for Production

```bash
cd apps/web
npm run build
```

### Running Production Build Locally

```bash
cd apps/web
npm run start
```

### Linting

```bash
cd apps/web
npm run lint
```

---

## 4. Running Commands from Repository Root

If you prefer to execute commands from the repository root without changing directories:

- **Frontend dev**: `npm --prefix apps/web run dev`
- **Frontend build**: `npm --prefix apps/web run build`
- **Backend compile (Windows)**: `.\apps\api\mvnw.cmd -f apps/api/pom.xml clean compile`
- **Backend compile (Unix)**: `./apps/api/mvnw -f apps/api/pom.xml clean compile`
