# Attributes


Attribute have an owner, a name, bounds, requirements, permissions, and a value.

While attributes have a lot to set, most of this is done in hte create and edit

When creating or editing the name of the attribute, do not put in the username, that is automatically added in the api

When creating the attribute, the user is the owner. After creation attributes cannot change ownership, but they can be copied.

An attribute can be edited in full until it is placed in a type. The attribute can be removed from the element type, and edited, and put back in.
But once an attribute has a live application in an element, it cannot be edited much except to retire it, which means nobody can use it for new stuff.
Only the owner, or someone in the owner's admin group can read and edit the attribute
Bounds are added as a mix of any bounds types

An attribute can be deleted if only it's not used anywhere

| Method | Path                        | TODO    | Route Name                   | Operation                                           | Args                                                                  |
|--------|-----------------------------|:--------|------------------------------|-----------------------------------------------------|-----------------------------------------------------------------------|
| Post   | attribute                   |         | core.attribute.create        | Makes a new attribute with caller as owner          | Required name: optional requirements, permissions, bounds, and value  |
| Patch  | attribute/edit/:id          |         | core.attribute.edit          | Edit Attributes                                     | Any detail of the attribute, sparse update                            |
| Get    | attribute/:id               |         | core.attribute.get           | returns full attribute info                         |                                                                       |
| Get    | attribute/read/:id          | *       |                              | Read Attribute , giving the value (default or live) | Optional element type, element,set, location, time                    |
| Get    | attribute/:id/bounds/ping   | * (set) | core.attribute.ping          | Determines if the attribute is in bounds            | Location, Time, Space, User  and Set                                  |
| Get    | attribute/:id/list/types    | *       |                              | Show where attribute is used in the types           | can provide a search using element type and other attributes,iterator |
| Get    | attribute/:id/list/elements | *       |                              | Show where attribute is used in the elements        | can provide a search,iterator                                         |
| Get    | attribute/list/managed      |         | core.attribute.list.managed  | Show attribute owned or managed by user             | can provide a search,iterator                                         |
| Get    | attribute/list/usage        |         | core.attribute.list.usage    | Show attribute not manage, but can be used          | can provide a search,iterator                                         |
| Delete | attribute/:id               |         | core.attribute.destroy       | Delete Attribute, if the user can                   |                                                                       |
| Get    | attribute/standard/list     |         | core.attribute.standard.list | Gets standard attributes                            |                                                                       |


        parent_attribute: attributes can optionally have a single parent
        user: can be one or none
        name: name of the attribute (unique to all attributes)
        is_retired: default false // if true then cannot be added to element types 

        meta:
            (can be in different langs or default lang)
            description: (in plain text or markup)
            name: (translate the name or a name that does not fit in the name rules for the legal name)
            standard-family: if named here this is a standard attribute
            author: who made this
            copywrite: any copywrite on the attribute content
            url: where to go for more info
            rating: marks adult or otherwise sensitive content (includes trigger warnings)
        bounds:
            // each bounds can have max one type of bounds: location, time , path
            read_bounds: []
            write_bounds: []

        requirements:
            elements:
                required_siblings: [attribute ids] for sharing the same element type or element
                forbidden_siblings: [attribute ids] cannot be in the same element or type
            sets:
                allergies: [force_rules] cannot be in the same set if force rules apply 
                affinities: [force_rules] this can only be in the set where force rules apply
        permissions:
            user_groups:
                usage: [] if empty then only the user's group can use this to create their types or add to elements 
                read: []  if empty anyone can read the attribute value
                write: [] if empty the admin group can change the attribute value.
            set_requirements: 
                is_read_policy_all: bool  
                is_write_policy_all: bool  
                read: [] attribute ids  : based on policy, if one, then any matches in a set makes it readable, or all must match
                write: [] attribute ids : based on policy, if one, then any matches in a set makes it readable, or all must match
        value:
            value_type: (name of the type of data )
            min: (numeric only)
            max: (numeric only)
            regex: (string only can set enums here)
            default:
            allow_null: default true, but can only be false if the default is set
        options:
            final:
            human:



When adding or editing in, or removing: bounds, attributes,  groups :
    The user needs to be able to read them (be member in user group of owner or else be allowed to read)
