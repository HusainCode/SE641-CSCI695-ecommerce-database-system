# Coding Guidelines

Practical coding-style guidance for the team. The goal is a codebase that
reads consistently no matter who wrote a given file — not an elaborate
enterprise architecture.

## Java / Backend

Primary standards:

- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
- Conventional Spring Boot layering (see below)
- Basic SOLID principles, applied pragmatically

### Naming Conventions

| Element | Convention | Example |
| --- | --- | --- |
| Classes | `PascalCase` | `ProductService`, `OrderController`, `CustomerRepository` |
| Methods / variables | `camelCase` | `findProductById`, `orderTotal`, `customerId` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_CART_SIZE` |
| Packages | lowercase | `controller`, `service`, `repository` |

Each Java class should have one clear responsibility. If a class is doing
more than one job, it is a candidate to be split.

### Spring Boot Layering

```text
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

Do **not** call the database directly from a controller:

```text
Controller
    ↓
Database        ✗ not allowed
```

Responsibilities:

- **Controller** — Handles HTTP/API concerns (routing, request/response,
  status codes). Keep controllers thin.
- **Service** — Contains business logic. This is where validation,
  calculations, and orchestration belong.
- **Repository** — Handles persistence/database access via Spring Data
  JPA. No business logic.
- **Entity** — Represents persistent database data (`@Entity` classes).
- **DTO** — Represents API request/response data, decoupling the public
  API contract from internal entity structure.

### General Java Rules

- Use constructor injection for dependency injection (standard Spring
  convention) rather than field injection.
- Use meaningful class, method, and variable names — prefer clarity over
  brevity.
- Avoid extremely large classes and methods; keep methods focused on one
  clear task.
- Avoid duplicated logic — extract shared behavior instead of
  copy-pasting.
- Do not put significant business logic inside controllers.

---

## REST API Conventions

Documented here for future development. **Do not implement these
endpoints yet** — these are naming/format examples only.

```text
GET    /api/products
GET    /api/products/{id}
POST   /api/products
PUT    /api/products/{id}
DELETE /api/products/{id}
```

- Use plural resource names (`/api/products`, not `/api/product`).
- Use the HTTP method that matches the operation's intent (`GET` to read,
  `POST` to create, `PUT` to update, `DELETE` to remove).
- Use appropriate HTTP status codes (`200`, `201`, `204`, `400`, `404`,
  `409`, `500`, etc.).
- Keep endpoint naming consistent across the whole project.

---

## TypeScript / React

### Naming Conventions

| Element | Convention | Example |
| --- | --- | --- |
| Components | `PascalCase` | `ProductCard.tsx`, `ShoppingCart.tsx` |
| Variables / functions | `camelCase` | `productList`, `calculateTotal()` |
| Custom hooks | `camelCase`, prefixed with `use` | `useProducts`, `useCart` |

### General Rules

- Use meaningful names for components, variables, and functions.
- Avoid giant React components — extract reusable UI into `components/`.
- Keep API calls organized under `services/`; do not call `fetch`/`axios`
  directly from components or pages.
- Keep shared TypeScript definitions under `types/`.
- Avoid `any` unless there is a legitimate, documented reason.
- Do not duplicate components or API logic unnecessarily — reuse what
  already exists.

---

## Comments and Readability

- Code should generally explain itself through meaningful names.
- Use comments when they explain **why** something is being done (a
  non-obvious constraint, workaround, or trade-off) — not **what** the
  code does.
- Avoid comments that simply repeat the code.
- Keep formatting consistent with the rest of the file.
- Remove unused imports and dead code before committing.
- Do not leave commented-out blocks of old code in the repository — Git
  history is the place for old code, not comments.
