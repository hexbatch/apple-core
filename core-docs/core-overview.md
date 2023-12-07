# Apple Core

The core api is not meant to be exposed directly to the public, but still needs basic auth and bearer tokens to use when the services call on it

The core is meant to be stand-alone for testing and demonstration purposes though

# Parts of the core api

* We have some objects (tokens) that are made out of attributes.
* A token has an owner and starts with some standard attributes. 
* A token is always in at least one token-set.
* A token can be in many token sets.
* A token set can contain tokens not owned by the owner of the token set.
* Token sets are altered, created and destroyed via set commands using requirements
* Actions listening in on different lifecycle stages of a token, and when a token joins a set, can run javascript to decide to allow this and do auto transfers of tokens

Attributes are defined by themselves, and attached to the token-type. The tokens are instances of the token-type


## General concepts


* [users](core-concepts/users.md)
* [groups](core-concepts/groups.md)
* [bounds](core-concepts/bounds.md)
* [attributes](core-concepts/attributes.md)
* [scripts](core-concepts/scripts.md)
* [remotes](core-concepts/remotes.md)
* [actions](core-concepts/actions.md)
* [types](core-concepts/types.md)
* [token](core-concepts/token.md)
* [sets](core-concepts/sets.md)
* [operations](core-concepts/operations.md)
* [searches](core-concepts/searches.md)



# api execution
[execution.md](core-api-general/execution.md)
Some things in api calls are done the same way

# expansions
[expansions.md](core-api-general/expansions.md)
Can extend the core later

# visualization while learning and testing
[visualization-testing.md](core-api-general/visualization-testing.md)
Be nice to the developers and testing!


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
[user admin](step-0-users-groups/user-admin-tasks.md)
Life can get tricky! And the layers may need a way to reset a pw or all tokens. Or when just using the core by itself, a pw might need resetting


----------------------------------------
# User Groups

A [user group](step-0-users-groups/group-overview.md)  is a collection of users. These groups are used for permission lists, and are the bedrock of the permission system in this library

Actions do not run on the token of the user group


-----------------------------------

# User authentication
[authentication.md](core-api-general/authentication.md)
users log in

------------------------------------

# Boundaries can be on the map or in time.

[bounds](step-1-bounds/bound-overview.md) are only applied to attributes.

Each bounds have a location and/or time and/or set path component, either is optional

If there is no bounds, the attribute is always on. Else, the attribute is only read, written, and applied inside the bounds

----------------------------------------

# Attributes

[attributes](step-2-attributes/attribute-overview.md) are the core of the api here.

Attributes can be made to interact with one another, to require each other to be read or used, to set permissions and conditions for anything that happens in this api


# Standard attributes
[standard-attributes.md](step-2-attributes/standard-attributes.md)
There is a list of attributes that have standard names

----------------------------------------------------

# Scripts
[scripts](step-3-scripts-remotes/script-overview.md) are Javascript can be set to run and generate a value when a token attribute is read

# Remotes
[Remotes](step-3-scripts-remotes/remote-overview.md) are remote callbacks to be run and generate a value when a token attribute is read# Remotes

# Metrics
[metrics](step-3-scripts-remotes/metrics-tasks.md) shows stats of calls to scripts and urls

# Actions
[actions](step-4-actions/action-overview.md)
are attribute values that listen to events and allow things to happen, they can use scripts and remotes

[events](step-4-actions/events.md) are listed here

---------------------------------------------------------

# Token types

[Token types](step-5-types/type-overview.md)
make tokens, and can select them from a set.
They contain the static attributes that come to life when a token is made


# Tokens
* [tokens.md](step-6-tokens/token-overview.md)
* [live attributes](step-6-tokens/live-attribute-overview.md)
* [parents](step-6-tokens/live-parent-overview.md)

Tokens are made from token types, and have live values of those attributes. 

Tokens can have other attributes added to them individually, either that are not in the token type, or overwriting the token type's added on to them

Tokens have their aggregate values: bounds, affinities, allergies


# Token set
[sets](step-7-sets/set-overview.md)
All tokens belong to one or more token sets.

A token set does not have any definition or structure, it's a loose organization of tokens.

* [Operations](step-7-sets/operations-overview.md)
* [Searches](step-7-sets/set-overview.md)
* [Relationships](step-7-sets/relationship-overview.md)




