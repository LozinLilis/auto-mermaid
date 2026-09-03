# Railroad ABNF

## Purpose
Render ABNF grammar rules as readable railroad paths.

## Authoring
Treat the current Live Editor Railroad (ABNF) example as syntax authority. Preserve rule names, literals, alternation, repetition, and grouping as ABNF semantics; never borrow EBNF/PEG interpretations.

## Rules
- Fix the entry rule and terminal paths first.
- Rule references resolve to definitions; alternation and repetition stay traceable.
- The railroad aids reading; it never replaces parser validation.

## Avoid
Do not turn railroad diagrams into business flows; do not drop ABNF constraints or treat the drawing as executable proof.
