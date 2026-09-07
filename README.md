# E-Commerce Management System

This repository contains the SE641/CSCI 695 E-Commerce Management System
project, developed by a team of graduate students in the Master of Science
in Software Engineering and Master of Science in Computer Science programs
at St. Cloud State University.

The system is a full-stack e-commerce platform: a React/TypeScript frontend
communicating with a Java/Spring Boot REST API backend, backed by a MySQL
relational database. It is designed to support a product catalog, shopping
cart, order processing, inventory management, simulated payments, shipment
tracking, and reporting.

> **Project Status:** Foundational project structure. Application features
> are implemented incrementally by the team — see [Project Roadmap](#project-roadmap).

## Team Members

- Husain Alshaikhamed
- Elias Gomez Marroquin
- Mayu Ebina
- Fairooz Nawar
- Dinesh Sevet

## Start Here

This repository is organized as a **monorepo** with separate frontend and
backend applications.

Before adding or modifying code, read the guide for the area you will be
working on:

- **Backend development:** [backend/README.md](backend/README.md)
  Read this before adding Java/Spring Boot code. It explains the backend
  architecture, package responsibilities, controllers, services,
  repositories, entities, DTOs, REST conventions, database rules,
  testing, and backend coding standards.

- **Frontend development:** [frontend/README.md](frontend/README.md)
  Read this before adding React/TypeScript code. It explains where to
  add pages, components, services, hooks, types, utilities, frontend API
  communication, and frontend coding standards.

- **Repository structure:** [docs/PROJECT_STRUCTURE.md](docs/PROJECT_STRUCTURE.md)
  Read this when you need to understand where files and folders belong,
  or before introducing a new directory.

- **Shared coding guidelines:** [docs/CODING_GUIDELINES.md](docs/CODING_GUIDELINES.md)
  Contains the common coding and naming standards used across the team.

**Do not create random folders or introduce a new project structure
without first checking the appropriate guide above.**

### Documentation Map

```text
README.md                          Project overview, setup, Git workflow, security rules
  |
  +-- backend/README.md            How to add backend code
  |
  +-- frontend/README.md           How to add frontend code
  |
  +-- docs/PROJECT_STRUCTURE.md    Where files/folders belong
  |
  +-- docs/CODING_GUIDELINES.md    Shared coding/naming standards
```

This README covers overall project information, setup, architecture, Git
workflow, and security rules. It intentionally does not repeat the
frontend/backend development guides — see the links above for those.

## Architecture

```text
React Frontend
      |
   REST API
      |
Spring Boot Backend
      |
    MySQL
```

The backend follows a conventional layered architecture:

```text
Controller → Service → Repository → MySQL
```

## Technology Stack

| Layer / Category | Technology |
| --- | --- |
| Frontend | React 19, TypeScript 5.9 |
| Backend | Java 21, Spring Boot 3.5.x |
| Database | MySQL 8.4 LTS |
| API Layer | REST API |
| ORM / Persistence | Spring Data JPA, Hibernate 6.x |
| Build Tool (backend) | Maven 3.9.x |
| Build Tool (frontend) | Vite |
| Version Control | Git, GitHub |
| Project Management | Jira |
| Deployment | Railway |

## Repository Structure

```text
/
├── frontend/
│   ├── README.md               Frontend development guide
│   └── src/                    React + TypeScript application
│
├── backend/
│   ├── README.md               Backend development guide
│   ├── Dockerfile              Backend container image
│   └── src/                    Java + Spring Boot application
│
├── docs/
│   ├── PROJECT_STRUCTURE.md    Repository/folder organization
│   └── CODING_GUIDELINES.md    Shared coding standards
│
├── docker-compose.yml           Runs backend + MySQL together
├── .env.example                 Docker Compose variable names (no real values)
├── README.md                    Main project entry point (this file)
└── .gitignore                   Files that should never be committed
```

- [`frontend/`](frontend/README.md) — React + TypeScript single-page
  application. Talks to the backend only through the REST API.
- [`backend/`](backend/README.md) — Java + Spring Boot REST API and
  business logic. Owns all database access.
- [`docs/`](docs/PROJECT_STRUCTURE.md) — Architecture notes, ER diagrams,
  database documentation, API documentation, and other technical
  reference material.

## Prerequisites

Recommended (Docker-based) setup:

- [Git](https://git-scm.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Node.js and npm](https://nodejs.org/) (for the React frontend)

If you prefer to run the backend without Docker, you will also need:

- [Java 21 (JDK)](https://adoptium.net/)
- [Maven 3.9.x](https://maven.apache.org/) (or use the included Maven
  wrapper `./mvnw` — no local install required)
- [MySQL 8.4](https://dev.mysql.com/downloads/mysql/) (for local database
  development)

## Running the Project with Docker

This project uses Docker for the Spring Boot backend and MySQL so team
members can use a consistent development environment and reduce
environment/configuration differences. **This is the recommended way for
the team to run the backend and database.**

The React frontend is not Dockerized — it continues to run locally with
Node/npm.

### Prerequisites

- [Git](https://git-scm.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Node.js and npm](https://nodejs.org/) (for the frontend)

You do **not** need to install or configure MySQL locally when using the
Docker setup — the `mysql` container handles that.

### 1. Start Backend + MySQL

From the repository root:

```bash
docker compose up --build
```

This starts:

- MySQL 8.4 (with a persistent volume, so data survives restarts)
- The Spring Boot backend

Backend: `http://localhost:8080`

### 2. Start Frontend

In another terminal:

```bash
cd frontend
npm install
npm run dev
```

Frontend: `http://localhost:5173`

### 3. Stop Backend + MySQL

From the repository root:

```bash
docker compose down
```

This stops and removes the containers. The database data itself is kept
in a Docker volume and is not lost.

### Configuration

Docker Compose reads `DB_NAME` and `DB_PASSWORD` from your environment
(or a local `.env` file at the repository root — see
[.env.example](.env.example)). If unset, safe local-only defaults are
used. Never commit a real `.env` file or real credentials.

## Getting Started (Without Docker)

You can also run each application directly on your machine instead of
using Docker. This requires a local MySQL installation. These are the
basic commands to **run** each application. For instructions on
**adding or modifying code**, see [backend/README.md](backend/README.md)
or [frontend/README.md](frontend/README.md).

### Backend (Spring Boot)

```bash
cd backend
./mvnw spring-boot:run
```

The API starts on `http://localhost:8080` by default.

To run tests:

```bash
cd backend
./mvnw test
```

To build a JAR:

```bash
cd backend
./mvnw clean package
```

Database connection settings are read from environment variables (see
[backend/src/main/resources/application.properties](backend/src/main/resources/application.properties)):

| Variable | Purpose | Default |
| --- | --- | --- |
| `DB_URL` | JDBC URL for MySQL | `jdbc:mysql://localhost:3306/ecommerce_db` |
| `DB_USERNAME` | Database username | `root` |
| `DB_PASSWORD` | Database password | *(empty)* |
| `SERVER_PORT` | Port the API listens on | `8080` |

Do not hardcode real credentials anywhere in the repository. Set these as
environment variables in your local shell or IDE run configuration.

### Frontend (React + TypeScript)

```bash
cd frontend
npm install
npm run dev
```

The app starts on `http://localhost:5173` by default.

Other available commands:

```bash
npm run build      # type-check and build for production
npm run lint        # run the linter
npm run preview     # preview a production build locally
```

## Team Development Workflow

When starting a new task:

1. Read this README.
2. Determine whether the task is frontend, backend, database, or
   documentation work.
3. Read the appropriate development guide
   ([backend/README.md](backend/README.md),
   [frontend/README.md](frontend/README.md), or
   [docs/PROJECT_STRUCTURE.md](docs/PROJECT_STRUCTURE.md)).
4. Pull the latest `main` branch.
5. Create a feature/fix/docs branch.
6. Add code using the established project structure.
7. Build/test the affected application.
8. Push the branch.
9. Open a Pull Request into `main`.

### Git Branching

**Nobody should develop directly on `main`.**

Before starting new work:

```bash
git checkout main
git pull
```

Create a branch:

```bash
git checkout -b feature/<feature-name>
```

Examples:

```text
feature/product-catalog
feature/shopping-cart
feature/order-api
feature/inventory-management
```

Bug fixes:

```text
fix/<description>
```

Examples:

```text
fix/cart-total
fix/product-search
```

Documentation:

```text
docs/<description>
```

Example:

```text
docs/api-documentation
```

After making changes:

```bash
git status
git add .
git commit -m "clear description of change"
git push -u origin <branch-name>
```

Then open a Pull Request into `main`.

Before merging:

- Make sure the project builds.
- Review the changed files.
- Resolve merge conflicts.
- Have another teammate review the PR when practical.

Do not force-push shared branches unless the team explicitly agrees.

### Commit Message Style

Keep commit messages short and descriptive:

```text
feat: add product catalog
feat: add order creation endpoint
fix: correct inventory update
docs: update setup instructions
refactor: simplify product service
test: add order service tests
chore: update project configuration
```

## Security / File Rules

The team must **never** commit:

- Passwords, database credentials, API keys, or other secrets
- `.env` files containing real secret values
- `node_modules/`
- Frontend build output (`frontend/dist/`)
- Backend build output (`backend/target/`)
- IDE-specific files (`.idea/`, `.vscode/` local settings)
- OS temporary files (`.DS_Store`, `Thumbs.db`)

These are already excluded via [.gitignore](.gitignore). If new
environment variables are introduced, document their **names** in this
README without including real values.

## Future Database Entities

The application's data model will eventually include:

`CUSTOMER`, `ADDRESS`, `PRODUCT`, `CATEGORY`, `PRODUCT_CATEGORY`,
`INVENTORY`, `CART`, `CART_ITEM`, `ORDER`, `ORDER_ITEM`, `PAYMENT`,
`SHIPMENT`

These are **not yet implemented**. The backend is structured (see
`entity/`, `repository/`) so the team can add them incrementally.

## Project Roadmap

- **Planning and design** — requirements, database schema, ER diagram,
  repository structure *(this foundation)*
- **Database and backend** — MySQL schema, entities, repositories,
  services, CRUD functionality
- **Frontend and API integration** — React UI, REST endpoints, product
  browsing/search
- **E-commerce functionality** — shopping cart, order processing,
  inventory updates, simulated payments and shipments, reporting
- **Testing and improvements** — integration testing, bug fixes, UI
  polish
- **Deployment and documentation** — Railway deployment, sample data,
  final documentation and diagrams

## Project Management

The team uses **Jira** for sprint planning, feature tracking, and bug
reports, and **GitHub** for source control, branches, and pull requests.

## Academic Context

This project is developed as a team class project for **SE641 & CSCI 695**
at **St. Cloud State University**. Although developed in an academic
setting, this repository is structured as an engineering project and
serves as a technical record of the team's application development,
database engineering, API design, system architecture, and collaboration.
