# Event Modeling Diagram

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `eventmodeling`).

## Default example: Shopping Cart Story

```mermaid
eventmodeling

tf 01 ui ShopUI
tf 02 cmd AddItemToCart
tf 03 evt ItemAdded
tf 04 rmo CartView ->> 03
tf 05 ui CheckoutUI
tf 06 cmd PlaceOrder
tf 07 evt OrderPlaced
tf 08 rmo OrderStatus ->> 07
```

## Fit

Business timeline: commands, events, views, actors, systems, read models.

## Rules

- Events state facts that happened; commands state intent; views state readable results.
- Keep the timeline in a single direction.
- Every command points to the events it produces; every view names the events it consumes.

## Avoid

Never let model output become an event fact on its own; do not label commands, events, and views with one shared style.
