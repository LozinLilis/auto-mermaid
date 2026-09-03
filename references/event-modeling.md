# Event Modeling

## Purpose
Business timeline: commands, events, views, actors, systems, read models.

## Authoring
Version-sensitive type: start from the current Live Editor Event Modeling example and replace items along the timeline; do not guess declaration names from old versions.

## Rules
- Events state facts that happened; commands state intent; views state readable results.
- Keep the timeline in a single direction.
- Every command points to the events it produces; every view names the events it consumes.

## Avoid
Never let model output become an event fact on its own; do not label commands, events, and views with one shared style.
