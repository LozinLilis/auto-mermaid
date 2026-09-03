# Class

## Purpose
Classes, interfaces, attributes, methods, inheritance, realization, aggregation, composition, dependency.

## Minimal syntax

```mermaid
classDiagram
    class Account {
        +String id
        +open()
    }
    class PremiumAccount
    Account <|-- PremiumAccount
```

## Rules
- Class diagrams carry static structure, not call order or state transitions.
- Keep visibility markers, types, and relation endpoints consistent.
- Show only members relevant to the question; do not dump full source.

## Avoid
Do not use plain arrows for inheritance; do not confuse instance data, database columns, and class members.
