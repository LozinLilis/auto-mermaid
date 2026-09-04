# Treemap

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `treemap-beta`).

## Default example: Monthly Household Budget

```mermaid
---
config:
  treemap:
    valueFormat: '$0,0'
---
treemap-beta
"Monthly Budget"
    "Housing"
        "Rent": 1400
        "Utilities": 220
        "Internet": 60
    "Food"
        "Groceries": 480
        "Dining out": 180
    "Transport"
        "Car payment": 320
        "Fuel": 140
    "Savings"
        "Emergency fund": 300
        "Retirement": 400
```

## Fit

Hierarchical quantity where area encodes size: top-down nesting down to leaf values.

## Rules

- Leaf values share one unit; the root is the whole.
- Keep nesting shallow (<=3 levels) for readability.

## Avoid

Do not use a treemap for flat lists or parts that do not sum to a whole; do not let area encode a second metric.
