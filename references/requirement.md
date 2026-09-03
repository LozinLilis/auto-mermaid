# Requirement

## Purpose
Requirements, elements, and tracing relations: contains, derives, satisfies, verifies, refines, traces, copies.

## Minimal syntax

```mermaid
requirementDiagram
    requirement req {
        id: R-001
        text: The service validates input
        risk: medium
        verifMethod: test
    }
    element service {
        type: functionalRequirement
        docRef: api-spec
    }
    service - satisfies -> req
```

## Rules
- Each requirement has a stable ID, clear text, risk, and verification method.
- Relation direction answers "who satisfies/verifies/derives whom".
- The diagram carries tracing relations, not the requirement prose or acceptance criteria.

## Avoid
Do not pass off a task list as requirements; requirement IDs, verification methods, and tracing links must keep a single authoritative source.
