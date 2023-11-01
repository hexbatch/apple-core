# Live attributes

When a token launches, then the top most attribute of each inherited parent is put on the live attribute list for it  

When an attribute is on a token, its live, and there is a record about the state of the attribute in the token

    Live attribute:
        current token id:
        static attribute id:
        static source of attribute: token type id, or live if just stuck on
        current_value: 
        activated: boolean - if not activated then this attribute does not count in the live, its skipped over
        local_state: if this attribute holds an action, script or remote

There can be duplicates of attributes here, one from the token type and one from a live attribute
When a live attribute is removed from the token, it's removed from the lookup here and the token type attribute is used again

When an attribute is turned off, then the token has no attribute by that name or id. This counts in many scenarios


## Multiple inheritance for attributes

For multiple inheritance, that has duplicate attributes, the order of inheritance determines which one is used

When inheriting from a series of ancestors, the most recent (closest ancestor) one will be used

This includes default global states

# Set context for changed attributes

When one token changes another token's attributes, the writer of the system has a choice to change this just for the set context, or if this is for any set.

When this is per set, when the token is taken out of the set, those changes are lost.
The only time changes are remembered are when the token is traveling through a parent child set relationship.
This is optional, and allows the attribute to regain any changes made in the parent when it returns from the child.
This can be nested in different levels of parent child travel, each parent can remember it settings until it leaves that parent.


Internally, we remember this the changes, kept or not, by using the stack id, the live attribute id, and the value there in a table row.
We push those on when the attribute value is changed in a set, and pop it off when the token leaves the set, not going to a child.