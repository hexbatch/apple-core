# Users in the core

All the api requires a logged-in user (except for the user creation call and getting standard attributes).
Users own most of the resources here. There is a strict permissions used. And it is easy to lock down what they create to only allow certain users or groups to interact with them.

There are permission groups, and a permission group for a user can have admins to write to that user's resource, or be a member to read the user's resource.
Each user has only one permission group that automatically apply to what they make. However, each user can make unlimited other permission groups, to apply to attributes and elements and sets. 

But there are no super-users, moderators or classic admins here in the core. No account is made special.
Someone has to get a user bearer element to see or change what that user has access to read and write.

There is not much required information to make a new user: a username. Any other information is added by attributes to the user element.
There are some standard attributes for descriptions.

Each user is also an element type, and an element, and an attribute. So a user can logically be put into sets of elements.
