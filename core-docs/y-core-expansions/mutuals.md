# Mutuals 


Mutual sets:
    Two or more sets that have one or more exact same tokens in their collections are connected together by these tokens, but not in a linked relationship
    These can be many sets bound together in different patterns and geometries. Mutually bound sets can also be connected via parent child relationships and links.
    Can select these relations into a set known as a view, which only contains mutually connected set systems (all the sets have to be directly or indirectly sharing the same tokens).

---------------------------------


A token can belong to any number of sets at the same time.
When two or more sets share that token, they have something in common.

What is a mutual group of sets?
If I find a set, then discover other sets have one or more of the same tokens.
Then I can look at those other sets, and find what shares tokens with them.
These tokens may be different from the ones shared with the first set.
After I do this as much as possible, or until I decide to stop including sets, then I have something called a mutual group of sets.
The sets are linked by shared tokens. The shared tokens might have other relationships too.

What is a view?
Views are sets that produce no events: there are no effects when tokens are put into or removed from a view, and the tokens in a view do not react to each other.
Set operations on views have no side effects, tokens in the set do not react to value changes or what is happening in the set. Allergies do not apply.
Think of a view as a read only selection of tokens. Views can be used for any tokens, not just mutuals. But they are necessary when looking at mutuals.
Views can have every set operations done to them as normal sets, they are sets themselves that are no different other than the no events.
A set is made into a view, and vice versa by adding or removing an attribute system defined

Mutual sets have a topology. Things can be done with them and their shared tokens.
* We can put these tokens into a new set
* We can do group aggregation operations on the attributes of these tokens: such as sum, or counts or averages or concatenation or json operations or min or max
* We can do these aggregations on families of these attributes or all the attributes, much like the group by in sql
* We can do operations on these mutual sets such as union (or), intersection (and) , difference (xor), and complement (those in A not in B)
* Because these operations do not cause events to possibly cascade into lengthy operations, we can allow for new custom mutual operations
* We can do topology operations on these mutual sets, do overlays and superimpose them: creating new groups of mutuals or selecting common tokens for things that match up
* For example, say I have  5 sets connected in a ring, and I match it up to a larger set of mutuals where there are some rings here and there.
I can match to all the rings, and collect tokens there. Or I can match to just rings of 5.


Mutual operation categories:
* Reduction of attribute values, and assign these group calculations to attributes on any token we can write. This can be dynamic or typed attributes.
* Select some or all of the shared tokens into a new set, or search result
* Split a mutual set, make a new mutual set from other mutuals, and combine mutual sets.
* Discover the common bounds for all the sets in a mutual group: the pattern of time all the sets exist, or a shared area on the map
* Do aggregation operations on the bounds in a mutual group

Selecting tokens from mutuals
* the shared tokens are of interest and can be filtered by different priorities
* select tokens that are shared N,M times
* select shared tokens based on attribute types and values and ranges of values
* after selecting, can filter by attribute or token type into different sets or sub aggregation operations


Aggregation operations:
Any tokens in a set can be reduced and have that number applied to an attribute (new or already existing) on a token. The set can be filtered to allow for sub-group operations and reductions.


Mutuals can make filters by using their aggregations and counting per family of attributes, or per attribute

Custom mutual operators : no event side effects so these operators can do anything!
* add new selection operators to choose a mutual group
* add new combination and other ways to manipulate groups


operations:

Selecting
----------

Can use a search to get the mutuals that share a token type
But there are interconnected mutuals that share more than one, and these may not be related to others except indirectly

But there are better ways: can pick out which sets using mutual select operations
    These can pick out a starting set based on some criteria, and then a limit of how far from the set to go. and will find interconnected paths
        tokens (sets connected by a, that shares a token b, find sets connected by b, that shares a c, etc)

Different selects can choose differently using different options: ie(topology or start at certain shared token)
    However any select will return sets that are all connected, there are no disconnected sets or groups of sets
    Can nest select operations to trim down from the start

Editing sets:
----------------


* Connect two sets with same token
* remove a shared token from a group of mutual sets

--------------------
grouping:
* union (or), intersection (and) , difference (xor), and complement (those in A not in B)

-----------------------


Selecting tokens in mutual sets:
these selections are put in a new set, where aggregation can happen, or other operations

    concept of a strong token: the more a token is shared in a mutual group, the stronger it is
    concept of a strong attribute: the more an attribute is in selection of strong tokens, the stronger it is
    can select using strength, along with other things, like ancestry of token or attribute
    can select by min and max shares of a set in a group of mutual (set a has 3 connections set b has 5) select for more than 4
    can select using number of times a token shared

-----------------
    custom select operations can be registered
allow macros to be made and remembered:
do push and popup on each pop to set precedent
api to combine , list, get, delete
use macro id when calling view operation (is this set too or just mutual operations)
marcos can call a remote or script


---------------------------
When a mutual is made, it is showing the tokens are they are when the api call was made. Tokens can change after that.
Mutuals do have the option to be live, in other words updated so the next time they are read, or used, it reflects accurately

In the code, when a token is part of a live mutual, then when that token leaves or enters a set, the mutual is updated.
This may break some or all of the mutual.

A mutual can have event listener for when a mutual is "evaporated" and is no more, or when its changed. static mutuals, those not live, receive no such updates though.

-----------------------------------------

Entanglement, its possible to add in a live or static mutual to a set. If a static mutual, this is just adding in the strong tokens and that is all there is.
Live mutuals though, can move their tokens in and out of a set by moving the set holding the live mutual in and out. If a mutual mutates then more tokens are added or removed as a result.
Evaporated mutuals remove all the tokens.

A set can host multiple entanglements at the same time. Duplicate tokens from more than one entanglement are, of course, only added once to the host set.
When an entanglement enters, if the set has event listeners, then all the tokens have to accepted, or none of them.
When a mutual mutates, then if the set denies the exit or entry of the token, then all the tokens from that mutual are removed, even if a same token, also in the mutual,
 has been added separately, and there are no events called here. If more than one entanglement is in a set, and one gets evicted, and the evicted one has one or more shared tokens in another mutual,
 then that other mutual gets evicted too.

----------------------------------------------------------------------------

# Mutual operations:

* Aggregation operations: can do aggregation operations on mutual sets. The operations can be written to a single attribute on a target token 
    Agg op to combine ordered tokens in a set to json array
* Strong attribute operations
* Superimposed operations.
* Operations on mutual sets.
* Selection on mutuals, this can be custom, see below.
* Mutual set selection: different ways to select mutual sets into a view
    When selecting, can put limits of how many mutual distance, and limit the mutual token types.
* Able to make macros. Macros made from push and pop of other operations. Only mutual operations allowed because they do no events
    Macros can be run by actions (not using script or remote, just set the macro id)
* Can register custom macros in the core, not by users, but by plugin. For instance macros to select via topology and area charges on mutual entanglements.