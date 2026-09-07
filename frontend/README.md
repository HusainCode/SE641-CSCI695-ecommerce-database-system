# Frontend Development Guide

The frontend is a single-page application built with:

- React 19
- TypeScript 5.9
- Vite

This guide explains how the frontend is organized and how to add new code
consistently.

## 1. Frontend Architecture

Intended data flow:

```text
Page / Component
      ↓
Service
      ↓
REST API
      ↓
Spring Boot Backend
```

Keep API communication separated from UI components — components and
pages should not call `fetch`/`axios` directly.

## 2. Directory Responsibilities

```text
src/
├── assets/
├── components/
├── hooks/
├── pages/
├── services/
├── types/
├── utils/
├── App.tsx
└── main.tsx
```

**`components/`**
Reusable UI components used by multiple pages.

Examples: `ProductCard.tsx`, `Button.tsx`, `LoadingSpinner.tsx`

**`pages/`**
Full page-level components corresponding to application screens.

Examples: `ProductsPage.tsx`, `CartPage.tsx`, `OrderHistoryPage.tsx`

**`services/`**
Communication with the Spring Boot REST API.

Examples: `productService.ts`, `orderService.ts`, `cartService.ts`

API calls should generally **not** be scattered directly throughout
components or pages.

**`hooks/`**
Reusable custom React hooks.

Examples: `useProducts.ts`, `useCart.ts`

**`types/`**
Shared TypeScript types and interfaces.

Examples: `Product.ts`, `Order.ts`, `Customer.ts`

**`utils/`**
Reusable helper functions that do not belong to a specific component.

Examples: `formatCurrency.ts`, `formatDate.ts`

**`assets/`**
Images, icons, and other static frontend assets.

## 3. How to Add a New Feature

Example only — a hypothetical `Product` feature, showing what a teammate
might eventually create and what each file would be responsible for.
**Do not create these files**; this is documentation, not a task.

```text
pages/
└── ProductsPage.tsx        # screen that displays the product list

components/
└── ProductCard.tsx         # reusable UI for a single product

services/
└── productService.ts       # REST calls to /api/products

types/
└── Product.ts              # shared Product type/interface

hooks/
└── useProducts.ts          # reusable logic for loading/managing products
```

## 4. React / TypeScript Coding Style

| Element | Convention | Example |
| --- | --- | --- |
| React components | `PascalCase` | `ProductCard.tsx`, `ShoppingCart.tsx`, `OrderHistory.tsx` |
| Functions / variables | `camelCase` | `calculateTotal()`, `productList`, `orderTotal` |
| Custom hooks | `camelCase`, must start with `use` | `useProducts()`, `useCart()` |
| Service files | `camelCase` | `productService.ts`, `orderService.ts` |
| Types / interfaces | `PascalCase` | `Product`, `Order`, `Customer` |
| Constants | `UPPER_SNAKE_CASE` (when appropriate) | `MAX_CART_SIZE` |

## 5. Component Rules

- Keep components focused on one responsibility.
- Avoid extremely large components.
- Extract reusable UI into `components/`.
- Do not duplicate the same UI across multiple pages.
- Keep page-level components in `pages/`.
- Do not put API logic directly throughout UI components.
- Keep API communication in `services/`.
- Put reusable stateful logic in `hooks/`.
- Put shared TypeScript definitions in `types/`.
- Put generic helper functions in `utils/`.
- Avoid using `any` unless there is a legitimate reason.
- Use meaningful names.
- Remove unused imports and dead code.

## 6. API Service Rules

React communicates with the Spring Boot backend through REST APIs.
Future API calls should be organized under `src/services/`, for example:

```text
productService.ts
cartService.ts
orderService.ts
```

Pages and components should call a service function rather than
duplicating fetch/API logic throughout the application.

API calls are **not implemented yet** — this section describes where
they will go.

## 7. Future Project Pages

The project proposal eventually includes:

- Product catalog
- Product search
- Product details
- Shopping cart
- Checkout / order creation
- Order history
- Order details
- Admin product management
- Admin inventory management
- Admin order management
- Sales and inventory reports

These are **future features only** — do not create these pages now.

## 8. Adding New Folders

Before creating a new folder:

1. Check whether the code belongs in an existing folder.
2. Do not create random folders.
3. Every new folder must have one clear responsibility.
4. Follow the existing project organization.
5. Avoid creating multiple folders that serve the same purpose.
6. Discuss significant structural changes with the team before
   reorganizing the frontend.

The goal is for every teammate to immediately understand where code
belongs.

## 9. Comments and Readability

- Prefer readable code and meaningful names.
- Comments should explain **why** something is done when necessary.
- Do not write comments that simply repeat the code.
- Do not leave large blocks of commented-out code.
- Keep formatting consistent.
- Avoid unnecessary complexity.

## 10. Before Adding Code

Ask yourself:

1. Is this a page, component, service, hook, type, utility, or asset?
2. Does an appropriate folder already exist?
3. Am I duplicating something that already exists?
4. Am I keeping API communication in `services/`?
5. Is this component reusable?
6. Am I following the existing naming conventions?

## 11. Running the Frontend

```bash
npm install
npm run dev
```

Other available commands (defined in `package.json`):

```bash
npm run build      # type-check (tsc -b) and build for production
npm run lint        # run oxlint
npm run preview     # preview a production build locally
```

There is no test script configured yet.

## 12. Git Workflow

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
3. Before submitting/merging the PR, run `npm run build` and
   `npm run lint` and verify your changes work.
4. If something is broken, fix it on your branch first. Do not merge
   broken code into `main`.
5. Commit and push your working branch.
6. Submit a Pull Request from your branch into `main`.
7. Merge the PR only after confirming the branch builds and lints
   correctly.

This keeps `main` stable and prevents one teammate's unfinished or
broken changes from breaking the project for everyone.

## 13. Before Opening a Pull Request

- [ ] Code is in the correct directory.
- [ ] Naming conventions are followed.
- [ ] No unnecessary files were added.
- [ ] No unrelated code was changed.
- [ ] No secrets were committed.
- [ ] No `node_modules/` files are tracked.
- [ ] TypeScript has no errors (`npm run build`).
- [ ] Frontend builds successfully.
- [ ] Linting passes (`npm run lint`).
- [ ] Code is readable.
- [ ] API logic is properly organized (in `services/`).
- [ ] Reusable code is not unnecessarily duplicated.

## 14. Important Git Rules

- **Never** commit `node_modules/`.
- Never commit `.env` files containing secrets, API keys, passwords, or
  credentials.
- Never commit build output (`dist/`).
- Never commit temporary IDE files.
- Develop on feature branches, not directly on `main`.

## 15. Keep This Guide Simple

This is a student team project. The primary goals are consistency,
readability, clear responsibilities, easy collaboration, and
maintainability — not advanced React architecture we aren't using.
