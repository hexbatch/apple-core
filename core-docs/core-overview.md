# Apple Core

The core api is not meant to be exposed directly to the public, but still needs basic auth and bearer elements to use when the services call on it

The core is meant to be stand-alone for testing and demonstration purposes though

# Parts of the core api

* We have some objects (elements) that are made out of attributes.
* AN element has an owner and starts with some standard attributes. 
* AN element is always in at least one element-set.
* AN element can be in many element sets.
* AN element set can contain elements not owned by the owner of the element set.
* Element sets are altered, created and destroyed via set commands using requirements
* Actions listening in on different lifecycle stages of an element, and when an element joins a set, can run the remote to decide to allow this and do auto transfers of elements

Attributes are defined by themselves, and attached to the type. The elements are instances of the type


## General concepts


* [users](core-concepts/users.md)
* [groups](core-concepts/groups.md)
* [bounds](core-concepts/bounds.md)
* [attributes](core-concepts/attributes.md)
* [remotes](core-concepts/remotes.md)
* [actions](core-concepts/actions.md)
* [types](core-concepts/types.md)
* [element](core-concepts/element.md)
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

A [user](step-0-users-groups/user-overview.md) is both a person (or bot) in this library, and an element type.
Any elements a user creates will inherit from this element type.

A user when created has some default attributes, some of which can only be read by the user.

When a user is created, a user group for it is also created. Any other user added to the group can read the private data.
Any other user promoted to admin in the user group can write to the user attributes.

User elements cannot be bounded, and they cannot run actions

---------------------------------------
# User Admin
[user admin](step-0-users-groups/user-admin-tasks.md)
Life can get tricky! And the layers may need a way to reset a pw or all elements. Or when just using the core by itself, a pw might need resetting


----------------------------------------
# User Groups

A [user group](step-0-users-groups/group-overview.md)  is a collection of users. These groups are used for permission lists, and are the bedrock of the permission system in this library

Actions do not run on the element of the user group


-----------------------------------

# User authentication
[authentication.md](core-api-general/authentication.md)
users log in

------------------------------------

# Boundaries can be on the map or in time.

[bounds](step-1-bounds/bound-overview.md) are only applied to attributes.

Each bound has a location and/or time and/or set path component, either is optional

If there is no bounds, the attribute is always on. Else, the attribute is only read, written, and applied inside the bounds

----------------------------------------

# Attributes

* [attributes](step-2-attributes/attribute-overview.md) are the core of the api here. 
Attributes can be made to interact with one another, to require each other to be read or used, to set permissions and conditions for anything that happens in this api


* [standard-attributes.md](step-2-attributes/standard-attributes.md)
There is a list of attributes that have standard names

----------------------------------------------------

# Remotes
* [Remotes](step-3-remotes/remote-overview.md) are remote callbacks to be run and generate a value when an element attribute is read# Remotes



# Actions
* [actions](step-4-actions/action-overview.md)
are attribute values that listen to events and allow things to happen, they can use remotes

* [events](step-4-actions/events.md) are listed here

* [servers](step-4-actions/servers.md) allow outside calls to use resources

---------------------------------------------------------

# Element types

* [Element types](step-5-types/type-overview.md)
make elements, and can select them from a set.
They contain the static attributes that come to life when an element is made

* [System types](step-5-types/system-types.md)

# Elements
* [elements.md](step-6-elements/element-overview.md)
* [live attributes](step-6-elements/live-attribute-overview.md)


Elements are made from element types, and have live values of those attributes. 

Elements cannot add or remove attributes once they are created.

Elements have their aggregate values: bounds, affinities, allergies


# Element set
[sets](step-7-sets/set-overview.md)
All elements belong to one or more element sets.

AN element set does not have any definition or structure, it's a loose organization of elements.

* [Operations](step-7-sets/operations-overview.md)
* [Searches](step-7-sets/set-overview.md)
* [Relationships](step-7-sets/relationship-overview.md)




