# Database Design

## Overview

LUMORA follows a **domain-driven database design**.

Instead of documenting the entire database as a single Entity Relationship Diagram (ERD), the data model is organized into business domains. This approach improves readability, maintainability and scalability while reflecting how enterprise SaaS applications are typically documented.

---

# Identity Domain

Responsible for user management, authentication and organizational structure.

```mermaid
erDiagram

    COMPANY ||--o{ USERS : contains
    USERS }o--|| ROLE : assigned
    USERS }o--|| DEPARTMENT : belongs_to

    COMPANY {
        int id PK
        string name
        string legal_name
        string tax_id
        string industry
        string country
        datetime created_at
    }

    USERS {
        int id PK
        int company_id FK
        int role_id FK
        int department_id FK
        string first_name
        string last_name
        string email
        string password_hash
        boolean active
        datetime created_at
    }

    ROLE {
        int id PK
        string name
        string description
        string permissions
        boolean active
        datetime created_at
    }

    DEPARTMENT {
        int id PK
        string name
        string description
        string cost_center
        boolean active
        datetime created_at
    }
```

---

# Operations Domain

Responsible for retail operations including stores, products, suppliers and inventory.

```mermaid
erDiagram

    COMPANY ||--o{ STORES : owns
    COMPANY ||--o{ PRODUCTS : manages
    COMPANY ||--o{ SUPPLIERS : contracts

    STORES ||--o{ INVENTORY : stores
    PRODUCTS ||--o{ INVENTORY : tracked

    STORES {
        int id PK
        int company_id FK
        string name
        string city
        string country
        string manager
        boolean active
        datetime created_at
    }

    PRODUCTS {
        int id PK
        int company_id FK
        string sku
        string name
        string description
        decimal unit_price
        string status
        datetime created_at
    }

    INVENTORY {
        int id PK
        int store_id FK
        int product_id FK
        int quantity
        int minimum_stock
        string status
        datetime updated_at
    }

    SUPPLIERS {
        int id PK
        int company_id FK
        string name
        string contact_name
        string email
        string phone
        string country
        datetime created_at
    }
```

---

# Sales Domain

Responsible for sales transactions and business reporting.

```mermaid
erDiagram

    STORES ||--o{ SALES : generates

    STORES {
        int id PK
        string name
        string city
        boolean active
    }

    SALES {
        int id PK
        int store_id FK
        date sale_date
        decimal subtotal
        decimal tax
        decimal total
        string payment_method
        datetime created_at
    }
```

---

# Domain Summary

## Identity

Manages users and organizational structure.

- Company
- Users
- Roles
- Departments

---

## Operations

Represents the operational side of the business.

- Stores
- Products
- Inventory
- Suppliers

---

## Sales

Stores transactional information used for reporting and analytics.

- Sales
- Revenue
- Executive KPIs

---

# Future Database Extensions

The MVP intentionally keeps the schema simple.

Future releases may introduce:

## Customer Management

- CUSTOMERS

## Sales

- SALE_ITEMS
- PAYMENTS
- RETURNS

## Procurement

- PURCHASE_ORDERS
- PURCHASE_ITEMS

## Inventory

- WAREHOUSES
- INVENTORY_MOVEMENTS
- STOCK_ADJUSTMENTS

## Product Catalog

- CATEGORIES
- BRANDS

## Analytics

- KPI_SNAPSHOTS
- AI_RECOMMENDATIONS
- FORECASTS

## Security

- AUDIT_LOGS
- USER_SESSIONS

---

# Design Principles

The database has been designed following enterprise software best practices.

- Multi-tenant architecture
- Domain-driven organization
- Normalized relational model (3NF)
- PostgreSQL compatible
- Spring Data JPA ready
- Scalable for SaaS environments
- Designed for future AI and analytics capabilities