# Architecture

## Purpose
System components, services, groups, boundaries, entry points, stores, connections.

## Authoring
architecture-beta
    group system(cloud)[System]
    service api(server)[API] in system
    service store(database)[Store] in system
    api:R --> L:store

## Rules
- Draw ownership boundaries and components first; add real dependency edges.
- Edge labels use relation verbs: `reads`, `writes`, `routes`, `validates`.
- Icons aid recognition only and never replace node names.

## Avoid
Do not draw time-ordered flow as architecture; do not let position imply deployment boundaries; if `architecture-beta` fails to parse, rebuild from the current Live Editor example.
