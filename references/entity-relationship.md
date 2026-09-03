# Entity Relationship

## Purpose
Entities, fields, primary/foreign keys, optionality, cardinality.

## Minimal syntax

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    CUSTOMER {
        string customer_id PK
        string name
    }
    ORDER {
        string order_id PK
        string customer_id FK
    }
```

## Rules
- Define entity boundaries first, then fields and cardinality.
- PK/FK markers must match real constraints.
- Relation labels are domain verbs: `places`, `contains`.

## Avoid
Do not stuff class methods into entities; do not let layout imply cardinality; never invent fields without evidence.
