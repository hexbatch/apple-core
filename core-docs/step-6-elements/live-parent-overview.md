# Live parents

each inherited parent has a live state, and can be turned off and on

    Live parent:
        element id:
        element_type id: //each of the top parents of the type from the element
        activated: boolean - if not activated then all the attibutes given to the element by this type are turned off, alternate attributes of same id in other inheritied are not turned on
        set: set id for shell changes
        parent: this table id for the type (if shell) allows popping shells
        parent: set id if traveling through parent child relationships
        toggled_at: timestamp


when the parent is turned off, then the live attributes from that parent, in the live attribute list, is also turned off


# Set context for changed attributes

A parent can be toggled in a shell context, in this case, we add a new row with the set and parent shell put in, to add in the context,
and when the shell ends, we remove this row
