# Chart Type Catalog

Route by the question the diagram must answer. Pick one primary type per diagram. Add a second type for the same slice only when it answers a different question from independent facts.

## Structure and boundaries

| Question to answer | Use | Good companion | Do not use it for |
|---|---|---|---|
| Which components exist, who owns what, how do they talk? | [Architecture](architecture.md) | Sequence (one request path) | step-by-step procedure |
| Same, expressed at C4 levels (context / container / component / deployment)? | [C4](c4.md) | Flowchart for dynamic views | mixing several C4 levels in one diagram |
| Two-dimensional block placement, occupancy, nesting? | [Block](block.md) | Architecture for semantics | ordered control flow |

## Behaviour and flow

| Question to answer | Use | Good companion | Do not use it for |
|---|---|---|---|
| What happens next, including branches and loops? | [Flowchart](flowchart.md) | State (what states mean) | message ordering between participants |
| Who calls whom, in what order, with what replies? | [Sequence](sequence.md) | Architecture | state transitions |
| What states can an object be in, and what triggers a change? | [State](state.md) | Sequence | plain call listings |
| Which commands raise which events, and which views consume them? | [Event Modeling](event-modeling.md) | State | internal call chains |

## Data and contracts

| Question to answer | Use | Good companion | Do not use it for |
|---|---|---|---|
| Entities, fields, keys, cardinality? | [Entity Relationship](entity-relationship.md) | Class (domain behaviour) | methods and behaviour |
| Types, interfaces, inheritance, members? | [Class](class.md) | ER | runtime call order |
| Bit ranges of a packet or binary layout? | [Packet](packet.md) | — | field tables as flows |
| Which requirement is satisfied / verified / traced by what? | [Requirement](requirement.md) | Flowchart | plain task lists |

## Planning, work, and analysis

| Question to answer | Use | Good companion | Do not use it for |
|---|---|---|---|
| When do tasks run, with dependencies? | [Gantt](gantt.md) | Kanban | causal networks |
| What work items are in which state column? | [Kanban](kanban.md) | Gantt | timelines |
| How do branches, commits, merges relate? | [Git](git.md) | — | generic flow |
| Why did this outcome happen? | [Ishikawa](ishikawa.md) | Flowchart | task checklists |
| What kind of problem context is this (clear / complicated / complex / chaotic)? | [Cynefin Framework](cynefin-framework.md) | — | generic 2x2 priority grid |
| How does one topic branch into a hierarchy of ideas? | [Mindmap](mindmap.md) | — | control flow |

## Data display

| Question to answer | Use | Do not use it for |
|---|---|---|
| Share of a single whole by category? | [Pie](pie.md) | multi-series or many slices |
| Position of items on two defined axes? | [Quadrant](quadrant.md) | axes without defined meaning |
| Multi-metric profile comparison? | [Radar](radar.md) | mixed scales or a hidden total score |

## Grammar readers

Railroad diagrams render a grammar as a readable path from entry to exit. Choose by the source grammar family and never translate operator semantics between them:

- [Railroad ABNF](railroad-abnf.md) — rules written in ABNF.
- [Railroad EBNF](railroad-ebnf.md) — rules written in EBNF.
- [Railroad TIR](railroad-tir.md) — TIR grammar dialect.
- [Railroad PEG](railroad-peg.md) — parsing expression grammars; ordered choice matters.

## Combination rules

- Architecture/C4 + Sequence: structure and one runtime path, each from its own facts.
- ER + Class: data shape and behaviour, only if both are real, separate sources.
- State + Sequence: lifecycle meaning and the calls that drive it.
- Requirement + Flowchart: tracing relations and the process being traced.

## Tie-breakers

When two candidate types both seem to fit, decide by the question's subject:

- Architecture vs C4 vs Block: C4 when the audience already works in C4 levels; Block when spatial placement/occupancy is the message; Architecture otherwise.
- Flowchart vs State: Flowchart when the reader asks "what step is next"; State when the reader asks "what can this object be, and what flips it".
- Sequence vs Flowchart: Sequence needs ≥2 named participants exchanging messages; a single actor's logic stays a flowchart.
- ER vs Class: ER when the source of truth is the data schema; Class when it is the code's type system.
- Pie vs Radar vs Quadrant: Pie = one whole split by category; Radar = several subjects profiled on identical metrics; Quadrant = items positioned on two defined axes.

## Version note

Version-sensitive types (Architecture, Cynefin Framework, Event Modeling, Ishikawa, Radar, Packet, all Railroad variants) shift syntax across Mermaid versions. Before authoring one, treat the current Mermaid Live Editor example for that type as the syntax authority.
