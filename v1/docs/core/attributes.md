# Attributes

Are the core of the api here.

Attributes can be defined by the code, in which case they are not owned, and cannot be edited or deleted.

Attributes can be created|edited|deleted by a user.

Attributes can be restricted to only be used in a token or type-group if there are one or more other specified siblings.
These siblings can have an ancestor or parent that matches this.

Attributes can have an optional whitelist to allow which users can own, change the value of, and read this value of this attribute.
A descendant can change the groups, but only by limiting the groups further

Attribute values can be a number, string, json, markdown, binary (image , pdf only), a script to run, location

string specific types can be :
* iso date time, color, url, email, social account , phone, any
* number is any numeric value
* location is lat, lon

An attribute is defined, when applied its value is put next to the action's instantiated values (a token or type group has a list of their attributes and current values)
Starting out, the default value is used, if no default then null

A new attribute can be made that has all the features of its parent, however any new things added to this will override the parent's

Attribute have an owner, a name, bounds, requirements, permissions, and a value

    so an attribute:
        parent_attribute: attributes can optionally have a single parent
        user: can be one or none
        name: name of the attribute (unique to all attributes)
        bounds:
            map: []
            time: []
        requirements:
            required_siblings: []
        permissions:
            owner_user_groups: [] if empty then anyone can use this to create their tokens and token-sets
            read_user_groups: []  if empty anyone can read the attribute value
            write_user_groups: [] if empty anyone can change the attribute value.
            set_requirements: 
                read: [] attribute ids
                write: [] attribute ids
        value:
            value_type: one of: numeric, string, string specific type,json, markdown, binary, action, script
            min: (numeric only)
            max: (numeric only)
            enum: (string only if no regex)
            regex: (string only if regex set then enum ignored)
            default:
            allow_null: default true, but can only be false if the default is set

## attribute permissions
Permissions can be given to user groups to read, write or create

By default, if no permissions, attributes can be read by everyone, and only written to by the owner


### set requirements

Conditional permissions can also be defined to allow the read and write to only occur when another attribute in the same token set is present.
This attribute does not need to be in the same token.


### Required set attributes for read

When this is set, actions do not run if that attribute cannot be read by anyone. This allows scripts to run not only when the token is at a certain location and time,
But when the token is combined with certain other tokens in a set

  
