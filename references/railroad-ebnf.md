# Railroad Diagram (EBNF)

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `railroad-ebnf-beta`).

## Default example: Expression Grammar

```mermaid
railroad-ebnf-beta
    title Expression Grammar

    expression = term ( "+" term | "-" term )* ;
    term = factor ( "*" factor | "/" factor )* ;
    factor = number | "(" expression ")" ;
    number = digit+ ;
    digit = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;
```

## Fit

Render EBNF rules as visual grammar paths: options, repetitions, branches.

## Rules

- Mark entry, exit, alternation, and repetition clearly.
- Keep rule names identical to the source; split complex rules.
- State implicit constraints in prose; the path carries structure only.

## Avoid

Do not imply precedence from node position; never delete options, repetition bounds, or recursion to shorten the drawing.
