# Attributes

Are the core of the api here. Attributes have value. By default, attributes can be read by everyone and written by no one else but the owner admin group

Attributes can be defined by the code, in which case they are not owned, and cannot be edited or deleted.

Attributes can be created|edited|deleted by a user.

Attributes can have a parent. All attributes on a server have the server attribute parent.

Attributes can have an optional whitelist to allow which users can use , change the value of, and read this value of this attribute.
A descendant can change the groups, but only by limiting the groups further

Attribute values can be many things, including a number, string, json, markdown, binary, a remote to run, location,
an action, map coordinates or more

When an attribute holds a remote, when a write happens the remote is run, and when a read happens the remote is run too.
Remotes can have caches and other things to prevent that from being overloaded.


An attribute is defined with a starting value.
When it is applied to a type, and the type makes an element, then this value can be changed and the change is only for that element or type.
This value can be changed by any who can write to the element

Starting out, the default value is used, if no default then null

A new attribute can be made that has all the features of its parent, however any new things added to this will override the parent's

Attribute have an owner, a name, bounds, requirements, permissions, and a value

Attributes can have optional explaining text

options:
  * Final means cannot be used as a parent
  * Human status, to selectively hide this attribute from searches if the human filter is on.


      so an attribute:
          parent_attribute: attributes can optionally have a single parent
          user: can be one or none
          name: name of the attribute (unique to all attributes)
          description: some text explaining why this attribute is used, etc, the author or other info
          is_retired: default false // if true then cannot be added to element types
          is_system: if so marked, then anyone can use this in their own types  
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
              remote_use_policy enum of read_and_write_local,read_only_remote_write_local,write_only_remote_read_local,read_and_write_remote, default is first  
          options:
              final:
              human:  
          servers:
            read_server_level: default is private
            write_server_level: default is private

## Value types

Data can be marked as:

* numeric
* string
* json
  

* points to something 
  * user_id
  * user group
  * attribute
  * element
  * element_type 
  * remote
  * action
  * search
  * schedule_bounds
  * map_bounds
  * shape_bounds
  * set
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

Ownership groups can use this to add to their own element types and elements.
Note that once someone else has permission to create with this attribute, and they make something with it, then that can never be taken back.
But the attribute could be retired to prevent any new use

Attributes can have parents, this means the children can change permissions and bounds. The usage permission can also be changed on a child


### set requirements

An attribute can behave differently based on the set it belongs to.

An attribute can make it impossible to join a set. An attribute can define the sets it will join based on the set content.
To deny entry to any set, then base the allergy on a common attribute ancestory, such as all attributes, or the server attributes.
And then make the affinities outweigh those.

Conditional permissions can also be defined to allow the read and write to only occur when another(or several) attribute in the same element set is present.
This attribute does not need to be in the same element.

Elements do not have to be visible to the element owner or user in the api to count to the requirements.

## Affinity and allergies

affinities and allergies also control when an element is allowed to be or not be in a set

Each affinity and allergy can have one or more force_rules

    force_rule:
        attribute_id:
        weight: number:  (negative means more repulsed, positive means more attracted)
        numeric_min:
        numeric_max:
        string_value: (constant or regex)

attributes normally hidden to a user do apply to force rules.

### Required set attributes for read

When this is set, actions do not run if that attribute cannot be read by anyone. This allows remotes to run not only when the element is at a certain location and time,
But when the element is combined with certain other elements in a set


### Boundaries

there are three sorts of boundaries


read bounds is that the attribute is readable inside these bounds only. The element can only be read if the union of the attribute bounds allows it

write bounds is that the attribute is writable inside these bounds only. Same as said for reading

Each category of boundary use can only use one of each boundary type (location, time, path)



## Naming rules

Attributes must have a name, but the name must start with the username that created it, followed by a dot. then something for 'attribute', another dot,  the name after that must be unique
