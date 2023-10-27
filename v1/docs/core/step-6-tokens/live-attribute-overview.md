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