# Set operations

When putting a token into a token set, or removing it from a set, actions can reject this on the token

When using a set in an operation, actions can block different operations

The value of this can be a script and set by bounds, the script can do a filter for the type of set operation or what is being used in the operation

set operations:

* T is the requirement and is always optional, if missing it means all are operated on
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

## Relation operations

Finds related tokens in sets. Tokens are related by having common ancestors and parents.

These operations can also filter by getting the related tokens that have attributes in common

* Z is an array of attributes the current user can read


        find related: A source, B source,  Z optional attributes , D destination

sets can have children and links.


## Search operations 

### Global Set

    All tokens are in a global set (G) so if needing to find any token at all use G for A 