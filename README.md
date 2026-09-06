# E-Commerce Database System

A full-stack e-commerce platform built with React, TypeScript, Java, Spring Boot, and MySQL.

This project is being developed by a team of graduate students as part of the Master of Science in Software Engineering program at St. Cloud State University for SE641 & CSCI 695.

The goal of the project is to design, develop, and deploy a complete e-commerce system while applying full-stack software engineering, REST API development, relational database design, transaction processing, and modern team development practices.

The application follows a layered architecture with a React and TypeScript frontend, a Java and Spring Boot REST API, and a relational MySQL database. The system is designed to support product management, shopping carts, order processing, inventory management, simulated payments, shipment tracking, and reporting.

This repository serves as the central engineering workspace for the project. It contains the application source code, database design, API documentation, architecture diagrams, technical documentation, deployment information, and other development resources.

> **Project Status:** Under active development. Features, documentation, diagrams, and deployment information will be updated as development progresses.

## Team Members

- Husain Alshaikhamed
- Elias Gomez Marroquin
- Mayu Ebina
- Fairooz Nawar
- Dinesh Sevet

## Technology Stack

| Layer / Category | Technology |
| --- | --- |
| Frontend / GUI | React 19, TypeScript 5.9 |
| Backend | Java 21, Spring Boot 3.5.x |
| Database | MySQL 8.4 LTS |
| API Layer | REST API |
| ORM / Persistence | Spring Data JPA, Hibernate 6.x |
| Build Tool | Maven 3.9.x |
| Version Control | Git, GitHub |
| Project Management | Jira |
| Deployment | Railway |

## System Architecture

The application follows a layered full-stack architecture that separates the frontend, API and business logic, persistence layer, and relational database.

```text
React + TypeScript
        |
        | HTTP / REST API
        v
Java + Spring Boot
        |
        | Controller
        v
      Service
        |
        v
    Repository
        |
        | Spring Data JPA / Hibernate
        v
      MySQL
```

### Frontend Layer

The frontend is developed using React and TypeScript. It provides the graphical user interface for customers and administrators and communicates with the Spring Boot backend through REST API requests.

### Backend Layer

The backend is developed using Java and Spring Boot. It is responsible for REST API endpoints, application business logic, validation, database operations, and communication between the frontend and persistence layer.

The backend follows a conventional layered architecture:

```text
Controller
    |
    v
Service
    |
    v
Repository
    |
    v
MySQL
```

### Persistence Layer

Spring Data JPA and Hibernate are used to map Java entities to relational database tables and manage persistence between the Spring Boot application and MySQL.

### Database Layer

MySQL provides persistent relational storage for customers, addresses, products, categories, inventory, shopping carts, orders, payments, shipments, and their relationships.

## Core Features

### Customer Features

The customer-facing portion of the application is designed to support common e-commerce workflows.

- Browse available products
- Search for products
- Browse products by category
- Filter products by price
- Filter products by availability
- View product details
- Add products to a shopping cart
- Update shopping cart quantities
- Remove products from a shopping cart
- Place orders
- View previous orders
- View order details
- View order status

### Product Management

The system provides functionality for managing the store's product catalog.

- Create products
- View products
- Update product information
- Delete products
- Assign products to categories
- Search products
- Filter products
- Manage product availability
- Associate products with inventory records

### Shopping Cart

The shopping cart connects customers with products before an order is created.

Planned functionality includes:

- Create a customer shopping cart
- Add products to the cart
- Update product quantities
- Remove products from the cart
- Maintain cart items
- Calculate information required for order creation
- Convert cart information into an order

### Order Management

The system supports the complete lifecycle of an order.

- Create customer orders
- Create associated order items
- Associate orders with customers
- Associate products with order items
- Calculate order totals
- Store order status
- Update order status
- Display customer order history
- Display individual order details
- Allow administrators to view and manage orders

## Inventory Management

Inventory is maintained separately from product information so that product data and inventory quantities can be managed independently.

The system is designed to:

- Track available product quantities
- Update inventory quantities
- Associate inventory records with products
- Update inventory when an order is placed
- Identify low-stock products
- Provide inventory reports
- Allow administrators to manage inventory

## Payments

Payment functionality is simulated for this project.

The application will store payment information associated with an order, including:

- Payment record
- Associated order
- Payment amount
- Payment status

