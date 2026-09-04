# Railroad Diagram (ABNF)

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `railroad-abnf-beta`).

## Default example: Email Address

```mermaid
railroad-abnf-beta
    title Email Address

    address = local-part "@" domain ;
    local-part = 1*( ALPHA / DIGIT / "." / "-" ) ;
    domain = label *( "." label ) ;
    label = 1*( ALPHA / DIGIT / "-" ) ;
```

## Fit

Render ABNF grammar rules as readable railroad paths.

## Rules

- Fix the entry rule and terminal paths first.
- Rule references resolve to definitions; alternation and repetition stay traceable.
- The railroad aids reading; it never replaces parser validation.

## Avoid

Do not turn railroad diagrams into business flows; do not drop ABNF constraints or treat the drawing as executable proof.
