# Apple Core

The core api is not meant to be exposed directly to the public, but still needs basic auth and bearer tokens to use when the services call on it

The core is meant to be stand-alone for testing and demonstration purposes though

# Parts of the core api

* We have some objects (tokens) that are made out of attributes.
* A token has an owner and starts with some standard attributes. 
* A token is always in at least one token-set.
* A token can be in many token sets.
* A token set can contain tokens not owned by the owner of the token set.
* Token sets are altered, created and destroyed via set commands using type-groups
* Actions listening in on different lifecycle stages of a token, and when a token joins a set, can run javascript to decide to allow this and do auto transfers of tokens

Attributes are defined by themselves, and attached to the token-type. The tokens are instances of the token-type

# User authentication

Some public and read only api calls do not need to have a logged-in user.
Otherwise, can use both basic auth to get a bearer token.

A user needs to have many different bearer tokens that are valid. Once the user gets his bearer token, he can use an api call to get another one.

A bearer token can be generated, to use with jobs, so the pw does not have to be sent with the job data. But the jobs should have just temporary tokens they delete when done.

So, need an api call to delete/unregister a bearer token given to it


# Token types

[Token types](token_types.md) make tokens, and can select them from a set. They contain the static attributes that come to life when a token is made


# Tokens
[tokens.md](tokens.md)
Tokens are made from token types, and have live values of those attributes. 

Tokens can have other attributes added to them individually, either that are not in the token type, or overwriting the token type's added on to them

Tokens have their aggregate values: bounds, affinities, allergies


# Token set
[sets.md](sets.md)
All tokens belong to one or more token sets.

A token set does not have any definition or structure, it's a loose organization of tokens.

------------------------------------

# Boundaries can be on the map or in time.

[bounds](step-1-bounds/bound-overview.md) are only applied to attributes.

Each bounds have a location and/or time and/or set path component, either is optional

If there is no bounds, the attribute is always on. Else, the attribute is only read, written, and applied inside the bounds


----------------------------------------
# User 

A [user](step-0-users-groups/user-overview.md) is both a person (or bot) in this library, and a token type.
Any tokens a user creates will inherit from this token type.

A user when created has some default attributes, some of which can only be read by the user.

When a user is created, a user group for it is also created. Any other user added to the group can read the private data. 
Any other user promoted to admin in the user group can write to the user attributes.

User tokens cannot be bounded, and they cannot run actions

---------------------------------------
# User Admin
[user admin](step-0-users-groups/admin-api.md)
Life can get tricky! And the layers may need a way to reset a pw or all tokens. Or when just using the core by itself, a pw might need resetting


---------------------------------------
# Aliases
[Alias](step-0-users-groups/alias-api.md)
Aliases allow setting different names using different languages

Api calls can have an optional language set in the call.
If there is no language, then no aliases will be used. However, if there is a language set, then the aliases will be looked for, if missing the non-alias will be needed.

Cannot mix aliases from different languages in same api call

----------------------------------------
# User Groups

A [user group](step-0-users-groups/group-overview.md)  is a collection of users. These groups are used for permission lists, and are the bedrock of the permission system in this library

Actions do not run on the token of the user group


----------------------------------------

# Attributes

[attributes](step-2-attributes/attribute-overview.md) are the core of the api here.

Attributes can be made to interact with one another, to require each other to be read or used, to set permissions and conditions for anything that happens in this api

-------------------------------

# Scripts
[scripts](step-3-scripts-urls/script-overview.md) are Javascript can be set to run and generate a value when a token attribute is read

# Urls
[urls](urls.md) are remote callbacks to be run and generate a value when a token attribute is read

# Actions

[actions](actions.md) are attribute values that are javascript that runs.

The actions also handle rate limiting, contracts, and whether a set action can happen


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

# Standard attributes
[standard-attributes.md](step-2-attributes/standard-attributes.md)
There is a list of attributes that have standard names