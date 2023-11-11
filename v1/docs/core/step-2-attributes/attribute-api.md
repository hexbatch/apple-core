# Attributes

attribute api defined at [attributes.yaml](../../../api-docs/attributes.yaml)

Attribute have an owner, a name, bounds, requirements, permissions, and a value.

While attributes have a lot to set, most of this is done in hte create and edit

When creating or editing the name of the attribute, do not put in the username, that is automatically added in the api

When creating the attribute, the user is the owner. After creation attributes cannot change ownership, but they can be copied.

An attribute can be edited in full until it is placed in a token-type. The attribute can be removed from the token type, and edited, and put back in.
But once an attribute has a live application in a token, it cannot be edited much except to retire it, which means nobody can use it for new stuff.
Only the owner, or someone in the owner's admin group can read and edit the attribute
Bounds are added as a mix of any bounds types

An attribute can be deleted if only it's not used anywhere

| Method | Path                      | Route Name | Operation                                             | Args                                                                 |
|--------|---------------------------|------------|-------------------------------------------------------|----------------------------------------------------------------------|
| Post   | attribute                 |            | Makes a new attribute with caller as owner            | Required name: optional requirements, permissions, bounds, and value |
| Patch  | attribute/edit/:id        |            | Edit Attributes, if possible, sparse                  | Any detail of the attribute, sparse update                           |
| Put    | attribute/edit/:id        |            | Edit Value , if possible, full replacement            | All the values for the definition                                    |
| Get    | attribute/:id             |            | returns full attribute info                           |                                                                      |
| Get    | attribute/read/:id        |            | Read Attribute , giving the value (default or live)   | Optional token type, token,set, location, time                       |
| Get    | attribute/:id/bounds/ping |            | Determines if the attribute is in bounds              | Location, Time and Set                                               |
| Get    | attribute/:id/permissions |            | Determines if the attribute can be read or written to | User,Location, Time and Set                                          |
| Get    | attribute/:id/list/types  |            | Show where attribute is used in the types             | can provide a search using token type and other attributes,iterator  |
| Get    | attribute/:id/list/tokens |            | Show where attribute is used in the tokens            | can provide a search,iterator                                        |
| Delete | attribute/:id             |            | Delete Attribute, if the user can                     |                                                                      |


        parent_attribute: attributes can optionally have a single parent
        user: can be one or none
        name: name of the attribute (unique to all attributes)
        description: some text explaining why this attribute is used, etc, the author or other info
        is_retired: default false // if true then cannot be added to token types 
        bounds:
            activity_bounds: []
            read_bounds: []
            write_bounds: []

        requirements:
            tokens:
                required_siblings: [attribute ids] for sharing the same token type or token
                forbidden_siblings: [attribute ids] cannot be in the same token or type
            sets:
                allergies: [force_rules] cannot be in the same set if this attribute is in any of the other tokens. 
                affinities: [force_rules] this must be in the same set somewhere before the token can be added to the set
        permissions:
            user_groups:
                usage: [] if empty then only the user's group can use this to create their types or add to tokens 
                read: []  if empty anyone can read the attribute value
                write: [] if empty the admin group can change the attribute value.
            set_requirements: 
                read: [] or {} attribute ids  : if this array, if one in a set can read, if object then all must be in set to read
                write: [] attribute ids : if this array, if one in a set can write, if object then all must be in set to write
        value:
            value_type: one of: numeric, string, string specific type,json, markdown, binary, action, script,url, token id
            min: (numeric only)
            max: (numeric only)
            regex: (string only can set enums here)
            default:
            allow_null: default true, but can only be false if the default is set



When adding or editing in, or removing: bounds, attributes,  groups :
    The user needs to be able to read them (be member in user group of owner or else be allowed to read)