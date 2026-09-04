# Git Graph

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `gitGraph`).

## Default example: Basic Git Flow

```mermaid
gitGraph
    commit id: "a3f82c1"
    branch develop
    checkout develop
    commit id: "b7e41d9"
    commit id: "c9d52e4"
    checkout main
    merge develop id: "d4e8f3a"
    commit id: "e1b6c90"
    branch feature
    checkout feature
    commit id: "f2a8d17"
    commit id: "a8c3f54"
    checkout main
    merge feature id: "b9d7e21"
```

## Fit

Commits, branches, checkouts, merges, tags, release lines.

## Rules

- Each commit node represents a real history node or an explicitly pedagogical one.
- Branch names, order, and merges must match the target history.
- Use tags or commit ids for releases, rollbacks, baselines.

## Avoid

Do not use gitGraph as generic flow; never invent commits, branches, or merges.
