# Element types

AN element type is a template to make an element from,

Element types can have many parents type parents,
but the attributes have to allow this to happen 
(attributes in different types may prevent some combinations)

Element types can have one or more parents, they can have many ancestors.
Elements cannot be ancestors or parents of themselves.

Types cannot change ownership, unless all the attributes and bounds and groups also change ownership, or are usuable by the new owner, at the same time.
(but elements can easiliy change owners)

Types can use attributes owned by others, as long as the permissions work out in the attribute permissions

    So: a type:
        user: one user owns the type
        ref: uuid
        allowed_creators: an optional user group
        name: using the naming rules
        is_retired: default false // if true then cannot be added to element types or make new elements
        is_final: bool, if true attribute cannot be inherited
        live_list: [ list of attributes that have live versions on the element, cannot be on the static list]
        private_live_list: [] list of attributes that are live and only readable by intersection of element owner group membership and attribute rules
        static_list: [] list of attributes that are static, their values are set at the type level and shared by all elements
        live_actions: [] list of attributes that hold actions for for the elements
        static_actions: [] list of attributes that hold actions for for the type level events
        attributes_final: [list of final attributes that cannot be overwritten by children]
        parents: []  -- the order is important, this list also has which ones are on and off

        

## Inheritance 

Can add parent to type as long as at least one attribute is readable

### Multiple inheritance for attributes

For multiple inheritance, there may be duplicate attributes,
the order of inheritance in the definition determines which one is used

When inheriting from a parent that has more than one attribute of the same id in its inheritance,
also use the most recent (the closest ancestor)  will be used

This includes default global states

### inherited or duplicated default global states

Each remote id has one stored global state under the key of that id.
Descendants of the remote have their own storage.

## Options

A type can mark its elements to be used in the human filter, to selectively hide elements made from this type in api calls if the human filter is on

A type can forbid being used to make other types


## Naming rules

Element types must have a name, this can be anything unique to that user. 
When using that name to search, then it is qualified by the username, seperated by a dot.


## allowed creators

Admins of the owners group can create elements from this type

Others can be given the permission to create elements from this type, or descendants from this type.
This means descendants can further restrict, but not expand, the allowed creators.
The group list to add others more than the creator's user group is optional, but can be added during definition
( cannot add after creation but can make new child for this)

Change membership on this group to give or remove element creation powers.
Admin ability, for the set group, does not make a creation ability difference, except to edit the members

## creation events
Each parent can have its own creation events. When an element is created, the creation events are fired from in order of inheritance,
so the furthest ancestors are fired at first. These actions can pass on the newly created element and owner to the remotes, and they can decide,
using any logic, to approve or disaprove this.

There can be messages given back to the user when this is denied. See events for how messages can be propogated to the user for failed events.


## starting parents as off

Some or all of the inherited parents can start in the off state, which means while their attributes override any ancestor or other type lesser in inheritance,
those attributes will not be available for reading or writing until that parent is turned on

# Attributes 

Attributes can be added to the type, so that they are readable in the element:

* attribues can be live, in which case they are readable and writable on the element. Each element can have a different value for same attribute
* or they can be static and the same values are in each element. Then the same attribute state is shared in all the elements.

Each attribute can be made readable or writable based on their bounds and permissions in their own definition.

Attributes can be on a final list, so that any child cannot override them (type will not be created if attempted)

Once a type has an element created, the type cannot be changed. Attributes cannot be added or removed to the type.

## Defining action listeners 

attributes can be placed in the live_actions if they hold an action, these have state in the elements 
attributes can be placed in the static_actions same way, but for type wide events

# Privacy for element owners
if the type defination has private_live_list entries, then these cannot be on the other attribute lists, except for the final.
Behind the scenes a new attribute is made that inherits from this attribute, that has a group to intersect membership of the parent,
and it is that attribute that is put into the live list for the element.

This allows for values to be hidden from the people who control the type, it allows privacy