The project does not connect to a real payment processor. Sample and synthetically generated payment data are used to model the workflow without storing or processing real financial information.

## Shipping

Shipment functionality is also simulated.

The application is designed to store:

- Shipment records
- Associated orders
- Tracking numbers
- Carrier information
- Shipment status
- Shipment dates

This allows the system to model an e-commerce shipping workflow without integrating with an external shipping provider.

## Administration

Administrative functionality provides management capabilities for the e-commerce system.

Administrators will be able to:

- Add products
- Update products
- Delete products
- Manage product categories
- Manage inventory quantities
- View orders
- Update order status
- Monitor inventory
- Identify low-stock products
- Access sales information
- Access inventory reports

## Reporting

The system includes database queries and reports that demonstrate how stored e-commerce data can be used to provide useful information.

Planned reporting functionality includes:

- Sales totals
- Inventory reports
- Low-stock products
- Best-selling products
- Orders by status
- Customer order history

## Database Design

The application uses a relational MySQL database with primary keys and foreign keys to maintain relationships and referential integrity.

### Core Database Entities

| Entity | Purpose |
| --- | --- |
| `CUSTOMER` | Stores customer information |
| `ADDRESS` | Stores customer addresses |
| `PRODUCT` | Stores product information |
| `CATEGORY` | Stores product categories |
| `PRODUCT_CATEGORY` | Creates relationships between products and categories |
| `INVENTORY` | Tracks product inventory |
| `CART` | Represents a customer's shopping cart |
| `CART_ITEM` | Stores products and quantities within a cart |
| `ORDER` | Stores customer order information |
| `ORDER_ITEM` | Stores products and quantities associated with an order |
| `PAYMENT` | Stores simulated payment information |
| `SHIPMENT` | Stores simulated shipment and tracking information |

## Database Relationships

The database is designed around relationships between the core e-commerce entities.

Examples include:

```text
CUSTOMER
   |
   +---- ADDRESS
   |
   +---- CART
   |       |
   |       +---- CART_ITEM ---- PRODUCT
   |
   +---- ORDER
            |
            +---- ORDER_ITEM ---- PRODUCT
            |
            +---- PAYMENT
            |
            +---- SHIPMENT
```

Products and categories use a many-to-many relationship:

```text
PRODUCT
   |
   v
PRODUCT_CATEGORY
   ^
   |
CATEGORY
```

These relationships allow the application to maintain structured and consistent data across the different parts of the system.

## Database Operations

The application is designed to demonstrate both standard CRUD operations and more advanced relational database functionality.

### CRUD Operations

The system supports operations such as:

- Create new products
- Read and view products
- Update product information
- Delete products
- Create customer information
- Update customer information
- Add shopping cart items
- Update shopping cart items
- Remove shopping cart items
- Create orders
- Update order status
- Update inventory quantities
- Create payment records
- Create shipment records

### Advanced Database Operations

The application is also designed to perform more advanced operations, including:

- Search products by name
- Search products by category
- Filter products by price
- Filter products by availability
- Join customers with their orders
- Join orders with order items
- Display complete customer order histories
- Calculate order totals
- Calculate sales totals
- Identify low-stock products
- Determine best-selling products
- Display orders by status
- Generate inventory reports
- Generate sales reports
- Update inventory when an order is placed

## Order Processing Flow

A typical order moves through several parts of the application.

```text
Customer
   |
   v
Browse Products
   |
   v
Shopping Cart
   |
   v
Cart Items
   |
   v
Create Order
   |
   v
Create Order Items
   |
   v
Calculate Order Total
   |
   v
Update Inventory
   |
   v
Create Simulated Payment
   |
   v
Create Simulated Shipment
```

This workflow connects the frontend, backend business logic, and multiple relational database entities.

## REST API

The React frontend communicates with the Spring Boot backend using REST APIs.

The API layer is responsible for exposing application functionality for resources such as:

- Products
- Categories
- Customers
- Addresses
- Shopping carts
- Cart items
- Orders
- Order items
- Inventory
- Payments
- Shipments
- Reports

Example resource structure:

```text
/api/products
/api/categories
/api/customers
/api/carts
/api/orders
/api/inventory
/api/payments
/api/shipments
```

The exact endpoint definitions will be documented as the API is implemented.

## Backend Architecture

