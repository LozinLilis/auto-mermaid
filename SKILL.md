---
name: auto-mermaid
description: "Mermaid diagram / repo diagram maintenance / flowchart / architecture request entry: auto-split scope, pick types, generate sources."
version: 0.1.0
license: MIT
metadata:
  purpose: "Unified skill set covering the 32 chart types of the official Mermaid Live Editor examples"
---

# Auto Mermaid

## When to trigger

Use when the user asks to choose, explain, write, modify, convert, or validate Mermaid diagrams, or makes a vague request such as "maintain diagrams for my repo" or "add diagrams to this project". A vague request must enter repository maintenance mode; never respond by only asking which chart type to draw.

## Two entry modes

### Repository maintenance mode

When the user gives a scope (repo, directory, module, files, or current diff) without naming chart types:

1. Take the user-specified path/module as the scope; if none is narrower, take the current repo but do a lightweight inventory first — never read all sources at once.
2. Read repo rules, entry docs, module lists, and key implementations in scope; extract facts from real symbols, callers, data structures, states, and configuration.
3. Split the scope into independently readable slices; each slice answers one primary question (component boundaries, call path, lifecycle, data relations, requirement tracing, schedule...).
4. Select one or more best-fit chart types per slice; generate multiple charts for one slice only when each answers a distinct question backed by independent facts.
5. Generate all diagram sources and maintain one diagram index: slice, chart type, fact sources, coverage boundary, and validation status map one-to-one.
6. Keep one style authority for the repo: `.auto-mermaid/theme.css` at the repo root, injected at render time (`mmdc -C`); `.mmd` sources stay free of inline colors. See [Shared style directory](references/repository-maintenance.md).

### Explicit-type mode

When the user names one or more chart types, the user decides the types; the skill still splits scope, reads the matching reference, generates from repo facts, checks whether each named type fits, and states limits for ill-fitting types instead of silently swapping types.

## Automatic type selection

Route by the primary question, not by file extension. Coarse map; the full table with per-type links is [Chart type catalog](references/catalog.md):

- Boundaries and structure -> Architecture / C4 / Block
- Control flow, lifecycle, call order, event chains -> Flowchart / State / Sequence / Event Modeling
- Data shape and contracts -> ER / Class / Packet / Requirement
- Work, schedule, history, analysis -> Gantt / Kanban / Git / Timeline / User Journey / Ishikawa / Cynefin / Mindmap / Wardley
- Data display and grammars -> Quadrant / Pie / Radar / XY Chart / Sankey / Treemap / Venn / Railroad (ABNF / EBNF / IR / PEG)

One slice may yield several diagrams (e.g. Architecture + Sequence) only when each answers a distinct question from independent facts. Load the matching type reference from the catalog before authoring.

## Workflow

- Locate: extract objects, relations, direction, branches, time, constraints.
- Split: cut the scope into independently readable slices; record fact sources per slice.
- Select: choose one or more types automatically; with user-named types, honor them and report fit.
- Author: start from the minimal skeleton in the matching reference; reuse repo vocabulary and stable IDs.
- Validate: check fenced blocks, declarations, identifiers, edge direction, labels, fact sources, and version compatibility; render whenever a renderer exists.
- Maintain: update only affected slices; keep untouched diagrams; sync the diagram index and coverage notes.
- Deliver: list generated/updated diagrams, what each covers, its sources, what is not covered, and actual verification results.

Full scanning, slicing, incremental maintenance, and artifact conventions: [Repository maintenance mode](references/repository-maintenance.md).

## Shared hard rules

- A chart type never substitutes for the domain model: ER carries entity relations, Class carries types and methods, State carries transitions.
- One diagram, one primary narrative; split dense content into an overview plus detail diagrams.
- Separate node IDs from display text; avoid spaces, punctuation, and reserved words in IDs.
- Edge labels state the real relation or condition, never filler like "handles" or "related".
- Do not encode time, causality, hierarchy, or set overlap with one shared arrow style; pick the type that matches the semantics.
- Labels are blocks too: adjacent edges, bidirectional edge pairs, and cross-lane messages place their labels in the same small region, and two long labels there will collide (measured in practice). Keep labels on such edges under ~6 characters, move the detail into `Note`/`%%` comments, and after rendering run a visual collision pass over every diagram: label↔label, label↔lifeline/edge, label↔frame.
- Render with the repo's shared style injected: `mmdc -C .auto-mermaid/theme.css`; colors and fonts live only in that file, never inline in `.mmd` sources.
- Report actual verification results before delivery; never claim syntax passes without rendering when claiming validation at all.

## Type references

One file per type at `references/<type>.md` (e.g. `references/sequence.md`); [Chart type catalog](references/catalog.md) links all types with routing. Load only the file(s) for the selected type(s).

## Delivery checklist

- [ ] Primary type matches the expression goal.
- [ ] The matching reference was read.
- [ ] Declarations and syntax are supported by the target Mermaid version.
- [ ] Nodes, edges, and labels do not mix different semantics.
- [ ] Each block was actually rendered, or the delivery states it was not.
- [ ] Render used the shared `.auto-mermaid/theme.css`; no inline colors in `.mmd` sources.
- [ ] Dense diagrams were split rather than shrunk.
