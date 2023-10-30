# Token Set

A set does not have any definition or structure, it's a loose organization of tokens. A set must have a token defining it.
A token can belong to one or more sets at the same time. Tokens can be shared between sets.

A token set is owned by the owner of the token that defines it.
But others' tokens can be added to the set, if possible.

The defining token of a set can have its ownership transferred

The token defining the set determines who can read (see the tokens in it) and write to the set (do set operations on it).
The defining token can have a location, and bounds, given to it, like any normal token.
This location can be used by set operations.

Tokens about to be added, or it a set, have allergies and affinities. This can prevent the token from being added,
or it can cause the token to move to a relative of the set soon after its added.

Tokens about to be added or removed can have their actions handle those events, and decline. Then the token is not moved.
Likewise, the token defining the set can have actions handle the event for the token entering and leaving the set.

A set can have a requirement to specify what tokens are allowed in there.


## Set relationships
[relationships](relationship-overview.md)
Token sets might be organized to have parents,siblings and links. There should be ways to navigate through this with the api.


## Movement
[movement-overview.md](movement-overview.md)
Tokens can move, on their own, through set relationships. They move on set relationship at a time to the next set that has the most compatibility.
This only happens if the affinity or allergies are set up for the token.


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

# Requirements in a set definition

When a set has a requirement in its definition, the means only the types and quantity of tokens are allowed into the set.
It can be that the requirement has a minimum of greater than 0 for one or more types.
This means that tokens can only be added via set operations that have that many at the same time

# Allergies and Affinities

A tokens total affinity and allergy is the sum of its attributes.

If there is no attraction to a set, and a repulsion, then the token cannot be added to the set.

However, if there is a mix or only attraction, then token can be added to the set.

If a set has relations, then if there is a mix and the token finds a better attraction in a link or child or parent, it will move sets on its own.

A set has these measured by the token by having the current set and its neighbors summed up:  
The total "charge" of this token to a set is +1 for each attraction in a set, and -1 for each repulsion, this total number is the charge-per-set or -+

* -+ in the current set is 100%
* each immediate neighbor has its -+ set at 50%
* so if the current is at 3 and the neighbors are at -1/2 and 5/2 , the total charge for the current set is 5, and for the neighbors is 3/2 - 2  = -1/2 and 5 + 3/2 = 8 1/2 the token goes to the neighbor at 8.5

This movement is calculated when the token is first added, and whenever any new set links/relations are made/removed, and when new tokens are added or removed from the current or connected sets

internally, the counting takes place after all movement is done via an api command

## Allergies

Sometimes an attribute does not want to be in a set if another attribute is already in the set. this is set in the attributes allergy array

## Affinities

Sometimes an attribute must have another attribute to already exist in a set before it can join it. This is set in the attribute's affinity array

# Read and write permissions can be defined by set membership

attributes have the option to be readable or/and writable based on other attributes being present in the same set (not necessarily in the same token)

Between the ability to control when a token is added to a set, and when something is readable. This makes for a powerful set of access choices.

Additionally, user permission is by group, and group membership can be restricted to a boundary (only active in time or location)


