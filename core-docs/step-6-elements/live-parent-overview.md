# Live parents

each inherited parent has a live state, and can be turned off and on

    Live parent:
        current element id:
        static element_type id:
        activated: boolean - if not activated then all the attibutes given to the element by this type are turned off, alternate attributes of same id in other inheritied are not turned on
        set: set id for set only changes
        parent: set id if traveling through parent child relationships
        toggled_at: timestamp


when the parent is turned off, then the live attributes from that parent, in the live attribute list, is also turned off


# Set context for changed attributes

When one element has a parent turned off or on, the writer of the system has a choice to change this just for the set context, the parent child relationship,
or if this is global.

