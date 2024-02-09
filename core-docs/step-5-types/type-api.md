#  Types


The owner of the type is the user who creates it. Type ownership cannot be transferred.

When editing types, the type must not be used anywhere, except one can always retire a type to prevent
the type from create new elements or being a parent in new types


Element types have an owner, options, attributes, and parents

Element types name and info are in its attributes

(other api here involve creating the element, getting element attribute values , and making a requirement)

| Method | Path            | Route Name | Description                         |
|--------|-----------------|------------|-------------------------------------|
| Post   | type            |            | Makes a new type                    |
| Patch  | type/:id        |            | Sparse edit an type                 |
| Patch  | type/:id/states |            | Sparse edit the states of a type    |
| Delete | type/:id        |            | Delete Only if not used             |
| Get    | type/:id/read   |            | Gets the type definition and states |
| Get    | type/:id/list   |            | iterator, List a type where used    |
| Get    | types/list      |            | iterator, List all the types        |

    
        user: one user owns the type
        name: using the naming rules
        allowed_creators: a list of user groups or individual users who can make elements from this type
        is_retired: default false // if true then cannot be added to element types or make new elements
        options:
            allow_changed_map_bounds: boolean
            allow_changed_time_bounds: boolean
            allow_changed_path_bounds: boolean
            allow_actions: boolean
            attribute_final_list: [or or more attribute ids that children or descendants cannot have]
        attributes: []
        parents: []  -- the order is important
        parents_starting_off: [] any of the above (optional)
        global_states: [attribute_id, state] (read only unless use api to set the state)


## Creating a type
The user running this is the owner,
Required is name and at least one attribute.

## Reading an type

When getting the type state, the type state for the remotes running on it can be seen


## Editing a type

Any admin in the user's group can edit, but can only edit if not in use
Any part can be changed if type not used.
When type is used, only the retired status and the allowed users can be set or changed,
and that only affects things made in the future. Elements already created are not affected.

One cannot edit a type when elements are made or children are made.



## Listing where a type is used at

Gives a list of types that inherits this, use wide option to list the descendants to N levels.
Can filter for attributes on the element too. 

## Listing elements that are created from this type

Gives list of elements, wide option to list elements made by descendants to N levels

## Listing types owned by this user

filter by attribute name or type parent or ancestor of N level range, or some combinations

