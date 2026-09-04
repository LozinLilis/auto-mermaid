# Gantt Chart

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `gantt`).

## Default example: Product Launch Plan

```mermaid
gantt
    title Product Launch Plan
    dateFormat YYYY-MM-DD
    section Planning
        Market research      :done, research, 2024-03-01, 10d
        Define requirements  :done, reqs, after research, 7d
    section Build
        Design prototype     :active, proto, after reqs, 14d
        User testing         :testing, after proto, 7d
    section Launch
        Marketing campaign   :marketing, after proto, 14d
        Release day          :milestone, after testing, 0d
```

## Fit

Tasks, phases, start/end dates, durations, completion state, dependencies.

## Rules

- Declare date format, timezone assumptions, and workday rules.
- Group with `section`; express dependencies with `after`.
- `done`/`active` must reflect real progress.

## Avoid

Do not use Gantt for dense causal networks; do not fake precise schedules for tasks with no date basis.
