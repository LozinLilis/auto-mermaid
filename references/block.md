# Block Diagram

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `block-beta`).

## Default example: Three-Tier Web Architecture

```mermaid
block-beta
  columns 3
  user(("User")):3
  space:3
  ui["Web UI"] api["API Server"] db[("Database")]

  user --> ui
  ui --> api
  api --> db

  style user fill:#ffe0b2,stroke:#fb8c00
  style db fill:#bbdefb,stroke:#1e88e5
```

## Fit

Two-dimensional blocks, grids, nested regions, occupancy, hardware/module layout.

## Rules

- Block diagrams are about spatial layout, not auto-flowed process.
- Control structure with `columns`, block widths, and `space`.
- Edges supplement relations; they do not replace layout meaning.

## Avoid

Do not let block widths, columns, and content length contradict each other; check the current editor example when syntax details shift.
