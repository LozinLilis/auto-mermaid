# Railroad Diagram (PEG)

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `railroad-peg-beta`).

## Default example: Calculator Grammar

```mermaid
railroad-peg-beta
    title Calculator Grammar

    Expression <- Term (("+" / "-") Term)* ;
    Term <- Factor (("*" / "/") Factor)* ;
    Factor <- Number / "(" Expression ")" ;
    Number <- Digit+ ;
    Digit <- "0" / "1" / "2" / "3" / "4" / "5" / "6" / "7" / "8" / "9" ;
```

## Fit

Render PEG (parsing expression grammar) expressions as readable parse paths.

## Rules

- Show ordered-choice precedence explicitly — PEG results depend on it.
- Preserve lookahead, negation, and recursion; they change parsing behaviour.
- Keep entry, success exit, and backtracking traceable.

## Avoid

Do not read a PEG railroad as an unordered CFG; never delete ordered choice or lookahead for visual simplicity.
