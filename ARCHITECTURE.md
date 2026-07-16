# LUMORA Architecture

LUMORA is designed to be extended and adapted to different business scenarios.

You can customize:

- Business domains
- Data sources
- Dashboard modules
- AI capabilities
- Security rules
- Integrations

The architecture has been designed to allow new features without affecting existing components.


## High-Level Architecture

![High Level Architecture](diagrams/high-level-architecture.png)

### Architecture Flow

```text
                    Users
                      │
                      ▼
              Angular Frontend
                      │
                  HTTPS / REST
                      │
                      ▼
             Spring Boot Backend
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
 Authentication   Business Logic   Reporting
        │             │             │
        └─────────────┼─────────────┘
                      │
               Spring Data JPA
                      │
                  Hibernate ORM
                      │
                      ▼
                 PostgreSQL
```

---

## Backend Architecture

![Backend Architecture](diagrams/backend-architecture.png)

### Backend Layers

```text
Controller
    │
    ▼
Service
    │
    ▼
Repository
    │
    ▼
Database
```

### Controller

- Receives HTTP requests
- Validates input
- Returns HTTP responses

### Service

- Implements business rules
- Coordinates application logic
- Calls repositories

### Repository

- Database access
- CRUD operations
- JPA Queries

### Database

- PostgreSQL
- Relational model
- Persistent storage

---

## Frontend

- Angular
- TypeScript
- Responsive Design
- REST API Consumer
- JWT Authentication

---

## Backend

- Java 21
- Spring Boot
- Spring Security
- Spring Data JPA
- Hibernate
- Bean Validation
- OpenAPI / Swagger

---

## Database

- PostgreSQL
- Relational Database
- Normalized Schema

---

## Security

- JWT Authentication
- Role-Based Access Control (RBAC)
- Password Encryption (BCrypt)

---

## API

- REST Architecture
- JSON
- HTTP Status Codes
- OpenAPI Documentation

---

## Multi-Tenant Architecture

Each company has:

- Own users
- Own stores
- Own products
- Own inventory
- Own sales
- Own dashboards
- Own KPIs

Business data is logically isolated.

---

## Future Integrations

- Python Analytics Engine
- Artificial Intelligence Assistant
- Power BI
- SAP Integration
- Microsoft Dynamics
- Oracle ERP
- CSV Import
- Excel Import

---

## Future Infrastructure

- Docker
- Docker Compose
- GitHub Actions
- AWS
- Monitoring
- Logging
- CI/CD Pipeline

---

## Design Principles

- Layered Architecture
- SOLID Principles
- Clean Code
- RESTful APIs
- Separation of Concerns
- Modular Design