# Quadrant Chart

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `quadrantChart`).

## Default example: Product Positioning

```mermaid
quadrantChart
    title Reach and engagement of campaigns
    x-axis Low Reach --> High Reach
    y-axis Low Engagement --> High Engagement
    quadrant-1 We should expand
    quadrant-2 Need to promote
    quadrant-3 Re-evaluate
    quadrant-4 May be improved
    Campaign A: [0.3, 0.6]
    Campaign B: [0.45, 0.23]
    Campaign C: [0.57, 0.69]
    Campaign D: [0.78, 0.34]
    Campaign E: [0.40, 0.34]
    Campaign F: [0.35, 0.78]
```

## Fit

Locate items on two well-defined continuous/ordinal axes with named zones.

## Rules

- Define axis directions, units, and the dividing line first.
- Point coordinates come from data or stated judgement.
- Quadrant names carry decision meaning, not "quadrant 1".

## Avoid

Do not call any 2D scatter a priority map; point distance must not encode an undefined third dimension.
