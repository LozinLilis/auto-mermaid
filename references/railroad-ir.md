# Railroad Diagram (IR)

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `railroad-beta`).

## Default example: Expression Grammar

```mermaid
railroad-beta
    title Expression Grammar

    expression = sequence(
        nonterminal("term"),
        zeroOrMore(sequence(
            choice(terminal("+"), terminal("-")),
            nonterminal("term")
        ))
    ) ;
    term = sequence(
        nonterminal("factor"),
        zeroOrMore(sequence(
            choice(terminal("*"), terminal("/")),
            nonterminal("factor")
        ))
    ) ;
    factor = choice(
        nonterminal("number"),
        sequence(terminal("("), nonterminal("expression"), terminal(")"))
    ) ;
    number = oneOrMore(nonterminal("digit")) ;
    digit = choice(terminal("0"), terminal("1"), terminal("2"), terminal("3"), terminal("4"), terminal("5"), terminal("6"), terminal("7"), terminal("8"), terminal("9")) ;
```

## Fit

Render a grammar written in the IR dialect (sequence, choice, zeroOrMore, oneOrMore, nonterminal, terminal) as a readable railroad path.

## Rules

- Preserve rule names, terminals, and repetition exactly; IR constructs map one-to-one to railroad shapes.
- Fix the entry rule first; keep recursion visible.

## Avoid

Do not read the picture as executable proof - final legality is judged by grammar tooling. Do not force-translate IR constructs into ABNF/EBNF/PEG semantics.
