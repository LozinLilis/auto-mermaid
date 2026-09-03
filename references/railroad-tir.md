# Railroad TIR

## Purpose
Render the TIR grammar dialect as railroad paths.

## Authoring
Version-sensitive dialect: copy the minimal Railroad (TIR) example from the Live Editor, then replace rule contents; do not guess fields from ABNF/EBNF syntax.

## Rules
- Keep rule text, entry, and exit conditions traceable.
- Split deeply recursive rules into local diagrams joined by rule names.
- Final legality is judged by grammar tooling, not the picture.

## Avoid
Do not force-translate TIR into a generic flow; never hide recursion, alternation, or repetition.
