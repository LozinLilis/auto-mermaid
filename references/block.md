# Block

## Purpose
Two-dimensional blocks, grids, nested regions, occupancy, hardware/module layout.

## Minimal syntax

```mermaid
block-beta
    columns 3
    A B C
    D:2 E
    A --> D
```

## Rules
- Block diagrams are about spatial layout, not auto-flowed process.
- Control structure with `columns`, block widths, and `space`.
- Edges supplement relations; they do not replace layout meaning.

## Avoid
Do not let block widths, columns, and content length contradict each other; check the current editor example when syntax details shift.