The Spring Boot backend is organized using a layered architecture.

### Controller Layer

Controllers receive HTTP requests from the frontend and expose REST API endpoints.

### Service Layer

Services contain application and business logic.

Examples include:

- Order processing
- Inventory updates
- Shopping cart operations
- Product management
- Reporting calculations

### Repository Layer

Repositories provide access to MySQL through Spring Data JPA.

The general request flow is:

```text
HTTP Request
     |
     v
Controller
     |
     v
Service
     |
     v
Repository
     |
     v
Hibernate / JPA
     |
     v
MySQL
```

The response travels back through the layers and is returned to the React frontend.

## Frontend

The React and TypeScript frontend provides the user-facing interface for the application.

Planned screens include:

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
- Sales reports
- Inventory reports

## Repository Structure

The repository will separate application code and technical documentation.

```text
ecommerce-database-system/
|
├── frontend/
│   └── React + TypeScript application
|
├── backend/
│   └── Java + Spring Boot application
|
├── docs/
│   ├── architecture/
│   ├── database/
│   ├── api/
│   ├── diagrams/
│   └── deployment/
|
└── README.md
```

The repository structure may evolve as the application grows.

## Engineering Documentation

Technical documentation will be maintained alongside the source code.

The documentation is planned to include:

- System architecture diagrams
- ER diagrams
- Database schema documentation
- REST API documentation
- Application flow diagrams
- Local development instructions
- Deployment instructions
- Technical design decisions
- Testing documentation

This allows the repository to serve as both the source code location and the central technical reference for the system.

## Development Workflow

The team uses Git and GitHub for source control and collaboration.

Development work will be organized using branches so team members can work on different parts of the system independently.

A typical workflow will be:

```text
Jira Ticket
     |
     v
Development Branch
     |
     v
Implementation
     |
     v
Testing
     |
     v
Pull Request
     |
     v
Review
     |
     v
Merge
```

This workflow helps organize development and reduce conflicts when multiple team members are working on the application.

## Jira and Agile Development

Jira is used for project management and development tracking.

The team uses Jira to manage:

- Sprints
- Features
- Engineering tasks
- Bug reports
- Task assignments
- Development progress

Development follows an Agile sprint-based approach so frontend, backend, database, testing, and documentation work can progress in parallel when appropriate.

## Testing

Testing will be performed throughout development rather than only after implementation is complete.

Testing areas include:

- Database operations
- REST API behavior
- Backend business logic
- Frontend and backend integration
- CRUD functionality
- Advanced database queries
- Order processing
- Inventory updates
- Database transactions
- Application integration

Additional testing documentation will be added as the project develops.

## Deployment

The application is planned to be deployed using Railway.

The deployed environment is expected to include:

```text
React Frontend
      |
      v
Spring Boot Backend
      |
      v
MySQL Database
```

Deployment configuration, environment information, and application URLs will be documented once the deployment environment is established.

## Project Roadmap

### Planning and Design

- Define system requirements
- Design database schema
- Create ER diagram
- Establish repository structure

### Database and Backend

- Create MySQL database
- Implement database tables and relationships
- Create Spring Boot backend
- Implement repositories and services
- Implement CRUD functionality

### Frontend and API Integration

- Build React interface
- Implement REST API endpoints
- Connect React to Spring Boot
- Implement product browsing and searching

### E-Commerce Functionality

- Implement shopping cart
- Implement order processing
- Implement inventory updates
- Implement simulated payments
- Implement simulated shipments
- Implement advanced database queries
- Implement reporting

### Testing and Improvements

- Test database operations
- Test frontend/backend integration
- Test advanced queries
- Test transactions
- Fix bugs
- Improve the user interface

### Deployment and Documentation

- Deploy application
- Populate database with sample data
- Complete engineering documentation
- Complete diagrams
- Perform final integration testing

## Academic Context

This project is being developed as a team class project for **SE641 & CSCI 695** at **St. Cloud State University**, with team members from both the **Master of Science in Software Engineering** and **Master of Science in Computer Science** programs.

Although developed in an academic setting, this repository is structured as an engineering project and serves as a technical record of the team's work, including application development, database engineering, API design, system architecture, testing, deployment, and team collaboration.

## Project Status

**Under active development.**

Source code, diagrams, API documentation, deployment information, and additional engineering documentation will be added and updated as development progresses.
