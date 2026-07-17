# LUMORAIQ Database Design

## Entity Relationship Diagram

The following diagram represents the main business domains and their relationships.

```mermaid
erDiagram

    COMPANY ||--o{ USERS : contains
    COMPANY ||--o{ STORES : owns
    COMPANY ||--o{ PRODUCTS : manages
    COMPANY ||--o{ SUPPLIERS : works_with

    USERS }o--|| DEPARTMENT : belongs_to
    USERS }o--|| ROLE : has

    STORES ||--o{ INVENTORY : controls
    PRODUCTS ||--o{ INVENTORY : tracked_in

    STORES ||--o{ SALES : generates
    PRODUCTS ||--o{ SALES : sold


    COMPANY {
        int id PK
        string name
    }

    USERS {
        int id PK
        string name
        string email
    }

    DEPARTMENT {
        int id PK
        string name
    }

    ROLE {
        int id PK
        string name
    }

    STORES {
        int id PK
        string name
        string location
    }

    PRODUCTS {
        int id PK
        string sku
        string description
        string status
    }

    INVENTORY {
        int id PK
        int quantity
        string status
    }

    SUPPLIERS {
        int id PK
        string name
    }

    SALES {
        int id PK
        date sale_date
        decimal amount
    }
```

---

## Domain Overview

The database model follows a multi-tenant SaaS architecture.

Each COMPANY represents an independent business tenant with isolated business data.

Main business domains:

- **Users Management**
    - Employees
    - Departments
    - Roles
    - Access control

- **Store Management**
    - Retail locations
    - Operational structure

- **Product Management**
    - Product catalog
    - Product lifecycle

- **Inventory Management**
    - Stock availability
    - Product tracking by store

- **Procurement Management**
    - Supplier relationships
    - Product sourcing

- **Sales Management**
    - Sales transactions
    - Business analytics data

---

## Future Extensions

The model is designed to support future capabilities:

- Executive dashboards
- KPI analytics
- AI-powered insights
- Automated reports
- ERP integrations
- Advanced inventory forecasting