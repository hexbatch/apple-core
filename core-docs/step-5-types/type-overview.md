# Element types

AN element type is a template to make an element from,

Element types can have many parents type parents,
but the attributes have to allow this to happen 
(attributes in different types may prevent some combinations)

Element types can have one or more parents, they can have many ancestors.
Elements cannot be ancestors or parents of themselves.

Types cannot change ownership, unless all the attributes and bounds and groups also change ownership, or are usuable by the new owner, at the same time.
(but elements can easiliy change owners)

Types can use attributes owned by others, as long as the permissions work out in the owner_user_groups

    So: a type:
        user: one user owns the type
        allowed_creators: an optional user group
        name: using the naming rules
        is_retired: default false // if true then cannot be added to element types or make new elements
        options:
            final:
            human:
        attributes: []
        parents: []  -- the order is important, this list also has which ones are on and off
        global_states: [attribute_id, state]



Global states are kept here for remotes.

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


## starting parents as off

Some or all of the inherited parents can start in the off state, which means while their attributes override any ancestor or other type lesser in inheritance,
those attributes will not be available for reading or writing until that parent is turned on

