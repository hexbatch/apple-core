# Attributes

Are the core of the api here. Attributes have value. By default, attributes can be read by everyone and written by no one else but the owner admin group

Attributes can be defined by the code, in which case they are not owned, and cannot be edited or deleted.

Attributes can be created|edited|deleted by a user.

Attributes can be restricted to only be used in a token if there are one or more other specified siblings.
These siblings can have an ancestor or parent that matches this.

Attributes can have an optional whitelist to allow which users can own, change the value of, and read this value of this attribute.
A descendant can change the groups, but only by limiting the groups further

Attribute values can be a number, string, json, markdown, binary (image , pdf only), a script to run, location, an action, a remote

A script and remote is writable, when a write happens, the last good ts is unset for the token, and the script or remote is passed in the write value

string specific types can be :
* iso date time, color, url, email, social account , phone, markdown,any
* number is any numeric value
* location is lat, lon

An attribute is defined with a starting value.
When it is applied to a token type, and the type makes a token. Then the attribute's value can be used, unless overridden, and put on the token's live values.
This value can be changed by any who can write to the token

Starting out, the default value is used, if no default then null

A new attribute can be made that has all the features of its parent, however any new things added to this will override the parent's

Attribute have an owner, a name, bounds, requirements, permissions, and a value

Attributes can have optional explaining text

options:
  * Attributes can be constant in that their defined value never changes. Constants cannot have actions, remotes or scripts
  * Attributes can be static so that their value is always read and written from the type and not the token
    * static attributes cannot have actions but can have scripts and remotes
  * Final means cannot be used as a parent
  * Human status, to selectively hide this attribute from searches if the human filter is on.


      so an attribute:
          parent_attribute: attributes can optionally have a single parent
          user: can be one or none
          name: name of the attribute (unique to all attributes)
          description: some text explaining why this attribute is used, etc, the author or other info
          is_retired: default false // if true then cannot be added to token types
          bounds:
              // each bounds can have max one type of bounds: location, time , path
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
              value_type: (name of the type of data )
              min: (numeric only)
              max: (numeric only)
              regex: (string only can set enums here)
              default:
              allow_null: default true, but can only be false if the default is set
          options:
              constant:
              static: (can be static or constant)
              final:
              human:  

## Value types

Data can be marked as:

* numeric
* string
  * regular strings
  * json
  * markdown
  * html
  * xml
  * binary 

* points to something 
  * user_id
  * user group id
  * attribute id
  * token id
  * script
  * remote
  * action
  * attribute
  * search
  * bounds
  * view
  * mutual
  * container


* Coordinates
  * map (lat lon)
  * cartesian (x,y,z)


## attribute permissions
Permissions can be given to user groups to read, write or create

By default, if no permissions, attributes can be read by everyone, and only written to by the owner

To make attributes read only or write only, make the set_requirements be an attribute that is defined to be allergic to this attribute

Ownership groups can use this to add to their own token types and tokens.
Note that once someone else has permission to create with this attribute, and they make something with it, then that can never be taken back.
But the attribute could be retired to prevent any new use

### set requirements
When an api uses a set context,

Conditional permissions can also be defined to allow the read and write to only occur when another(or several) attribute in the same token set is present.
This attribute does not need to be in the same token.

These required attributes need to be on, and have their parent type on, in the token, to be marked present

## Affinity and allergies
affinities and allergies also control when a token is allowed to be or not be in a set, and controls token movement through a network of sets. See sets

Each affinity and allergy can have one or more force_rules

    force_rule:
        attribute_id:
        weight: number:  (negative means more repulsed, positive means more attracted)
        numeric_min:
        numeric_max:
        string_value: (constant or regex)

### Required set attributes for read

When this is set, actions do not run if that attribute cannot be read by anyone. This allows scripts to run not only when the token is at a certain location and time,
But when the token is combined with certain other tokens in a set


### Boundaries

there are three sorts of boundaries

activity bounds is the token must be in these bounds to do a lifecycle change. If the bounds is a set path bounds, then this only applies to some lifecycles such as set operations.
The map location, and time existence, of the token must also be in the union of bounds for the activity bounds

read bounds is that the attribute is readable inside these bounds only. The token can only be read if the union of the attribute bounds allows it

write bounds is that the attribute is writable inside these bounds only. Same as said for reading

Each category of boundary use can only use of of each boundary type (location, time, path)



## Naming rules

Attributes must have a name, but the name must start with the username that created it, followed by a dot. then something for 'attribute', another dot, then the name must be unique
