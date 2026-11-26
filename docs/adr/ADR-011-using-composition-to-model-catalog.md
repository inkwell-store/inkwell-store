# Using composition to model catalog

## Context

A very common pattern to implement is to define classes in an OOP language to model the entities or "things" you work with and map these entities to database tables. This problem is quite famous and the attempt to adjust relational models to classes is famously called **ORM** (Object-relational-mapping).

Classes mapped to tables can be expressed

## Options considered

* Favor inheritance over composition
* Favor composition over inheritance

## Decision

I choose to use composition as my primary entity relationship. This goes in line with the priniciples established in the famous book *Design Patterns*, published in 1994 by Erich Gamma, Richard Helm, John Vlissides and Ralph Johnson.

Composition is just more flexible than inheritance. Currently, my model is not well defined and it can change quite a bit with time.

Naturally, I can use inheritance in specific situations, but as a whole, I think composition makes more sense for a flexible and constantly evolving data model.

## Consequences

* Using composition makes relationships between entities less complex and avoids issues that come out naturally from inheritance strategies.
* Separation of concers is strengthed with composition. For example, having a **Book** be composed of a **Product** makes a Book own the publication identity, while a Product owns the commercial aspects.
