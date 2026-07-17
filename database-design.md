# LUMORAIQ Database Design

## Entity Relationship Diagram

```mermaid
erDiagram

    COMPANY ||--o{ USERS : has
    COMPANY ||--o{ STORES : owns
    COMPANY ||--o{ PRODUCTS : owns
    COMPANY ||--o{ SUPPLIERS : manages

    DEPARTMENT ||--o{ USERS : contains
    ROLE ||--o{ USERS : assigned

    STORES ||--o{ INVENTORY : manages
    PRODUCTS ||--o{ INVENTORY : tracked

    SUPPLIERS ||--o{ PRODUCTS : provides

    STORES ||--o{ SALES : generates
    PRODUCTS ||--o{ SALES : sold


    COMPANY {
        bigint id PK
        varchar name
    }

    USERS {
        bigint id PK
        bigint company_id FK
        bigint department_id FK
        bigint role_id FK
        varchar name
        varchar email
    }

    DEPARTMENT {
        bigint id PK
        bigint company_id FK
        varchar name
    }

    ROLE {
        bigint id PK
        varchar name
    }

    STORES {
        bigint id PK
        bigint company_id FK
        varchar name
        varchar location
    }

    PRODUCTS {
        bigint id PK
        bigint company_id FK
        varchar sku
        varchar description
        varchar status
    }

    INVENTORY {
        bigint id PK
        bigint store_id FK
        bigint product_id FK
        integer quantity
        varchar status
    }

    SUPPLIERS {
        bigint id PK
        bigint company_id FK
        varchar name
    }

    SALES {
        bigint id PK
        bigint store_id FK
        bigint product_id FK
        date sale_date
        decimal amount
    }
```

---

## Design Notes

The database model is designed following a multi-tenant SaaS architecture.

Each COMPANY represents an independent business tenant with isolated data.

Main domains:

- **Users Management**: Employees, departments and roles for access control.
- **Stores Management**: Physical retail locations belonging to each company.
- **Product Management**: Central product catalog.
- **Inventory Management**: Stock availability by store and product.
- **Procurement Management**: Supplier relationships and product sourcing.
- **Sales Management**: Transaction data used for analytics and business intelligence.

The model is designed to support future extensions such as:

- Dashboard KPIs
- AI-powered insights
- Data analytics
- Automated reports
- External ERP integrations