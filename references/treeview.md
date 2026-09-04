# TreeView

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `treeView-beta`).

## Default example: Project File Structure

```mermaid
treeView-beta
    my-project/
        src/
            components/
                Button.tsx
                Header.tsx
            App.tsx
            index.js
        .gitignore
        package.json
        README.md
```

## Fit

Filesystem or module layout rendered as a monospace file tree (directories bold, files regular). For "what is in this repo / directory" questions — not for concept hierarchies (use Mindmap).

## Rules

- First line after the type keyword is the root node.
- Two-space indent per level (tabs also parse; keep one style per file).
- Directory entries end with `/`; file entries do not.
- Names may contain spaces, `:`, `()`, `[]`, `{}`, `&`, `#`, `*`, `%`, `^`, `@`, `!`, `?`, `.`, `+`, `~`, backticks, leading dots.
- A literal `/` inside a name is unsupported (rendered as a nested path); rename or drop such entries.
- Deep trees stay readable down to ~100+ nodes without splitting.

## Avoid

Do not use a tree view for concept hierarchies, call graphs, or any tree whose nodes are not filesystem/module entries.

## Availability

Beta type: supported from Mermaid 11.16.0; on older renderers the block fails to render.

## Measured pitfalls

- Node text and connector lines are **hardcoded to black** (`fill:black` / `stroke:black` in the embedded stylesheet) and do not follow `theme` or `themeVariables` (measured on 11.16.0: `theme:'dark'` and the `background` token both leave the text black). For a dark background, override the three classes via `themeCSS` — they beat the embedded rules only with `!important`: `&{background-color:#0d1117}.treeView-node-label{fill:#e6edf3!important}.treeView-node-line{stroke:#8b949e!important}.treeView-node-icon{color:#8b949e!important}` (see "Style control surface" in `repository-maintenance.md` for why `&` and `!important` are both required).
