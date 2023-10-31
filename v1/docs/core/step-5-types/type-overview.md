# Token types

A token type is a template to make a token from,

Token types can have many parents type parents,
but the attributes have to allow this to happen 
(attributes in different types may prevent some combinations)

Token types can have one or more parents, they can have many ancestors.
Tokens cannot be ancestors or parents of themselves.

Types cannot change ownership.

Types can use attributes owned by others, as long as the permissions work out in the owner_user_groups

    So: a token-type:
        user: one user owns the type
        allowed_creators: a list of user groups or individual users who can make tokens from this type
        name: using the naming rules
        is_retired: default false // if true then cannot be added to token types or make new tokens
        options:
            allow_changed_map_bounds: boolean
            allow_changed_time_bounds: boolean
            allow_changed_path_bounds: boolean
            allow_actions: boolean
            attribute_final_list: [or or more attribute ids that children or descendants cannot have]
        attributes: []
        parents: []  -- the order is important
        parents_starting_off: [] any of the above (optional)
        global_states: [attribute_id, state]



Global states are kept here for remotes and scripts.

## Inheritance 

### Multiple inheritance for attributes

For multiple inheritance, there may be duplicate attributes,
the order of inheritance in the definition determines which one is used

When inheriting from a parent that has more than one attribute of the same id in its inheritance,
also use the most recent (the closest ancestor)  will be used

This includes default global states

### inherited or duplicated default global states

Each script or remote id has one stored global state under the key of that id.
Descendants of the script or remote have their own storage.

## Options

A token type can be made unchangeable in part or whole. Different bound types an be made final.
So can any attributes, to make sure actions cannot be overridden.

If any of the event attributes are on the final list, then any descendant cannot do that event.
This includes creation or destruction


## Naming rules

Token types must have a name, but the name must start with the username that created it, followed by a dot.
Then the alias for the word 'type', another dot, then the name must be unique

Aliases for the token type can be created, via aliases, in different languages. 
They must follow the naming convention and be unique

## allowed creators

Others can be given the permission to create tokens from this type, or descendants from this type.
This means descendants can further restrict, but not expand, the allowed creators.
Group lists can be used to change the users allowed.


## starting parents as off

Some or all of the inherited parents can start in the off state, which means while their attributes override any ancestor or other type lesser in inheritance,
those attributes will not be available for reading or writing until that parent is turned on
