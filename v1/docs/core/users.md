# User

User is both a person (or bot) in this library, and a token type. Any tokens a user creates will inherit from this token type.

A user when created has some default attributes, some of which can only be read by the user.

When a user is created, a user group for it is also created. Any other user added to the group can read the private data.
Any other user promoted to admin in the user group can write to the user attributes

The only top level information a user contains is its id, its guid (automatically made or changed to a unique string in the system),
its token type, and the token of the user itself. 

The user data is found by getting the attributes of the user token.

The token type starts with a list of standard attributes. By default all of the "Core ID and display" attributes are there.

A user can include non system attributes they have permission for, and this is added directly to the token type, and the token automatically picks up on this new attribute.

The token type can only create that one user token, but token types inheriting from that user token can create amounts of tokens defined in the new token type. 

for the user token, actions cannot run, and bounds cannot be set

    So a user:
        id: number
        guid: string
        token-type: made new for the user, inherits from the system user token type (see system tokens and attributes)
        token: the actual token represting the user

When a user is created, a [user group](user_groups.md)  is created as well, whose token inherits both from the default group token, and the user token made here.
The creator of the user is also the creator of the user group

Anyone added to the user group will be able to read the user's private data. An admin on the user's group will be able to also write all private and public data.

The user logged in to create this user is automatically put into the new user's admin group.

If there is nobody logged in, then the creating user is the root user.

The library has one root user made by default.

The core library has no concept of administrators or moderators, but these users can be added by the layers to be an admin in the user's group

When a user requests to be removed, then someone in the user's admin group can write to the attributes to remove information



