# Gantt

## Purpose
Tasks, phases, start/end dates, durations, completion state, dependencies.

## Minimal syntax

```mermaid
gantt
    title Release plan
    dateFormat YYYY-MM-DD
    section Build
    Design :done, design, 2026-01-01, 5d
    Implement :active, impl, after design, 7d
```

## Rules
- Declare date format, timezone assumptions, and workday rules.
- Group with `section`; express dependencies with `after`.
- `done`/`active` must reflect real progress.

## Avoid
Do not use Gantt for dense causal networks; do not fake precise schedules for tasks with no date basis.
