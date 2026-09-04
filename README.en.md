# auto-mermaid

![badges](./assets/badges.png)

**An agent skill that turns vague diagram requests — especially _"maintain the diagrams for my repo"_ — into a set of Mermaid diagrams grounded in real repository facts.**

[中文 README](./README.zh.md) · [License: MIT](./LICENSE)

![pipeline](./assets/banner.png)

## Why it exists

"Draw a diagram" is a vague request, and the usual failure mode is one giant flowchart with invented arrows. `auto-mermaid` instead:

- treats the request as a **repository-maintenance task**, not a one-shot drawing
- extracts relations only from **real evidence** — source symbols, callers, data structures, states, config, tests, Git history
- never claims a diagram is valid without **actually rendering it**

## How it works

1. **Scope** — a repo, directory, module, file list, or current diff. If the user gives nothing narrower, the skill takes the whole repo but runs a lightweight inventory first; it never reads every source at once.
2. **Slice** — the scope is cut into independently readable slices; each slice answers **one primary question** (component boundaries, call path, lifecycle, data relations, requirement tracing, schedule…).
3. **Route** — each slice is routed to the chart type that fits its semantics. The full routing table lives in [`references/catalog.md`](./references/catalog.md); a slice may yield several diagrams only when each answers a distinct question backed by independent facts.
4. **Generate** — diagram sources (`.mmd`) start from the minimal skeleton in the matching type reference, reuse repo vocabulary and stable IDs, and keep every relation traceable via `%% facts` comments.
5. **Validate** — fenced blocks, declarations, identifiers, edge directions, labels, and fact sources are checked, then each block is **rendered with `mmdc`** whenever a renderer exists.
6. **Maintain** — on follow-up changes only affected slices are updated; untouched diagrams stay; stale relations are removed only after confirmation; the diagram index stays in sync.

## Two entry modes

| Mode | Trigger | Behavior |
| --- | --- | --- |
| **Repository maintenance** | a scope without named chart types, e.g. *"maintain diagrams for this repo"* | full pipeline above: inventory → slice → auto-route → generate → index |
| **Explicit types** | the user names one or more chart types | the user's types are honored; the skill still splits scope, checks fit, and **states limits for ill-fitting types instead of silently swapping them** |

## Covered chart types

**32 types**, the full set of the official Mermaid Live Editor examples — each with its own reference file (fit, the official default example as syntax authority, and measured pitfalls):

> Flowchart · Class · Sequence · Entity Relationship · State · Mindmap · Tree View · Architecture · Block · C4 · Cynefin Framework · Event Modeling · Gantt · Kanban · Git · Timeline · User Journey · Ishikawa · Wardley Maps · Packet · Requirement · Pie · Quadrant · Radar · XY Chart · Sankey · Treemap · Venn · Railroad (ABNF / EBNF / IR / PEG)

Routing details, combination rules, and tie-breakers: [`references/catalog.md`](./references/catalog.md).

## Shared style directory

Every repo gets **one style authority**: `<repo-root>/.auto-mermaid/theme.css`.

- rendered with `mmdc -C .auto-mermaid/theme.css`, so `.mmd` sources stay **semantic** — no inline colors, no per-diagram styling
- a restyle touches **one file** plus a re-render pass; the git diff of the SVGs shows exactly what changed
- the template in [`references/repository-maintenance.md`](./references/repository-maintenance.md) carries **measured cascade facts** (e.g. every rule needs the `#my-svg` ID prefix or it loses to Mermaid's embedded theme) and the boundary of what CSS can control (fonts, stroke, corner radius — **not** node positions)

## Repository layout

```mermaid
%%{init: {'theme':'dark','themeCSS':'&{background-color:#0d1117}.treeView-node-label{fill:#e6edf3!important}.treeView-node-line{stroke:#8b949e!important}.treeView-node-icon{color:#8b949e!important}'}}%%
treeView-beta
auto-mermaid/
  LICENSE
  SKILL.md
  README.md
  README.en.md
  README.zh.md
  assets/
    banner.png
    badges.png
  references/
    catalog.md
    repository-maintenance.md
    architecture.md
    block.md
    c4.md
    class.md
    cynefin-framework.md
    entity-relationship.md
    event-modeling.md
    flowchart.md
    gantt.md
    git.md
    ishikawa.md
    journey.md
    kanban.md
    mindmap.md
    packet.md
    pie.md
    quadrant.md
    radar.md
    railroad-abnf.md
    railroad-ebnf.md
    railroad-ir.md
    railroad-peg.md
    requirement.md
    sankey.md
    sequence.md
    state.md
    timeline.md
    treemap.md
    treeview.md
    venn.md
    wardley.md
    xychart.md
```

## Hard rules (abridged)

- **Facts first.** Relations must trace to a file, symbol, doc, test, or Git record; unknowns are marked pending, never invented.
- **Render or stay silent.** A diagram is only reported as validated after a real `mmdc` render; dense diagrams are split rather than shrunk.
- **One style file.** No inline colors in `.mmd` sources; the shared `theme.css` is the single authority.

## Version note

Most types are version-sensitive (`-beta` suffix or syntax that shifts across versions). The **official default example embedded in each reference file** is the syntax authority; on an older renderer, a failed render is checked against that example, not by editing the source.

## License

[MIT](./LICENSE)
