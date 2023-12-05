# Token Set

A set does not have any definition or structure, it's a loose organization of tokens. A set must have a token defining it.
A token can belong to one or more sets at the same time. Tokens can be shared between sets.

A token set is owned by the owner of the token that defines it.
But others' tokens can be added to the set, if possible.



The defining token of a set can have its ownership transferred. This is also known as the set token.
Set tokens are seen as normal tokens unless in a set which has them as a child or link or parent.
Any token can make a set and still be a regular token.
Set tokens can have action handlers for set events. An action handler processing the token-adding-to-set event can filter out tokens using any logic

The token defining the set determines who can read (see the tokens in it) and write to the set (do set operations on it).
This is by who can read and write to the token.

The defining token can have a location, and bounds, given to it, like any normal token.
This location can be used by set operations.



Tokens about to be added, or it a set, have allergies and affinities. This can prevent the token from being added,
or it can cause the token to move to a relative of the set soon after its added.

Tokens about to be added or removed can have their actions handle those events, and decline. Then the token is not moved.
Likewise, the token defining the set can have actions handle the event for the token entering and leaving the set.

A set can have a requirement to specify what tokens are allowed in there.
If a set has a location bounds, then it has an option to only accept tokens inside it that have no location set.
the option for location_checks can be turned on or off at set definition time


## Set relationships
[relationships](relationship-overview.md)
Token sets might be organized to have parents,siblings and links. There should be ways to navigate through this with the api.

## Group sets
[group sets](group-set-overview.md) allow groups to be used more in the api for many things


## Requirements
[sets.requirements.md](requirements-overview.md)
Requirements  specify what types are wanted, and amount of each of types.
I can make a requirement of a couple of types, and say the first type should be 5 to 8 tokens, and the second type must be at least 10 in amount

Requirements are used in token set operations and anywhere there are some requirements to the types and amounts of tokens.


## Set Operations
[sets.operations](operations-overview.md)
We can do operations on sets to make new sets, combine sets, and see what is in a set

## Definition

    So a token-set:
        id: the id of the set
        token: Every set has a token to define it, which adds ways to describe the set, search for it in path operations, or give it some location and time
        tokens: []
        parent-token-set: (optional) may have a parent, used for organizing token sets. (cannot be cyclic)
        linked-sets: (optional) may have links to other sets (can be cyclic so two sets can link to each other)
        requirement: id (optional), if there are max and min requirements, or not, this types the set and filters tokens
        location_checks: true or false

# Requirements in a set definition

When a set has a requirement in its definition, the means only the types and quantity of tokens are allowed into the set.
It can be that the requirement has a minimum of greater than 0 for one or more types.
This means that tokens can only be added via set operations that have that many at the same time

# Allergies and Affinities

A tokens total affinity and allergy is the sum of its attributes.

If there is no attraction to a set, and a repulsion, then the token cannot be added to the set.

However, if there is a mix or only attraction, then token can be added to the set.

If a token, already in a set, has more of an allergy to it, its not removed from the set automatically

## Allergies

Sometimes an attribute does not want to be in a set if another attribute is already in the set. this is set in the attributes allergy array

## Affinities

Sometimes an attribute must have another attribute to already exist in a set before it can join it. This is set in the attribute's affinity array

# Read and write permissions can be defined by set membership

attributes have the option to be readable or/and writable based on other attributes being present in the same set (not necessarily in the same token)

Between the ability to control when a token is added to a set, and when something is readable. This makes for a powerful set of access choices.

Additionally, user permission is by group, and group membership can be restricted to a boundary (only active in time or location)


