# Live attributes

When an element launches, then the top most attribute of each inherited parent is put on the live attribute list for it  

When an attribute is on an element, its live, and there is a record about the state of the attribute in the element

The same attribute on the same element can have different values based on its context (set membership or parent child relations)

* Attribute values has a microsecond time stamp of when last written to (updated_at) and or turned on (toggled_at)
* an attribute can be overwritten if the same type, or a child, is added. Siblings do not overwrite each other
* an attribute added to the element can overwrite global attribute for that element only
* a set context attribute will overwrite a per element attribute, or a type attribute
* a child set attribute changes overwrites the parent
* no limit to how many live attributes that overwrite the earlier one. They stack by when applied.




    Live attribute:
        current element id: (null for global all elements)
        attribute id:
        overwritten_by : when a new live element is added that overwrites, this is filled in by what is overwriting it
        set: set id for set only changes
        parent: set id if shell
        current_value: 
        activated: boolean - if not activated then this attribute does not count in the live, its skipped over
        toggled_at: timestamp 
        local_state: if this attribute holds a remote

There can be duplicates of attributes here, one from the element type , the element and the context
When a context ends, it's removed from the lookup here and the element type attribute is used again

When an attribute is turned off, then the element has no attribute by that name or id. This counts in many scenarios


## Multiple inheritance for attributes

For multiple inheritance, that has duplicate attributes, the order of inheritance determines which one is used

When inheriting from a series of ancestors, the most recent (closest ancestor) one will be used

This includes default global states

# Set context for changed attributes

When an action writes to its parent attributes, the attribute can be written in normal, set or shell context.
Normal is the default, the attribute is changed and the same element in other sets see this change, 
unless they have their values written to in their own set context.

When this is set context, this change is only seen by other reads in the same set. 
When the element is taken out of the set, those changes are lost.

Actions can also write to the element but in the context of a shell's children.

A shell is when selected elements from one set are put into a new set, then the parent set's element's attribute can be written by that action to be in 
the parent set's context.

Internally, we remember this the changes, kept later or not, by using the live attribute structure above using a set and parent id , 
in a new row for that attribute.

We push those on when the attribute value is changed in a set or shell context, and pop it off when the element leaves the set,or the shell ends.




# static attributes 

the statics defined in the type are here also, but cannot be overrriden by a set or shell context. Static is always global 
