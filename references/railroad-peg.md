# Railroad PEG

## Purpose
Render PEG (parsing expression grammar) expressions as readable parse paths.

## Authoring
Use the current Live Editor Railroad (PEG) example as syntax authority. PEG ordered choice, sequences, lookahead, and repetition must not be read as unordered set alternation.

## Rules
- Show ordered-choice precedence explicitly — PEG results depend on it.
- Preserve lookahead, negation, and recursion; they change parsing behaviour.
- Keep entry, success exit, and backtracking traceable.

## Avoid
Do not read a PEG railroad as an unordered CFG; never delete ordered choice or lookahead for visual simplicity.
