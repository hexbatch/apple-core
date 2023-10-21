# Token set

All tokens belong to one or more token sets.

A token set does not have any definition or structure, it's a loose organization of tokens.

A token set must be owned by only one user. Ownership is not transferred, but the tokens in one set can be added to the tokens in another set.

A user's group can read a token set, or write and change it if admin

A token set has a location given by the user token.

This location can be used by set operations.

## Set relationships
[sets.relationships.md](sets.relationships.md)
Token sets might be organized to have parents,siblings and links. There should be ways to navigate through this with the api.


## Definition

    So a token-set:
        user: must be one user
        name: unique (optional) used for pathing of set paths for set boundaries (todo boundary type of set paths to read and write or action)
        tokens: []
        token: (optional) if some description is needed for this token set, or for identifying it with a set path
        parent-token-set: (optional) may have a parent, used for organizing token sets. (cannot be cyclic)
        linked-sets: (optional) may have links to other sets (can be cyclic so two sets can link to each other)
        type-group: id (optional), if there are max and min requirements, or not, this types the set and these rules will be honoroed 

Tokens here can be reused and shared between sets, and have other roles at the same time

## Type groups
[sets.type-groups.md](sets.type-groups.md)
Type groups  specify what types are wanted, and amount of each of types.
I can make a type group of a couple of types, and say the first type should be 5 to 8 tokens, and the second type must be at least 10 in amount

Type groups are used in token set operations and anywhere I need some requirements to the types and amounts of tokens.



## Set Operations
[sets.operations.md](sets.operations.md)
We can do operations on sets to make new sets, combine sets, and see what is in a set



## Permissions for a token to be added to a set

By default, a token can always be added to a set if the set is owned by the same person who is owning the token.

By default, a token cannot be added to a set if they are owned by different users.

However, other people can add a token to their sets if the attribute allows_set has a truthful value

if the allows_set is falsy value, even the token owner cannot add to the token set

allows_set, being an attribute, can use a javascript to do complex logic to decide this

## Allergies and Affinities

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

### Allergies

Sometimes an attribute does not want to be in a set if another attribute is already in the set. this is set in the attributes allergy array

### Affinities

Sometimes an attribute must have another attribute to already exist in a set before it can join it. This is set in the attribute's affinity array

## Read and write permissions can be defined by set membership

attributes have the option to be readable or/and writable based on other attributes being present in the same set (not necessarily in the same token)

Between the ability to control when a token is added to a set, and when something is readable. This makes for a powerful set of access choices.

Additionally, user permission is by group, and group membership can be restricted to a boundary (only active in time or location)
