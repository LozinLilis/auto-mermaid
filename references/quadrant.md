# Quadrant

## Purpose
Locate items on two well-defined continuous/ordinal axes with named zones.

## Minimal syntax

```mermaid
quadrantChart
    title Priority map
    x-axis Low effort --> High effort
    y-axis Low value --> High value
    quadrant-1 Invest
    quadrant-2 Explore
    quadrant-3 Defer
    quadrant-4 Quick wins
    Item A: [0.75, 0.8]
```

## Rules
- Define axis directions, units, and the dividing line first.
- Point coordinates come from data or stated judgement.
- Quadrant names carry decision meaning, not "quadrant 1".

## Avoid
Do not call any 2D scatter a priority map; point distance must not encode an undefined third dimension.
