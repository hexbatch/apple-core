# Apple Core

The core api is not meant to be exposed directly to the public, but still needs basic auth to use when the services call on it

The core is meant to be stand alone for testing and demonstration purposes though

# Parts of the core api

* We have some objects (tokens) that are made out of attributes.
* A token has an owner and starts with some standard attributes. 
* A token is always in at least one token-set.
* A token can be in many token sets.
* A token set can contain tokens not owned by the owner of the token set.
* Token sets are altered, created and destroyed via set commands using type-groups
* Actions listening in on different lifecycle stages of a token, and when a token joins a set, can run javascript to decide to allow this and do auto transfers of tokens

Attributes are defined by themselves, and attached to the token-type. The tokens are instances of the token-type

# Token types

Tokens can have one or more parents, they can have many ancestors.
 Ancestors (which includes parent) cannot by cyclic by having their ancestors be something they are an ancestor of.

    So: a token-type:
        user: one user owns the type
        attributes: []
        parents: []




# Token set

All tokens belong to one or more token sets.

A token set does not have any definition or structure, it's a loose organization of tokens.

A token set must be owned by only one user. Ownership is not transferred, but the tokens in one set can be added to the tokens in another set

    So a token-set:
        user: must be one user
        tokens: []
        token-type: (optional) if some description is needed for this token set


## Type groups

Type groups are used in token set operations

A token-type can be added into a type-group:

Tokens can belong to one or more type-groups.

A type-group can be used in token-set operations, where tokens are added or removed between sets

Type-groups can have attributes, to give it a name and appearance, or notes, and to provide logic for set operations
* The array of attributes can have those inherited from the attribute_filter which can look at the set to filter and decide which will be allowed

Type groups can be owned if attaching appearance and docs. But ownership is not used when type-groups are used in set operations

The token types can have a max and min amounts. In set operations the exact amount used will default to be either the min,then max if min not set, or all available if neither

    So: a type-group:
        user: maybe one user owns the type
        attributes: []
        token-types: [ {
            type: token-type
            minimum_needed: optional
            maximum_needed: optional
        }]

## Set operations 

When putting a token into a token set, using an operation, the allows_set is evaluated if the owners are not the same, or if present.

When using a set in an operation, the token set can have an attribute allows_set_operation which has to be truthful to proceed
The value of this can be a script and set by bounds, the script can do a filter for the type of set operation or what is being used in the operation

set operations:

* T is the type-group and is always optional, if missing it means all are operated on
* A is the source set
* B is a second source set
* D is the destination set


        combine/add: A source, B source,  T pattern, D destination
        remove: A source, T pattern,, D destination / removes tokens from a set puts it in another set
        create set: => new empty set
        delete set: removes a set, fails if any token here is not already in another set
        edit_attribute => attribute name, attribute value , A source, T pattern
        change_owner => new owner id, A source, T pattern




## Permissions for a token to be added to a set

By default, a token can always be added to a set if the set is owned by the same person who is owning the token.

By default, a token cannot be added to a set if they are owned by different users.

However, other people can add a token to their sets if the attribute allows_set has a truthful value

if the allows_set is falsy value, even the token owner cannot add to the token set

allows_set, being an attribute, can use a javascript to do complex logic to decide this

## Read and write permissions can be defined by set membership

attributes have the option to be readable or/and writable based on other attributes being present in the same set (not necessarily in the same token)

Between the ability to control when a token is added to a set, and when something is readable. This makes for a powerful set of access choices.

Additionally, user permission is by group, and group membership can be restricted to a boundary (only active in time or location)

------------------------------------

# Boundaries can be on the map or in time.

Boundaries are only applied to attributes.

map bounds is a set of closed polygons denoting map coordinates , that is applied to an attribute. 

A token's total map bounds is the union of all the map bounds in the attributes of a token-type  except do not use any script type attribute bounds in this

An attribute can have zero , one or many map bounds

    so a map-bound:
        user: must be one user.
        name: name of the bounds (unique to maps)
        polygon array: at least one polygon, they can overlap or not be connected or join


Time bounds is defined by both a range to start and stop using this bounds, and an option period that includes a duration.

How the bounds are used on attributes, and how they propagate is same as described in the map bound

    so a time-bound:
        user: must be one user.
        name: name of the bounds (unique to times)
        start: when to apply this bounds, inclusive
        stop: when to stop this bounds, inclusive
        cron: optional crontab string
        period_length: only used and required when the cron is defined, is how long this time is allowed per cron run

Boundary operations:
    in the api, both type bounds can be created|edited|listed|deleted. When listed will show the attributes this is used on


----------------------------------------
# User 

A user is described in the api this way.

A user has an id, a guid, and their own token type.

The token type has the list of attributes. A user can include non system attributes they have permission for

    So a user:
        id: number
        guid: string
        token-type: made new for the user, inherits from the system user token type (see system tokens and attributes)

When a user is created, a user group is created as well, whose token inherits both from the default group token, and the user token made here.

Anyone added to the user group will be able to read the user's private data. An admin on the user's group will be able to also write all private and public data

----------------------------------------
# User Groups

A user group is a collection of users who have permissions.

A user group is not discoverable to non-members, but a user can see which groups they belong in

A user group can have attributes for image, docs, but scripts do not run here.

Each user group inherits from a base user group token type. For example, if a company creates a group.

The group owner is the owner of the token-type, who is the creator of the group.

When adding attributes to the token-type, the attributes have to be readable and writable by the owner and whoever is editing

    So a user-group:
        users: [] who is in the group
        admins: [] who can directly modify the list using the api
        token-type: made new for the group, inherits from the system group token type (see system tokens and attributes)

