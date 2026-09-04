# Entity Relationship Diagram

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `erDiagram`).

## Default example: Basic ER Schema

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ ORDER_ITEM : contains
    PRODUCT ||--o{ ORDER_ITEM : includes
    CUSTOMER {
        string id
        string name
        string email
    }
    ORDER {
        string id
        date orderDate
        string status
    }
    PRODUCT {
        string id
        string name
        float price
    }
    ORDER_ITEM {
        int quantity
        float price
    }
```

## Fit

Entities, fields, primary/foreign keys, optionality, cardinality.

## Rules

- Define entity boundaries first, then fields and cardinality.
- PK/FK markers must match real constraints.
- Relation labels are domain verbs: `places`, `contains`.

## Avoid

Do not stuff class methods into entities; do not let layout imply cardinality; never invent fields without evidence.
