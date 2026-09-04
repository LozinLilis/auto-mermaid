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

A slice may carry several diagrams only when the facts genuinely separate and each diagram takes a different perspective (proven combinations: [catalog](catalog.md) combination rules). Never generate charts to cover all 32 types.

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

## Shared style directory

One style authority per maintained repo: `<repo-root>/.auto-mermaid/theme.css`. Colors, fonts, and stroke widths exist only there; a `.mmd` with inline `style`/`fill:`/hex is a contract violation (existing repo convention wins; record the authority in the atlas).

```bash
mkdir -p .auto-mermaid   # first run only; write theme.css from the template below
for f in docs/diagrams/*.mmd; do   # restyle = edit theme.css, re-run this, git-diff the SVGs
  mmdc -i "$f" -o "${f%.mmd}.svg" -C .auto-mermaid/theme.css   # Windows: pass native paths to -C/-p
done
```

The only styling a `.mmd` may contain is a name binding — verified on mermaid-cli 11.x: the token lands in the SVG class attribute, theme.css colors it.

```text
classDef halted cssClass-halted
class A halted
```

Default theme.css (ship when the repo has none). Hard constraint, measured: Mermaid embeds its own theme CSS into the SVG with an `#my-svg` ID prefix on every rule (specificity 1-1-1); bare class selectors (0-1-1) in an injected `-C` file lose the cascade no matter where they are appended. Every rule below carries the prefix — a theme that "renders but looks unchanged" almost always means it is missing this. Verify by pixels, not by grepping the SVG for your CSS text:

```css
#my-svg svg { font-family: "Segoe UI", "PingFang SC", "Microsoft YaHei", sans-serif; }
/* text vertical centering: Mermaid sizes label boxes from its built-in 14px font;
   when theme.css shrinks the font, the table-cell content anchors to the top of the
   foreignObject box and every node label sits high (measured: 7/44px margins at 10px
   font). Flex-centering the label div restores centering at any font size. */
#my-svg foreignObject > div {
  display: flex !important;
  align-items: center;
  justify-content: center;
  height: 100%;
}
#my-svg .node rect, #my-svg .node polygon, #my-svg .node circle, #my-svg .node path { fill: #f8fafc; stroke: #475569; stroke-width: 1.2px; }
#my-svg .label text, #my-svg .label span, #my-svg span { fill: #0f172a; color: #0f172a; }
#my-svg .cluster rect { fill: #f1f5f9; stroke: #94a3b8; stroke-dasharray: 4 3; }
#my-svg .edgePath .path { stroke: #64748b; stroke-width: 1.2px; }
#my-svg .edgeLabel, #my-svg .edgeLabel p { background-color: #ffffff; color: #334155; }
/* semantic categories — #my-svg .node.<name> matches the source's cssClass-<name> */
#my-svg .node.halted rect { fill: #fef2f2; stroke: #b91c1c; }

/* Sequence diagrams use a separate class family; .node selectors do not reach them. */
#my-svg .actor, #my-svg .participant { fill: #ffffff; stroke: #000000; }
#my-svg .actor-line { stroke: #000000; stroke-width: 0.8px; }
#my-svg .messageLine0, #my-svg .messageLine1 { stroke: #000000; }
#my-svg .labelBox, #my-svg .loopLine { stroke: #000000; fill: #ffffff; }
#my-svg .note { fill: #ffffff; stroke: #000000; }
```

Measured cascade facts: (1) bare class selectors lose outright — every Mermaid theme rule carries the `#my-svg` ID prefix; (2) with the prefix, mmdc's injected CSS sits in a later `<style>` block than the theme, so it wins at equal specificity — it even beats inline fill presentation attributes on elements (measured: plain declaration and `!important` both override note `fill="#EDF2AE"`; no `!important` needed); (3) pixel-count verification needs a tolerant threshold: subpixel font rendering leaves faint colored fringes on every glyph edge, which naive color thresholds count as "leaked color" — always confirm a pixel anomaly visually before chasing it.

Layout knobs: `font-family`, `font-size`, `rx` (corner radius) and `stroke-width` are plain CSS properties and are overridable from theme.css. Measured boundary: CSS `font-size` does **not** rescale node boxes — Mermaid sizes every box from its built-in font and the injected stylesheet runs after layout, so boxes keep their original geometry (identical across theme variants); shrinking the font therefore leaves the label anchored high in its box until the flex-centering rule above is applied. What CSS cannot control: the layout engine itself (node positions, spacing, rank direction) — restyle only, never re-layout from CSS.

## Style control surface (measured)

When the user asks "how do I make it look like X", route them through these tiers, strongest to weakest:

1. **Per-diagram `%%{init}%%`** — `theme` (default/dark/forest/neutral/base), `themeVariables` (per design token), `themeCSS` (raw CSS). Inline in the `.mmd`; use for one-off needs, not for repo-wide style.
2. **Shared stylesheet** — `mmdc -C .auto-mermaid/theme.css` (or the host's CSS hook). The recommended repo-wide authority; restyle = edit one file + re-render.
3. **Semantic name bindings** — `classDef`/`style`/`class` in the source; colors live in the stylesheet, never hex in the source.
4. **Built-in theme** — the embedded `#my-svg`-prefixed CSS everything above overrides.

`themeCSS` caveats (all measured on mermaid-cli 11.x):
- every selector is wrapped in the `#my-svg` namespace: a class you write as `.x` becomes `#my-svg .x`; writing your own `#my-svg` prefix produces the dead selector `#my-svg #my-svg .x`.
- it is prepended **before** the theme's own rules in the same style block, so at equal specificity the theme wins — use `!important` to beat hardcoded theme declarations.
- `& { ... }` compiles to a true `#my-svg { ... }` root rule and is the only measured way to paint the SVG's own background (theme-agnostic dark box, e.g. for beta types whose canvas the `background` token does not reach); `:scope` compiles to the dead `#my-svg :scope`.
- mmdc's `-b` writes an inline `background-color` on the root that beats any CSS — when verifying SVG-native backgrounds, strip that inline style or screenshot the rendered page, not the mmdc PNG.

## Validation and delivery

- Check every `.mmd` for declaration, syntax, IDs, references, and edge direction.
- When a Mermaid CLI, Live Editor, or repo render script exists, render every new/changed diagram — not just the overview.
- Trace at least one key relation per diagram back to real source or docs, so an atlas that is syntactically valid cannot be factually wrong.
- On render failure, isolate syntax vs. version vs. content with the matching reference's minimal example; never delete relations to fake a pass.
- Deliver per diagram: path, type, slice covered, fact sources, verification result, remaining limits.
- If sources were produced but not rendered, state "sources generated, render unverified"; never claim the diagrams passed.
