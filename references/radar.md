# Radar Diagram

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `radar-beta`).

## Default example: Student Grades

```mermaid
---
title: "Grades"
---
radar-beta
  axis m["Math"], s["Science"], e["English"]
  axis h["History"], g["Geography"], a["Art"]
  curve a["Alice"]{85, 90, 80, 70, 75, 90}
  curve b["Bob"]{70, 75, 85, 80, 90, 85}

  max 100
  min 0
```

## Fit

Multi-metric profiles of several subjects on identical, normalized axes.

## Rules

- All subjects share the same metric set, direction, and scale.
- Keep metrics few and meaningful; define what high/low means.
- Use only when the profile comparison itself is the point.

## Avoid

Do not mix scales; do not let enclosed area act as a hidden total score; confirm current syntax against the Live Editor example.
