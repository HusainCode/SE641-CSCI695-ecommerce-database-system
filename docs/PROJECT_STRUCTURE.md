# Project Structure

This document explains how the repository is organized so that any teammate
can find where code belongs and add new code in a consistent, predictable
place.

## Root Layout

```text
/
├── frontend/     React + TypeScript application
├── backend/      Java + Spring Boot application
├── docs/         Technical and project documentation
├── README.md     Main project setup and development instructions
└── .gitignore    Files that should never be committed
```

### `frontend/`

The React + TypeScript single-page application. Communicates with the
backend exclusively over the REST API — it does not access the database or
any other backend resource directly.

### `backend/`

The Java + Spring Boot REST API and business logic layer. Owns all database
access via Spring Data JPA.

### `docs/`

Technical and project documentation: architecture notes, ER diagrams,
database documentation, API documentation, and other reference material.
Keep documentation close to the code it describes; only project-wide
material belongs here.

### `README.md`

Entry point for the repository. Explains what the project is, how to set up
a development environment, and how to run each application.

### `.gitignore`

Defines which generated files, build artifacts, and local/secret files are
never committed.

---

## Frontend Structure (`frontend/src/`)

```text
src/
├── components/   Reusable React UI components
├── pages/        Page-level React components
├── services/     REST API communication with the backend
├── hooks/        Reusable custom React hooks
├── types/        Shared TypeScript types and interfaces
├── utils/        Reusable frontend helper functions
└── assets/       Images and other static frontend resources
```

**`components/`**
Reusable, presentation-focused UI building blocks (buttons, cards, form
inputs, layout pieces) that can be composed into pages. A component should
not know which page it lives on.

**`pages/`**
Top-level views that correspond to a route (e.g. product catalog page,
cart page, order history page). Pages compose components and call
`services/` for data; they should stay thin.

**`services/`**
All HTTP communication with the Spring Boot backend lives here. Components
and pages should call a service function rather than making `fetch`/`axios`
calls directly. This keeps API logic in one place and easy to change.

**`hooks/`**
Reusable custom React hooks (state, effects, or logic shared across
components/pages). Hook filenames and function names start with `use`.

**`types/`**
Shared TypeScript types/interfaces used across more than one file (e.g. API
response shapes, domain models). Types local to a single component can stay
in that component's file.

**`utils/`**
Small, pure helper functions (formatting, calculations, etc.) with no
framework or API dependencies.

**`assets/`**
Static files such as images, icons, and fonts.

---

## Backend Structure (`backend/src/main/java/.../ecommerce/`)

```text
ecommerce/
├── controller/   REST API controllers and HTTP request/response handling
├── service/      Application business logic
├── repository/   Database access using Spring Data JPA repositories
├── entity/       JPA entities representing database data
├── dto/          Request/response and data-transfer objects
├── config/       Spring/application configuration
└── exception/    Application-specific exceptions and centralized error handling
```

**`controller/`**
Exposes REST endpoints. Handles HTTP concerns only — request parsing,
response status codes, routing to a service. Contains no business logic
and no direct database access.

**`service/`**
Contains the application's business logic. Called by controllers, and in
turn calls repositories. This is where validation, calculations, and
workflow decisions belong.

**`repository/`**
Spring Data JPA repository interfaces for database access. No business
logic here — just persistence.

**`entity/`**
JPA `@Entity` classes that map directly to database tables.

**`dto/`**
Data Transfer Objects used for API request/response payloads, decoupling
the public API shape from internal entity structure.

**`config/`**
Spring configuration classes (beans, CORS, application-wide setup).

**`exception/`**
Custom exception classes and centralized exception handling
(e.g. `@ControllerAdvice`).

Empty directories are tracked with a `.gitkeep` placeholder until real code
is added.

---

## Team Rules

1. Do not create random folders because you are unsure where something
   belongs — ask the team or use the closest existing directory first.
2. Before creating a new directory, determine whether the file belongs in
   an existing directory.
3. New directories must have one clear responsibility.
4. Follow the existing naming conventions (see `CODING_GUIDELINES.md`).
5. Keep frontend and backend concerns separated — no backend code in
   `frontend/`, no frontend code in `backend/`.
6. Do not place business logic in controllers.
7. Do not access the database directly from controllers.
8. API communication from the React application should be organized
   through the `services/` layer rather than scattered throughout
   components.
9. Reusable UI should go in `components/` rather than being duplicated
   across pages.
10. Shared TypeScript types should go in `types/`.
11. If someone believes the project structure needs to change
    significantly, discuss it with the team before restructuring the
    repository.

These rules exist for readability and maintainability, and to make the
repository easy for every teammate to understand and contribute to.
