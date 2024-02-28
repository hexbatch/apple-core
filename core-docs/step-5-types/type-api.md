#  Types


The owner of the type is the user who creates it. Type ownership cannot be transferred.

When editing types, the type must not be used anywhere, except one can always retire a type to prevent
the type from create new elements or being a parent in new types


Element types have an owner, options, attributes, and parents

Element types name and info are in its attributes

(other api here involve creating the element, getting element attribute values , and making a requirement)

| Method | Path                                      | Route Name | Description                               |
|--------|-------------------------------------------|------------|-------------------------------------------|
| Post   | type                                      |            | Makes a new type                          |
| Patch  | types/:id                                 |            | Sparse edit an type                       |
| Patch  | types/:id/states                          |            | Sparse edit the states of a type          |
| Delete | types/:id                                 |            | Delete Only if not used                   |
| Get    | types/:id/read                            |            | Gets the type definition and states       |
| Get    | types/:id/list                            |            | iterator, List a type where used          |
| Get    | types/list                                |            | iterator, List all the types              |
| Post   | types/server/protected_list/new           |            | Makes a new server protected list         |
| Post   | types/server/protected_list/:list/edit    |            | Edts a new server protected list          |
| DELETE | types/server/protected_list/:list/destroy |            | Deletes server protected list             |
| get    | types/server/protected_list/:list/read    |            | shows details about server protected list |

    
        user: one user owns the type
        allowed_creators: an optional user group
        name: using the naming rules
        is_retired: default false // if true then cannot be added to element types or make new elements
        is_final: bool, if true attribute cannot be inherited
        live_list: [ list of attributes that have live versions on the element, cannot be on the static list]
        private_live_list: [] list of live attributes that are live and only readable and writable by element owner
        static_list: [] list of attributes that are static, their values are set at the type level and shared by all elements
        private_static_list: [] list of static attributes that are live and only readable and writable by element owner
        live_actions: [] list of attributes that hold actions for for the elements
        static_actions: [] list of attributes that hold actions for for the type level events
        attributes_final: [list of final attributes that cannot be overwritten by children]
        parents: []  -- the order is important, this list also has which ones are on and off
        servers:
            protected-servers: list id/name of protected servers


## Creating a type
The user running this is the owner,
Required is name and at least one attribute.

## Reading a type

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

    

