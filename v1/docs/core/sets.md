# Token set

All tokens belong to one or more token sets.

A token set does not have any definition or structure, it's a loose organization of tokens.

A token set must be owned by only one user. Ownership is not transferred, but the tokens in one set can be added to the tokens in another set.

A user's group can read a token set, or write and change it if admin

A token set has a location given by the user token.

This location can be used by set operations.

## Set relationships

Token sets might be organized to have parents,siblings and links. There should be ways to navigate through this with the api.
Note that there is not a restriction of the same user owning the parent and children. Also note that nested folders can be made.

This file structure of sets can be serialized and shared using the normal set serialization.

Children cannot be descendants to ancestors (no inheritance loops)

Links are one way and can be cyclic

Children are defined by the parent. Links are defined by the token doing the link to the other token

Links are stored in a specific type of attribute as the token id of the child or target

A set can make a link  by setting a new attribute dynamically on the set token whose value is the target set.
The attribute can also have an affinity for the target set, but the value is null. If the token of the set is in a set with the token that has the affinity,
Then dynamic linkage can happen. But if an allergy gets in the way, this link can be broken

Same sort of linking for child parent, but here, the attributes need to be on both parent and child and be reciprocal in their values (or affinities for dynamic) 

Each link attribute can inherit from a link attribute base

## Definition

    So a token-set:
        user: must be one user
        name: unique (optional) used for pathing of set paths for set boundaries (todo boundary type of set paths to read and write or action)
        tokens: []
        token: (optional) if some description is needed for this token set, or for identifying it with a set path
        parent-token-set: (optional) may have a parent, used for organizing token sets. (cannot be cyclic)
        linked-sets: (optional) may have links to other sets (can be cyclic so two sets can link to each other)

Tokens here can be reused and shared between sets, and have other roles at the same time

## Type groups

Type groups are used in token set operations

A token-type can be added into a type-group:

Tokens types can belong to one or more type-groups.

A type-group can be used in token-set operations, where tokens are added or removed between sets

Type-group can have a token to denote who owns it, and any attributes , to give it a name and appearance, or notes, and to provide logic for set operations
* Attributes can have those inherited from the attribute_filter which can look at the set to filter and decide which will be allowed

Ownership is not used when type-groups are used in set operations

The token types can have a max and min amounts. In set operations the exact amount used will default to be either the min,then max if min not set, or all available if neither

    So: a type-group:
        token: (optional) if some description is needed for this type-group, or for identifying it with a set path, or putting bounds of when this can be used
        token-types: [ {
            type: token-type
            minimum_needed: optional
            maximum_needed: optional
        }]

## Set operations

When putting a token into a token set, using an operation, the allows_set is evaluated if the owners are not the same, or if present.

When using a set in an operation, the token set can have an attribute allows_set_operation which has to be truthful to proceed
The value of this can be a script and set by bounds, the script can do a filter for the type of set operation or what is being used in the operation

set operations:

* T is the type-group and is always optional, if missing it means all are operated on
* A is the source set
* B is a second source set
* D is the destination set
* M is a token type
* G is a token type guid
* P is export data for a token set
* S is an optional bounds for the tokens in the sets. This can be used in any operations. The tokens must be in these bounds. "
* Path-specifier can be added to any operation



        combine/add: A source, B source (optional),  T pattern, D destination
        remove: A source, T pattern, D destination / removes tokens from a set puts it in another set
        create set: => new empty set
        delete set: removes a set, fails if any token here is not already in another set
        edit_attribute => attribute name, attribute value , A source, T pattern
        change_owner => new owner id, A source, T pattern
        copy => P source, G token type guid from source , M destination token type, D destination
        count => A source, path specifier  > number 

### Relation operations

Finds related tokens in sets. Tokens are related by having common ancestors and parents.

These operations can also filter by getting the related tokens that have attributes in common

* Z is an array of attributes the current user can read


        find related: A source, B source,  Z optional attributes , D destination

sets can have children and links.


### Gathering operations

Operations similar to grep of find for the attribute values and their static content, in a file structure (treat links like siblings in a folder or more accurately here sibling sets)

operations to make simple key value objects for each set ( singular or with siblings (links) or children) with attribute names the keys and static values
each token can be a new object of (attribute:value) and these can optionally be left alone or condensed to a single layer of key values
if condensed, then the values for each attribute turn into an array for each set

searching can filter static values via regex, numeric_range, comparison (comparisons can be nested), or strict string match

    search: A source,  Z  attributes , T optional pattern, options to recurse levels, to filter, to condense => simple object

#### Using tags to gather - path specifier

Sometimes want to find stuff in set relations, where there is a token in one set, and another token in a set elsewhere, or a token path,

this token path can be sort of like a url apples/bananas/pears

this will start the search for any sets that have the apples token, then for any sibling or children sets that have bananas, then for any s or c sets that have pears, then do the search

optionally, there can be gaps in between the sets that have the tags, so we may not find apples in the parent set, but in some descendant, then the bananas would be further in a grandchild, etc

both tags and attribute names can be searched for this way, and the search combined

so, in this notation # means a token name, and . means an attribute and :x means value of x, and > means no gaps

that means to search for #apples>.bears:2/#witches.broomsticks:wooden

would be to start looking in the top set for tokens called apples,
then for any immediate children or siblings if there is a set with an attribute of bears that has a value of 2,
for any descendant or sibling chain find witches token that have wooden broomsticks

A path specifier can be added to any set operation

Once can count the path specifier in a set, this is used for some actions

---------------

Searches by set relationships. While a space or > can mean immediate or gap set relations

one can put in required relationships in a set too, this @ is done before the #.
@child(#ads.none) @parent(.persimmons) @link(#roads)

so #apples>@child(#ads.none).bears:2

searches first sets of apple tokens, then for any immediate child whose set token it type ads with attribute none fine a token with attribute bear value 2 in that set

### Global Set

    All tokens are in a global set (G) so if needing to find any token at all use G for A 

### Copy

Copy allow tokens to be shared across servers operated by different people.

It takes the publicly visible attributes, and creates new tokens owned by the calling user with its attributes set to the public ones.
And has an originating data attributes: origin_server_url, origin_token_guid

When a token is verified to have this data, the server that owns it is called, and it can send back an answer, or can send back updated data

Token sets can be exported to be in a json like structure, converted to an object here

### export data

Token sets can be serialized to have the data in the attributes as key value pairs, as seen by the logged-in user.

Token set relations can also be serialized with the token set, if chosen, with references to the sibling, parent and children sets to be used to get their data


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
