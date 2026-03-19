# Towards a generic model for card games

We are developing a generic model for defining arbitrary card games, including their rules and the cards themselves.

## Entities

Every part of the game state is an _entity_. Cards, players, teams, and even the game itself are examples of entities.

The entities of a game can be organized as a _tree_ with parent-child relationships:

![Entity Tree](EntityTree.png)

### Entity Attributes

Each entity can have a set of _attributes_ and values. The cost or power of a card, as well as the current life total of a player are great examples for attributes. Attribute values are integers (positive, negative, or zero).

### Entity Tags

_Tags_ are used to describe the basic nature or current state of an entity. Examples are whether a card is a monster or a location, or whether a card has already been used this turn.

Tags can also be applied to other entities, such as the game state itself, for example to store the current turn phase.

Also, tags can be used for specifying the layer of an entity in the entity tree, e.g. if an entity is a player or card.

### Entity Links

Entities can be _linked_ to other entities to express temporary relationships, such as monsters that are about to fight each other. Links are directional: Linking entity A to entity B does not mean that entity B is linked to entity A. Entities can have multiple links.

## Mutations

This very generic model allows for a very narrow, specific, yet highly impactful set of _mutations_:

* `SetAttribute(entity, attribute, value)`
* `AddTag(entity, tag)`
* `RemoveTag(entity, tag)`
* `LinkEntities(source, target, linkType)`
* `UnlinkEntities(source, target, linkType)`

These mutations are sufficient to change the state of any part of the game.

## Events

With this well-defined set of mutations, we can deduce a set of _events_ that can be used to trigger game rules or card abilities:

* `AttributeChanged(entity, attribute, oldValue, newValue)`
* `TagAdded(entity, tag)`
* `TagRemoved(entity, tag)`
* `EntitiesLinked(source, target, linkType)`
* `EntitiesUnlinked(source, target, linkType)`
