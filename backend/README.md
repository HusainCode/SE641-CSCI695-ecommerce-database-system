# Backend Development Guide

The backend is a REST API built with:

- Java 21
- Spring Boot 3.5.x
- Maven
- Spring Data JPA / Hibernate
- MySQL
- REST APIs

This guide explains how the backend is organized and how to add new code
consistently.

## Backend Architecture

Standard request flow:

```text
Client
  ↓
Controller
  ↓
Service
  ↓
Repository
  ↓
MySQL
```

Follow this flow unless there is a clear, discussed reason not to.

## Package Responsibilities

```text
src/main/java/edu/stcloudstate/se641/ecommerce/
├── config/
├── controller/
├── dto/
├── entity/
├── exception/
├── repository/
└── service/
```

**`controller/`**
- REST API endpoints
- Handles HTTP requests and responses
- Calls the service layer
- Should **not** contain database access or significant business logic

**`service/`**
- Business logic
- Coordinates application operations
- Calls repositories

**`repository/`**
- Spring Data JPA repositories
- Database access only

**`entity/`**
- JPA entities
- Represents database tables and relationships

**`dto/`**
- API request and response objects
- Do not expose entities directly through the API when a DTO is
  appropriate

**`config/`**
- Spring configuration

**`exception/`**
- Custom exceptions
- Global API exception handling

## How to Add a New Backend Feature

Example only — walking through a hypothetical `Product` feature to show
the order and responsibility of each file. **Do not create these files**;
this is documentation, not a task.

1. **`entity/Product.java`** — defines the `Product` JPA entity and its
   mapping to the database table.
2. **`dto/ProductRequest.java`** / **`dto/ProductResponse.java`** —
   define the shape of data accepted from and returned to API clients.
3. **`repository/ProductRepository.java`** — Spring Data JPA interface
   for querying/persisting `Product` entities.
4. **`service/ProductService.java`** — business logic (validation,
   calculations, orchestration) that uses the repository.
5. **`controller/ProductController.java`** — REST endpoints that accept
   HTTP requests and delegate to `ProductService`.
6. **Tests** — unit/integration tests for the new service and controller
   behavior.

### Example Feature Structure

```text
entity/
└── Product.java

dto/
├── ProductRequest.java
└── ProductResponse.java

repository/
└── ProductRepository.java

service/
└── ProductService.java

controller/
└── ProductController.java
```

Again: documentation only. Do not create these files as part of the
foundation work.

## Coding Standards

Follow:

- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
- Spring Boot conventions
- Basic SOLID principles

| Element | Convention | Example |
| --- | --- | --- |
| Classes | `PascalCase` | `ProductController`, `ProductService`, `ProductRepository` |
| Methods | `camelCase` | `findProductById()`, `createProduct()`, `updateInventory()` |
| Variables | `camelCase` | `productId`, `orderTotal` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_CART_SIZE` |
| Packages | lowercase | `controller`, `service`, `repository` |

## Spring Boot Rules

- Keep controllers thin.
- Put business logic in services.
- Put database access in repositories.
- Prefer constructor injection.
- Do not directly access repositories from controllers.
- Do not put SQL/database logic in controllers.
- Keep classes focused on one responsibility.
- Avoid duplicate code.
- Use meaningful names.
- Do not create unnecessary abstractions.
- Do not create random packages.
- Before adding a new package, determine whether the code belongs in an
  existing package.
- Discuss major architecture changes with the team first.

## REST API Conventions

Documentation examples only — not yet implemented:

```text
GET    /api/products
GET    /api/products/{id}
POST   /api/products
PUT    /api/products/{id}
DELETE /api/products/{id}
```

- Use plural resource names.
- Use appropriate HTTP methods.
- Use appropriate HTTP status codes.
- Keep endpoint naming consistent across the project.

## Database Rules

- Entities belong in `entity/`.
- Repositories belong in `repository/`.
- Use Spring Data JPA for database access.
- Relationships should match our approved database design.
- Do not make database schema changes without considering how they
  affect other teammates.
- Do not hardcode database credentials.
- Never commit passwords or secrets.

## Testing

Backend tests belong in:

```text
src/test/java/edu/stcloudstate/se641/ecommerce/
```

Tests should follow the same package organization as the production code
where practical.

## Before Adding Code

Ask yourself:

1. Which layer does this code belong to?
2. Does a package for it already exist?
3. Am I putting business logic in the service layer?
4. Am I keeping database access in the repository layer?
5. Am I following the existing naming/style conventions?
6. Does this change affect the database schema or another teammate's
   work?

## Git Workflow

```text
Create Branch
     ↓
Make Changes
     ↓
Test Changes on Your Branch
     ↓
Commit & Push Branch
     ↓
Submit Pull Request (PR)
     ↓
Merge into main
```

**The most important rule: never merge changes into `main` before
verifying that your changes work correctly on your own branch.**

1. Create a separate branch for your work. Never develop directly on
   `main`.
2. Make your changes on that branch.
3. Before submitting/merging the PR, run `./mvnw clean test` (or
   `mvnw.cmd clean test` on Windows) and verify your changes build and
   pass.
4. If something is broken, fix it on your branch first. Do not merge
   broken code into `main`.
5. Commit and push your working branch.
6. Submit a Pull Request from your branch into `main`.
7. Merge the PR only after confirming the branch builds and tests pass.

This keeps `main` stable and prevents one teammate's unfinished or
broken changes from breaking the project for everyone.

## Before Opening a Pull Request

- [ ] Code is in the correct package.
- [ ] Naming conventions are followed.
- [ ] No secrets or credentials were committed.
- [ ] No unnecessary files were added.
- [ ] No unrelated code was changed.
- [ ] Backend builds successfully.
- [ ] Tests pass.
- [ ] Code is readable and formatted consistently.

Build and test using the Maven wrapper already included in this repo:

**Linux/macOS/WSL:**

```bash
./mvnw clean test
```

**Windows:**

```bash
mvnw.cmd clean test
```
