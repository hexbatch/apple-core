# Live attributes

When an element launches, then the top most attribute of each inherited parent is put on the live attribute list for it  

When an attribute is on an element, its live, and there is a record about the state of the attribute in the element

The same attribute on the same element can have different values based on its context (if in a shell)

* Attribute values has a microsecond time stamp of when last written to (updated_at) and or turned on (toggled_at)

When building the live attributes from a type:
* an attribute can be overwritten if the same type, or a child, is added. Siblings do not overwrite each other
* a shell context attribute is a new row for that element's attribute, with the shell id (the set id, but in)
* a child set attribute changes overwrites the parent
* no limit to how many live attributes that overwrite the earlier one. They stack by when applied.




    Live attribute:
        current element id: (null for global all elements)
        attribute id:
        overwritten_by : when a new live element is added that overwrites, this is filled in by what is overwriting it
        set: set id for shell only changes
        parent: this table id for the attribute (if shell) allows popping shells
        current_value: 
        time_to_live: datetime when this value expires, null for non remote server types, for constant
        activated: boolean - if not activated then this attribute does not count in the live, its skipped over
        toggled_at: timestamp 
        constant_status_type: (not_constant,is_constant,waiting_constant) enum --set a element creation, or first write

There can be duplicates of attributes here, from different parent types , or a shell context
When a context ends, it's removed from the lookup here and the element type attribute is used again

When an attribute is turned off, then the element has no attribute by that name or id. This counts in many scenarios

When a parent is turned off or on, its done in another table, which is linked to here (see live parents)

## Multiple inheritance for attributes

For multiple inheritance, that has duplicate attributes, the order of inheritance determines which one is used

When inheriting from a series of ancestors, the most recent (closest ancestor) one will be used

This includes default global states

# Set context for changed attributes

When an action writes to its parent element's attributes, the attribute can be written in normal, or shell context.
The action cannot choose which, its just whatever context this takes place.

Normal is the default, the attribute is changed and the same element in other sets see this change.

When this is shell context, this change is only seen by other reads in the same shell. (unless static, that is always global)
When the  shell ends, those changes are lost.


A shell is when selected elements from one set are put into a new set, and the elements can have return policies when the shell ends.
When a shell ends,the parent set's element's attribute value can be overwritten by, or merged with, the return

Internally, we remember this the changes, kept later or not, by using the live attribute structure above using a set and parent id , 
in a new row for that attribute.

We push those on when the attribute value is changed in a  shell context, and pop it off when the element leaves the set,or the shell ends.




# static attributes 

the statics defined in the type are here also, but cannot be overrriden by a set or shell context. Static is always global 
