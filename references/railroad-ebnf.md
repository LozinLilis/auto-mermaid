# Railroad EBNF

## Purpose
Render EBNF rules as visual grammar paths: options, repetitions, branches.

## Authoring
Start from the current Live Editor Railroad (EBNF) example and let the current Mermaid version parse it. Do not swap quantifier semantics between ABNF, EBNF, and PEG.

## Rules
- Mark entry, exit, alternation, and repetition clearly.
- Keep rule names identical to the source; split complex rules.
- State implicit constraints in prose; the path carries structure only.

## Avoid
Do not imply precedence from node position; never delete options, repetition bounds, or recursion to shorten the drawing.
