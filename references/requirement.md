# Requirement Diagram

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `requirementDiagram`).

## Default example: E-Bike Braking System

```mermaid
requirementDiagram

    requirement rider_safety {
        id: 1
        text: Riders must be able to stop safely in all conditions.
        risk: high
        verifymethod: test
    }

    functionalRequirement brake_response {
        id: 1.1
        text: Brakes engage within 100 ms of lever pull.
        risk: medium
        verifymethod: test
    }

    performanceRequirement stopping_distance {
        id: 1.2
        text: Stop from 25 km/h within 4 m on dry pavement.
        risk: medium
        verifymethod: demonstration
    }

    designConstraint water_resistance {
        id: 1.3
        text: Brake electronics must be IP67 rated.
        risk: low
        verifymethod: inspection
    }

    element brake_controller {
        type: hardware
        docRef: "specs/brake-controller"
    }

    element road_test_suite {
        type: "test suite"
        docRef: "qa/road-tests"
    }

    rider_safety - contains -> brake_response
    rider_safety - contains -> stopping_distance
    brake_response - derives -> water_resistance
    brake_controller - satisfies -> brake_response
    road_test_suite - verifies -> stopping_distance
```

## Fit

Requirements, elements, and tracing relations: contains, derives, satisfies, verifies, refines, traces, copies.

## Rules

- Each requirement has a stable ID, clear text, risk, and verification method.
- Relation direction answers "who satisfies/verifies/derives whom".
- The diagram carries tracing relations, not the requirement prose or acceptance criteria.

## Avoid

Do not pass off a task list as requirements; requirement IDs, verification methods, and tracing links must keep a single authoritative source.
