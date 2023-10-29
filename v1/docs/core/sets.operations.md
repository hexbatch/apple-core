# Set operations

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

## Relation operations

Finds related tokens in sets. Tokens are related by having common ancestors and parents.

These operations can also filter by getting the related tokens that have attributes in common

* Z is an array of attributes the current user can read


        find related: A source, B source,  Z optional attributes , D destination

sets can have children and links.


## Gathering operations

Operations similar to grep of find for the attribute values and their static content, in a file structure (treat links like siblings in a folder or more accurately here sibling sets)

operations to make simple key value objects for each set ( singular or with siblings (links) or children) with attribute names the keys and static values
each token can be a new object of (attribute:value) and these can optionally be left alone or condensed to a single layer of key values
if condensed, then the values for each attribute turn into an array for each set

searching can filter static values via regex, numeric_range, comparison (comparisons can be nested), or strict string match

    search: A source,  Z  attributes , T optional pattern, options to recurse levels, to filter, to condense => simple object

## Using tags to gather - path specifier

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

## searches by set relationships

Searches by set relationships. While a space or > can mean immediate or gap set relations

one can put in required relationships in a set too, this @ is done before the #.
@child(#ads.none) @parent(.persimmons) @link(#roads)

so #apples>@child(#ads.none).bears:2

searches first sets of apple tokens, then for any immediate child whose set token it type ads with attribute none fine a token with attribute bear value 2 in that set

to start a search at a particular set, use the @set(#apples)

to list all the tokens in a set, do not put any modifiers after the last set: 


to search with ownership use the @owner(some user attribute)
to search all sets a user owns, that you can see just do @owner(.username:will)

to combine searches using the set modifiers and the user modifier
@set(#apples@owner(.username:will))


to see if something exists, without getting an iterator search result back put ? at the end of the search

Search results give back iterators and a page contents, use the iterator id to get the next page, 
iteration is one way only and can have duplicates in the results as things are updated in between calls for a page

todo max min for value , or regex for value
### Global Set

    All tokens are in a global set (G) so if needing to find any token at all use G for A 