# Cynefin Framework

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `cynefin-beta`).

## Default example: Incident Response

```mermaid
cynefin-beta
  title Incident Response

  complex
    "Investigate root cause"
    "Run chaos experiment"

  complicated
    "Analyze performance data"
    "Expert review needed"

  clear
    "Restart service"
    "Apply known fix"

  chaotic
    "Page on-call immediately"

  confusion
    "Unknown failure mode"

  complex --> complicated : "Pattern identified"
  clear --> chaotic : "Complacency"
```

## Fit

Classify problems into Clear / Complicated / Complex / Chaotic / Disorder to pick a response stance.

## Rules

- Place each item in a domain backed by evidence; uncertain items stay in Disorder/pending.
- Attach the domain's response style (sense-analyze-respond, probe-sense-respond, act-sense-respond).
- Domain semantics matter more than decorative placement.

## Avoid

Do not reduce Cynefin to a generic 2x2 priority grid; quadrant position never substitutes for the complexity judgement.
