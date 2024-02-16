# User

User is both a person (or bot) in this library, and an element type. Any elements a user creates will inherit from this element type.
The type for the user is created when the user is made, The type has the same name as the user.
The user type inherits from a standard user type, but other types can be added here to mixin with that user type also.
The user's type can only create one element, that of the user, but can be used as a parent for other types.

A user, when created, has some default attributes, on his element, some of which can only be read by the user.


When a user is created, a user group for it is also created. This user group has the same name as the user.
Any other user added to the group can read the private data.
Any other user promoted to admin in the user group can write to the user attributes, and manage resources for the user.


The only top level information a user contains is its id, its guid (automatically made or changed to a unique string in the system),
its element type, and the element of the user itself.

The user data is found by getting the attributes of the user element.

The element type starts with a list of standard attributes. By default, all the "Core ID and display" attributes are there.

A user can include non system attributes they have permission for, and this is added directly to the element type, and the element automatically picks up on this new attribute.

The element type can only create that one user element, but element types inheriting from that user element can create amounts of elements defined in the new element type.

for the user element, actions cannot run, and bounds cannot be set

    So a user:
        id: number
        guid: string
        type: made new for the user, inherits from the system user element type (see system elements and attributes)
        element: the actual element represting the user



The core library has no concept of administrators or moderators, or root, but these users can be added by the layers when they log in as other users.

When a user requests to be removed, then the layers write overwrite any identifying attributes to remove information; and if no elements by the user is in circulation, will remove them.

## Members of the user's group

When a user is created, a [user group](group-overview.md)  is created as well, whose element inherits both from the default group element, and the user element made here.
The creator of the user is also the creator of the user group

Anyone added to the user group will be able to read the user's private data. An admin on the user's group will be able to also write all private and public data.



If the user is admin he can edit resources created by the user, and can see all the resource data.
If a user is just a member though, he can only view the user element's private data.

## Types of users

The system will create a new type called the User Base type, and it creates an element from that. Other elements can be generated, 
but the first element can never be deleted

The user base type, which always has the same guid across servers, inhertits from the system type, which always has its own guid 

### Usernames

Each user has a unique username, with no punctuation of most kinds, and not starting with a digit, and no whitespace

# User type patterns

User can be created which has as its base one or more already existing user types.
When a user is created like this, the admin group of the new user is a child of the parent users' admin groups,
this membership use the union of all the parent's group members to be the admin members of the shared user.
Admin priv is transferred likewise.

When one of the contributing users changes its admin group members or admins, then this is reflected in the union of groups

Alternately, the same multiple inheritance user can have its own independent user group, and the inheritance reflects organization rather than permissions.

Also, a user type can include non-user types as parents.

## Organizing users

* Users can be organized by attaching some special attribute(s) to categorize them
* Users can be organized using some type that has attributes



