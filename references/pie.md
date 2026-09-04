# Pie Chart

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `pie title Pets adopted by volunteers`).

## Default example: Basic Pie Chart

```mermaid
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```

## Fit

Category shares of a single whole, few categories, meaningful sum.

## Rules

- All values share one population, one measurement basis, one time window.
- Merge minor categories into "Other" when slices get many.
- The title names the whole and the basis.

## Avoid

Do not compare multiple time series or many near-equal slices; do not present unnormalized numbers as percentages.
