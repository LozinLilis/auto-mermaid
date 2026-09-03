---
name: auto-mermaid
description: "Mermaid diagram / repo diagram maintenance / flowchart / architecture request entry: auto-split scope, pick types, generate sources."
version: 0.1.0
license: MIT
metadata:
  purpose: "Unified skill set covering the 24 chart types of the Mermaid Live Editor example menu"
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

### Explicit-type mode

When the user names one or more chart types, the user decides the types; the skill still splits scope, reads the matching reference, generates from repo facts, checks whether each named type fits, and states limits for ill-fitting types instead of silently swapping types.

## Automatic type selection

Route by the primary question, not by file extension:

- Components, services, boundaries, dependencies -> Architecture / C4 / Block
- Steps, branches, exceptions, loops -> Flowchart
- Call order across participants -> Sequence
- Types, interfaces, inheritance, methods -> Class
- Entities, fields, keys, cardinality -> Entity Relationship
- Object lifecycle and transitions -> State
- Commands, events, views, business timeline -> Event Modeling
- Packet bit layout -> Packet
- Requirements and verification/tracing links -> Requirement
- Branches, commits, merges -> Git
- Task scheduling with dates -> Gantt
- Work-state columns -> Kanban
- Central-topic hierarchy -> Mindmap
- Cause analysis -> Ishikawa
- Decision-context classification -> Cynefin Framework
- Two-axis positioning, share of a whole, multi-metric profile -> Quadrant / Pie / Radar
- Grammar rule paths -> Railroad ABNF / EBNF / TIR / PEG

One slice may yield, for example, Architecture + Sequence ("component relations + one run path"). Never generate Class + Entity Relationship just because classes and a database exist; each chart needs its own set of facts. See the full routing table in [Chart type catalog](references/catalog.md).

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
- Report actual verification results before delivery; never claim syntax passes without rendering when claiming validation at all.

## 24 sub-references

Full routing: [Chart type catalog](references/catalog.md). Load on demand:

- [Flowchart](references/flowchart.md)
- [Class](references/class.md)
- [Sequence](references/sequence.md)
- [Entity Relationship](references/entity-relationship.md)
- [State](references/state.md)
- [Mindmap](references/mindmap.md)
- [Architecture](references/architecture.md)
- [Block](references/block.md)
- [C4](references/c4.md)
- [Cynefin Framework](references/cynefin-framework.md)
- [Event Modeling](references/event-modeling.md)
- [Gantt](references/gantt.md)
- [Git](references/git.md)
- [Ishikawa](references/ishikawa.md)
- [Kanban](references/kanban.md)
- [Packet](references/packet.md)
- [Pie](references/pie.md)
- [Quadrant](references/quadrant.md)
- [Radar](references/radar.md)
- [Railroad ABNF](references/railroad-abnf.md)
- [Railroad EBNF](references/railroad-ebnf.md)
- [Railroad TIR](references/railroad-tir.md)
- [Railroad PEG](references/railroad-peg.md)
- [Requirement](references/requirement.md)

## Delivery checklist

- [ ] Primary type matches the expression goal.
- [ ] The matching reference was read.
- [ ] Declarations and syntax are supported by the target Mermaid version.
- [ ] Nodes, edges, and labels do not mix different semantics.
- [ ] Each block was actually rendered, or the delivery states it was not.
- [ ] Dense diagrams were split rather than shrunk.
