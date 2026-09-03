# Repository Maintenance Mode

## Goal

Turn a vague request such as "maintain diagrams for my repo" into a set of Mermaid diagrams grounded in real repository facts and maintained incrementally. The point is not one pretty overview; it is to identify the distinct structural perspectives that actually exist in scope and generate only diagrams with information gain.

## Scope resolution

Resolve scope by priority:

1. Files, directories, modules, packages, branches, or work items the user names.
2. The current change set: inspect VCS status and diff first, then follow call chains for necessary context.
3. The repository root: inventory directories, entry points, and docs first, then pick high-value slices; never read every source file by default.

For very large scopes, slice by top-level modules, runtime boundaries, data boundaries, and independent lifecycles. A large repo justifies more diagrams, not one vague overview.

## Scan order

### Rules and current state

Read applicable repo rule files, architecture docs, READMEs, module lists, and existing diagram sources. Existing diagrams are assets to maintain, not automatic truth; spot-check key relations against implementation and tests.

### Structural facts

Within scope, extract:

- packages, modules, services, adapters, stores, external boundaries;
- public entry points, key types, functions, traits/interfaces, commands, events;
- callers, callees, data reads/writes, message directions, error returns;
- state sets, transitions, durable commit points, recovery, retries;
- entity fields, primary/foreign keys, configuration constraints, requirement tracing;
- Git history, task dates, metric data, or packet bit fields (only when such facts actually exist in scope).

Only draw relations traceable to a file, symbol, doc section, test, or Git record. Mark unconfirmed content as pending verification; never let the model invent edges.

## Slice record

Record per slice:

- `slice_id`: stable, readable, tied to a business concept;
- `scope`: files/modules/symbols;
- `question`: the single primary question the diagram answers;
- `facts`: nodes, relations, conditions, times, constraints;
- `source_refs`: where each fact was found;
- `candidate_types` / `selected_types`;
- `coverage`: what is deliberately not expressed;
- `validation`: syntax and render status.

A slice may carry several diagrams, but each must take a different perspective:

- component boundaries + one request path -> Architecture/C4 + Sequence;
- data entities + domain behaviour -> Entity Relationship + Class;
- lifecycle + triggering calls -> State + Sequence;
- acceptance + implementation tracing -> Requirement + Flowchart.

Split into multiple diagrams only when the facts genuinely separate. Never generate charts to cover all 24 types.

## Generation rules

1. Follow the repo's existing diagram directory, naming, and render tooling if present.
2. Otherwise store Mermaid sources under `docs/diagrams/` with an `index.md` diagram atlas in the same directory; never overwrite same-named files without identifying the old diagram and its sources first.
3. Save each diagram as its own `.mmd` (or the repo's existing Mermaid extension); record fact sources in the atlas, not only in chat.
4. `index.md` lists at least: diagram name, slice, type, coverage, sources, last update, render status, uncovered items.
5. Maintain incrementally by default: untouched diagrams stay; affected diagrams update only their slice; confirm a relation truly disappeared before deleting it.
6. With user-named types, still generate them; if a type fits a slice poorly, keep the requested diagram, note the limit in the atlas, and optionally add one minimal fitting diagram — never silently change the type.

## Generation order

1. One minimal scope-overview diagram: the best of Architecture, C4, or Flowchart.
2. Detail diagrams for real questions found by the scan: Sequence, State, Class, Entity Relationship, Requirement, etc.
3. Data-display / grammar / management views last: Pie, Quadrant, Radar, Gantt, Kanban, Git, Packet, Railroad.
4. Before adding a diagram, check it expresses relations no earlier diagram carries; no new information, no new diagram.

## Validation and delivery

- Check every `.mmd` for declaration, syntax, IDs, references, and edge direction.
- When a Mermaid CLI, Live Editor, or repo render script exists, render every new/changed diagram — not just the overview.
- Trace at least one key relation per diagram back to real source or docs, so an atlas that is syntactically valid cannot be factually wrong.
- On render failure, isolate syntax vs. version vs. content with the matching reference's minimal example; never delete relations to fake a pass.
- Deliver per diagram: path, type, slice covered, fact sources, verification result, remaining limits.
- If sources were produced but not rendered, state "sources generated, render unverified"; never claim the diagrams passed.
