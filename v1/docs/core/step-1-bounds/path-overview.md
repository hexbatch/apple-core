# Set Path boundaries

Means the attribute can only be active when the token is in one of a group of set expressions

A set path bounds is one or more of the set expressions.

So, the attribute is only on when then token is inside those set conditions, and then the attribute might be readable or writable from that set only.

The same token would have different on or off attributes based on reading it in another set, which it can belong to, at the same time.

## Set expressions

each token set has an optional name and token, the token can have attributes with values
so, a path could be identified by name#token_type.attribute:value

And there can be wild cards too
* #token_type.attribute:value (no name of path)
* name.attribute (no token type or attribute value)
* .attribute:value (only attribute can also just a check the attribute is set and readable)

A set expression can also be a parent/child relationship using the notation of being able to skip
#token_type.attribute:value/.b-attribute>name





