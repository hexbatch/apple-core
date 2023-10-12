We have some objects (tokens) that are made out of attributes.
A token has an owner and starts with some standard attributes. 
A token is always in at least one token-set.
A token can be in many token sets.
A token set can contain tokens not owned by the owner of the token set.

Attributes are defined by themselves, and attached to the token-type. The tokens are instances of the token-type

# Token types

Tokens can have one or more parents, they can have many ancestors.
 Ancestors (which includes parent) cannot by cyclic by having their ancestors be something they are an ancestor of.

    So: a token-type:
        user: one user owns the type
        attributes: []
        parents: []

# Type groups

A token-type can be added into a type-group:
    Tokens can belong to one or more type-groups.
    A type-group can be used in token-set operations, where tokens are added or removed between sets
    Type-groups can have attributes, to give it a name and appearance, or notes, and to provide logic for set operations
    type groups can be owned if attaching appearance and docs. But ownership is not used when type-groups are used in set operations

    So: a type-group:
        user: maybe one user owns the type
        attributes: []
        token-types: []


# Token set

All tokens belong to one or more token sets.
A token set does not have any definition or structure, it's a loose organization of tokens.
A token set must be owned by only one user. Ownership is not transferred, but the tokens in one set can be added to the tokens in another set

    So a token-set:
        user: must be one user
        tokens: []


------------------------------------

# Boundaries can be on the map or in time.

Boundaries are only applied to attributes.

map bounds is a set of closed polygons denoting map coordinates , that is applied to an attribute. 
A token's total map bounds is the union of all the map bounds in the attributes of a token-type or a type-group except do not use any script type attribute bounds in this
An attribute can have zero , one or many map bounds

    so a map-bound:
        user: must be one user.
        name: name of the bounds (unique to maps)
        polygon array: at least one polygon, they can overlap or not be connected or join


Time bounds is defined by both a range to start and stop using this bounds, and an option period that includes a duration.
How the bounds are used on attributes, and how they propogate is same as described in the map bound

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
A user has an id, a guid, and a list of attributes. A user can include non system attributes they have permission for

    So a user:
        id: number
        guid: string
        attributes: []

----------------------------------------
# User Groups

A user group is a collection of users who have permissions.
A user group is not discoverable to non-members, but a user can see which groups they belong in
A user group can have attributes for image, docs, but scripts do not run here.
Because user groups do not have an owner, only system attributes or attributes that do not need permission checks can be used here

    So a user-group:
        users: [] who is in the group
        admins: [] who can directly modify the list using the api
        attributes: []

----------------------------------------

# Attributes

Are the core of the api here. 
Attributes can be defined by the code, in which case they are not owned, and cannot be edited or deleted.
Attributes can be created|edited|deleted by a user.
Attributes can be restricted to only be used in a token or type-group if there are one or more other specified siblings. 
    These siblings can have an ancestor or parent that matches this.
Attributes can have an optional whitelist to allow which users can own, change the value of, and read this value of this attribute.
    A descendant can change the groups, but only by limiting the groups further

Attribute values can be a number, string, json, markdown, binary (image , pdf only), a script to run
string specific types can be :
iso date time, color, url, email, social account , phone, any
number is any numeric value

An attribute is defined, when applied its value is put next to the action's instantiated values (a token or type group has a list of their attributes and current values)
Starting out, the default value is used, if no default then null

    so an attribute:
        user: can be one or none
        name: name of the attribute (unique to attributes that are owned by this user (or owned by none))
        bounds:
            map: []
            time: []
        required_siblings: []
        owner_user_groups: [] if empty then anyone can use this to create their tokens and token-sets
        read_user_groups: []  if empty anyone can read the attribute value
        write_user_groups: [] if empty anyone can change the attribute value.
        value:
            value_type: one of: numeric, string, string specific type,json, markdown, binary, action
            min: (numeric only)
            max: (numeric only)
            enum: (string only if no regex)
            regex: (string only if regex set then enum ignored)
            default:
            allow_null: default true, but can only be false if the default is set


-------------------------------

# Actions

Actions can be registered that run javascript functions.
Scripts that are run, are not able to access the api, so the passed in values is the object copy of the thing only, and can be altered by the script without api changing.
Scripts can change the local and global settings for themselves.

Actions can run on boundary set on the attribute, cron times make it run, entering or exiting areas: see location_entering, location_leaving.

Actions can be used to change own parent or other thing's values (so token or the token sets the token is in) (permission apply).

Actions can be used to set rules for creation of a token 
    To disallow creation, each token starts with a created attribute whose value must be truthful, if this value is false, then the token is not saved and creation fails.
    Creation rate limiting is handled by the creation actions script_state

Rate limiting is scripts running on token set changes, or lifecycle changes

Multiple actions can listen to the same lifecycle changes or other conditions.
    So, to rate limit token creation and charge someone have two actions. One to limit and one to charge
(need to figure out how to set up value transfers from one user/token attribute to another)

Lifecycle for attributes:
creation
owner-change
token-set addition
token-set removal


    so an action:
        action-name: can be any unique name
        action-version: can be a version (optional)
        action-owner: actions may be owned by a user, but optional
        target attribute guid:
        target-from-state: literal string, number or regex (empty means always) can be used with the lifecycles
        lifecycle: [] array of life cycles this script runs on, without looking at the target from-state, can be empty
        recipient attribute: the script can only change the recipient attribute
        recipient token: if not empty, this token must be writable by the user of the action, the token does not have to be the target, and no other tokens will be written to
        per-token: if true, this script runs per token that has the attribute meet requirements, and only its attribute can be changed
                   if false then script runs per set, and all the set population tokens and their target attributes are looked at,  and any recipient token in the set can be changed.
        run-when-out-area: default false, else runs when token or type-group is outside of location bounds
        run-when-in-area: default true runs when the token or type-group is inside the location bounds
        md5 of script: makes sure the script is not changed when this is applied to any instantiated actions
        param_attributes: [] if not empty then these attributes must exist on the token or type-group for the action to run
        local_script_state: stored json and passed to script as an object, updated in the script. This is per instantiation
        local_script_state_init: the initial local_script_state
        global_script_state: shared by all instantiated actions, its initial state set in the definition of this action here
        script: input(target_tokens[], param-attribute-values,token-set, local script_state, global script state) : {array changed recipient attributes  {guid,value}, new script_state local and global}


----------------------------------------------------

# set operations


set operations:

        combine: A source B source  C pattern D destination
        divide: sets A source B pattern C destinations
        create set: => empty set
        delete set: A removes a set
        list_user => C pattern(optional) , returns set
        populate_set => T type, D destination
        edit attribute => attribute name, attribute value , A source

-------------------------------------------------------------

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
    user-guid

-------------------------------------------------------------

# Standard token types


name:
description:
image:
symbol:
primary_color:
background_color:



