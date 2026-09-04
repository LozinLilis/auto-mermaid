# Venn Diagram

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `venn-beta`).

## Default example: Product Sweet Spot

```mermaid
venn-beta
    title "Finding the Product Sweet Spot"
    set Desirable
    set Feasible
    set Viable
    union Desirable,Feasible["Worth prototyping"]
    union Feasible,Viable["Cheap to run"]
    union Desirable,Viable["Hard to build"]
    union Desirable,Feasible,Viable["Sweet spot"]
```

## Fit

Overlap of sets: membership, union, and intersection regions, each labelable.

## Rules

- Sets are crisp; every labeled region states what membership means.
- Keep to <=4 sets for readability; label only non-empty regions that carry meaning.

## Avoid

Do not use a Venn for hierarchy (use Mindmap) or fuzzy membership without a stated basis; do not place items in regions without evidence.
