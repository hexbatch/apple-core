# Set Path boundaries

A set path bounds is one or more search expressions.

Means the attribute can only be active when the element is in a set matched by the search path.
The search path must end in an element being the set, or a set containing something.

So, this means api calls when doing stuff to elements in a set, activate any possible path bounds to turn things on or off.
This is not related to any other set the api call is involved in. Only when changing elements or sets in an api call,  the set that is changed or has elements inside it change.

Path bounds only affect attributes inside the set the bounds is activated



So, the attribute is only on when then element is inside those set conditions, and then the attribute might be readable or writable from that set only.

The same element would have different on or off attributes based on reading it in another set, which it can belong to, at the same time.

## Set expressions

(see search expressions for more info)

each element set has an element with an id, the element can have attributes with values
so, a path could be identified by name#element_type.attribute:value

And there can be wild cards too
* #element_type.attribute:value (no name of path)
* name.attribute (no element type or attribute value)
* .attribute:value (only attribute can also just a check the attribute is set and readable)

A set expression can also be a parent/child relationship using the notation of being able to skip
#element_type.attribute:value/.b-attribute>name

a set expression can also be a required element sibling in a set

a set expression can be conveyed to be a set that has some relationship (other set linking to it, a parent or a child)


        so a path-bound:
        user: id
        name: name of the bounds (unique to the user's bounds)
        search_expressions: array of search expressions ending at a set the element can belong to


