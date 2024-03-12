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

| Method | Path                         | TODO    | Route Name                    | Operation                                           | Args                                                                  |
|--------|------------------------------|:--------|-------------------------------|-----------------------------------------------------|-----------------------------------------------------------------------|
| Post   | attribute                    |         | core.attributes.create        | Makes a new attribute with caller as owner          | Required name: optional requirements, permissions, bounds, and value  |
| Patch  | attributes/edit/:id          |         | core.attributes.edit          | Edit Attributes                                     | Any detail of the attribute, sparse update                            |
| Get    | attributes/:id               |         | core.attributes.get           | returns full attribute info                         |                                                                       |
| Get    | attributes/read/:id          | *       |                               | Read Attribute , giving the value (default or live) | Optional element type, element,set, location, time                    |
| Get    | attributes/:id/bounds/ping   | * (set) | core.attributes.ping          | Determines if the attribute is in bounds            | Location, Time, Space, User  and Set                                  |
| Get    | attributes/:id/list/types    | *       |                               | Show where attribute is used in the types           | can provide a search using element type and other attributes,iterator |
| Get    | attributes/:id/list/elements | *       |                               | Show where attribute is used in the elements        | can provide a search,iterator                                         |
| Get    | attributes/list/managed      |         | core.attributes.list.managed  | Show attribute owned or managed by user             | can provide a search,iterator                                         |
| Get    | attributes/list/usage        |         | core.attributes.list.usage    | Show attribute not manage, but can be used          | can provide a search,iterator                                         |
| Delete | attributes/:id               |         | core.attributes.destroy       | Delete Attribute, if the user can                   |                                                                       |
| Get    | attributes/standard/list     |         | core.attributes.standard.list | Gets standard attributes                            |                                                                       |


        



When adding or editing in, or removing: bounds, attributes,  groups :
    The user needs to be able to read them (be member in user group of owner or else be allowed to read)