## Inherited groups to restrict or put conditional membership

Groups that inherit from other group token-types also inherit their memberships and admins
These tokens can be restricted by space and time, and have extra or fewer members and admins

Inherited groups are good for allowing a subset or geo or time fencing permissions for attribute or sets

----------------------------------------

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

    so an attribute:
        user: can be one or none
        name: name of the attribute (unique to attributes that are owned by this user (or owned by none))
        bounds:
            map: []
            time: []
        required_siblings: []
        permissions:
            owner_user_groups: [] if empty then anyone can use this to create their tokens and token-sets
            read_user_groups: []  if empty anyone can read the attribute value
            write_user_groups: [] if empty anyone can change the attribute value.
            set_requirements: 
                read: [] attribute ids
                write: [] attribute ids
        value:
            value_type: one of: numeric, string, string specific type,json, markdown, binary, action
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

  

-------------------------------

# Actions

Actions can be registered that run javascript functions.

Scripts that are run, are not able to access the api, so the passed in values is the object copy of the thing only, and can be altered by the script without api changing.

Scripts can change the local and global settings for themselves.

Actions can run on boundary set on the attribute, cron times make it run, entering or exiting areas: see location_entering, location_leaving.

Actions can be used to change own parent or other thing's values (so token or the token sets the token is in) (permission apply).

Actions can be used to set rules for creation of a token 
* To disallow creation, each token starts with a created attribute whose value must be truthful, if this value is false, then the token is not saved and creation fails.
* Creation rate limiting is handled by the creation actions script_state

Rate limiting is scripts running on token set changes, or lifecycle changes

Multiple actions can listen to the same lifecycle changes or other conditions.
* So, to rate limit token creation and charge someone have two actions. One to limit and one to charge
* But, this can also be the same action

An inheritance chain will run the actions from the ancestors to the current
  * if any action fails, then there will be a db rollback, and nothing is saved

When setting a charge, if there are not enough tokens in the source token set, the action will fail
 * The charge will only happen if the script returns a truthful value to the target attribute

Lifecycle for attributes:
* creation
* owner-change
* token-set addition
* token-set removal
* token-set mass attribute altering


    so an action:
        action-name: can be any unique name
        action-version: can be a version (optional)
        action-owner: actions may be owned by a user, but optional
        target attribute guid:
        target-from-state: literal string, number or regex (empty means always) can be used with the lifecycles
        lifecycle: [] array of life cycles this script runs on, without looking at the target from-state, can be empty
        recipient: //optional
            recipient attribute: the script can only change the recipient attribute
            recipient token: if not empty, this token must be writable by the user of the action, the token does not have to be the target, and no other tokens will be written to
        charge : //optional sets up a token-set operation
            charge_type: the type-group to charge with
            charge_source_set: the token-set to remove tokens from
            charge_destination_set: the token-set to put the tokens
        per-token: if true, this script runs per token that has the attribute meet requirements, and only its attribute can be changed
                   if false then script runs per set, and all the set population tokens and their target attributes are looked at,  and any recipient token in the set can be changed.
        run-when-out-area: default false, else runs when token or type-group is outside of location bounds
        run-when-in-area: default true runs when the token or type-group is inside the location bounds
        script:
            md5 of script: makes sure the script is not changed when this is applied to any instantiated actions
            param_attributes: [] if not empty then these attributes must exist on the token or type-group for the action to run
            local_script_state: stored json and passed to script as an object, updated in the script. This is per instantiation
            local_script_state_init: the initial local_script_state
            global_script_state: shared by all instantiated actions, its initial state set in the definition of this action here
            script: input(target_tokens[], param-attribute-values,token-set, local script_state, global script state, set operation info) 
                    returns
                    : {array changed recipient attributes  {guid,value}, new script_state local and global}


----------------------------------------------------


# Data types

each data type has its own set of api operations

data types:

    action
    map bounds
    time bounds
    attributes
    token-type
    type-group
    token
    token-set
    user-group
    user

-------------------------------------------------------------

# System defined items

## Standard token types

### User Tokens

The user token has all the core identification and display attributes. When a user is created, a new token type is inherited

The base user token also is in some system defined groups

### Group Tokens

The group token has all the core identification and display attributes. When a group is created, a new token type is inherited

## Standard groups

* regular_user : this user is a vanilla ordinary user without special privileges 
* full_admin_user : this user can read, write any attribute, and can create tokens inheriting from any attribute, and assign ownership to anyone of any resource, and do user group changes
    

## Standard attributes 

 * Core ID and display
 * Management flags
 * Organization

### Core identification and display

* name: string
* email: string
* phone: string
* address: string
* location: map_coordinates
* description: markdown
* image: binary
* symbol: binary (small image svg)
* primary_color: color
* background_color: color
* svg_symbol_image  : binary (small image svg)
* favicon : binary (regular image types) 32px square
* small_thumbnail: binary (regular image types) 128px square
* medium_thumbnail: binary (regular image types) 256px square

### Management flags

* allows_set: evaluated for truthful determines if a token can be added to a token set
* allows_set_operation : evaluated for truthful to see if the set operation can take place
* attribute_filter : if present, only the attribute named here in the target-attribute will be allowed, if the value is truthful

### Organization

Read only tags, to sort tokens. By default, tags can be read by everyone and written to by no one

Base tag attribute, which has direct children being tag categories, then more specific tags inherit from the categories.

Tags should be about what the token contains, or what the token is about

* user - the token is about a user
* media - the token has media such as image, pdf, or video urls
* documentation - the token has markdown files to explain stuff



