# Live parents

each inherited parent has a live state, and can be turned off and on

    Live parent:
        current token id:
        static token_type id:
        activated: boolean - if not activated then all the attibutes given to the token by this type are turned off, alternate attributes of same id in other inheritied are not turned on

when the parent is turned off, then the live attributes from that parent, in the live attribute list, is also turned off


# Set context for changed attributes

When one token has a cluster turned off or on, the writer of the system has a choice to change this just for the set context, or if this is for any set.

see live attributes when they do this
