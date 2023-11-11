# Set Path boundaries

A set path bounds is one or more search expressions.

Means the attribute can only be active when the token is in a set matched by the search path.
The search path must end in a token being the set, or a set containing something.

So, this means api calls when doing stuff to tokens in a set, activate any possible path bounds to turn things on or off.
This is not related to any other set the api call is involved in. Only when changing tokens or sets in an api call, its the set that is changed or has tokens inside it change.

Path bounds only affect attributes inside the set the bounds is activated



So, the attribute is only on when then token is inside those set conditions, and then the attribute might be readable or writable from that set only.

The same token would have different on or off attributes based on reading it in another set, which it can belong to, at the same time.

## Set expressions

(see search expressions for more info)

each token set has a token with an id, the token can have attributes with values
so, a path could be identified by name#token_type.attribute:value

And there can be wild cards too
* #token_type.attribute:value (no name of path)
* name.attribute (no token type or attribute value)
* .attribute:value (only attribute can also just a check the attribute is set and readable)

A set expression can also be a parent/child relationship using the notation of being able to skip
#token_type.attribute:value/.b-attribute>name

a set expression can also be a required token sibling in a set

a set expression can be conveyed to be a set that has some relationship (other set linking to it, a parent or a child)


        so a path-bound:
        user: id
        name: name of the bounds (unique to the user's bounds)
        search_expressions: array of search expressions ending at a set the token can belong to


