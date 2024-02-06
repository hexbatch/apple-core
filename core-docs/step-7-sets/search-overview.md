# Gathering operations

Operations similar to grep of find for the attribute values and their static content, in a file structure (treat links like siblings in a folder or more accurately here sibling sets)

operations to make simple key value objects for each set ( singular or with siblings (links) or children) with attribute names the keys and static values
each element can be a new object of (attribute:value) and these can optionally be left alone or condensed to a single layer of key values
if condensed, then the values for each attribute turn into an array for each set


Search results of sets lists the set's parent.

searching can filter static values via regex, numeric_range, comparison (comparisons can be nested), or strict string match

    search: A source,  Z  attributes , T optional pattern, options to recurse levels, to filter, to condense => simple object




## Using tags to gather - path specifier

Sometimes want to find stuff in set relations, where there is an element in one set, and another element in a set elsewhere, or an element path,

this element path can be sort of like a url apples/bananas/pears

this will start the search for any sets that have the apples element, then for any sibling or children sets that have bananas, then for any s or c sets that have pears, then do the search

optionally, there can be gaps in between the sets that have the tags, so we may not find apples in the parent set, but in some descendant, then the bananas would be further in a grandchild, etc

both tags and attribute names can be searched for this way, and the search combined

so, in this notation # means an element name, and . means an attribute and :x means value of x, and > means no gaps

that means to search for #apples>.bears:2/#witches.broomsticks:wooden

would be to start looking in the top set for elements called apples,
then for any immediate children or siblings if there is a set with an attribute of bears that has a value of 2,
for any descendant or sibling chain find witches element that have wooden broomsticks

A path specifier can be added to any set operation

Once can count the path specifier in a set, this is used for some actions

## searches by set relationships

Searches by set relationships. While a space or > can mean immediate or gap set relations

one can put in required relationships in a set too, this @ is done before the #.
@child(#ads.none) @parent(.persimmons) @link(#roads)

so #apples>@child(#ads.none).bears:2

searches first sets of apple elements, then for any immediate child whose set element of type 'ads' with attribute none fine - find an element with attribute bear value 2 in that set

to start a search at a particular set, use the @set(#apples)

to list all the elements in a set, do not put any modifiers after the last set:


to search with ownership use the @owner(some user attribute)
to search all sets a user owns, that you can see just do @owner(.username:will)

can also search for elements in a set owned by a user : @owner(.username:will)#apples, @owner(.email:*.gmail.com).green:free

to combine searches using the set modifiers and the user modifier
@set(#apples@owner(.username:will))


to see if something exists, without getting an iterator search result back put ? at the end of the search

Search results give back iterators and a page contents, use the iterator id to get the next page,
iteration is one way only and can have duplicates in the results as things are updated in between calls for a page

## Value ranges
 can add ranges to values bears:2,4, bears:,4 
 can add regex or enums to values bears:black|red|pink


## Search objects

Searches can be saved for future use, search json looks like an array of paths

    a search
    id
    user
    [search parts],
    optional requirement to order
    optional requirement to filter

each search part is:
        
    skip: > or / (optinal if left out then > )
     set conditions:
        owner:
        relationship_to: search part
    element name: (optional )
    element_id: (optional)
    element_owner: (optional)
    attributes:
        [{
            attribute name or id,
            value (literal or range or regex)
        }]


the id here is the guid generated, not the proper element name

### Search objects extendable

Extensions can add in new fields in the overall and part of the search


# Other search operations

---------

@mutual()

returns sets that share the same elements in this path

can combine with @set() or other, when finding the @set, then will use that set element

@set and @mutual can have an upper or lower number for members or connected sets
@set(.what)[2,5] between 2 and 5 different elements with attribute .what
can also do [2,] for lower bounds and [,5] for upper

will give paginated if too big

------------

nested @ stuff
@mutual(@child(@user('will')))

----------------

Ancestry modifiers

~ means descended from but not including

= means exact element no descendants

=#cats.furry   -- matches cats element only
~#cats.furry   -- only descendants of this element

## use in attributes and elements

---------------------
multiple things
, comma separates  use in @set and @mutual and multiple inheritance

#catty@set(.long, =#tickle)  gets sets defined by catty or descenents which contain both elements with long attribute and exact match for tickle

@mutual(.run, .go) gets interconnecting sets that share one or more elements which have the attributes of .run and .go


(#runs, =#running).poking  gets an element that inherits from both runs (and descendants) and running exact

--------------------------------

@child(.who) selects any child that is a set that contains the .who attribute
@child(.who).what  above but the child element defining the set must have a who attribute


------------------------

.bookmark @child(@mutual(.gosh) )#go  an element defining a set must be a child of another set that has a bookmark attribute,
and contain at least two set elements who have a mutual element of attribute .goth

-----------------
@view is shorthand for @set(@mutual)
