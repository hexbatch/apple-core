# Users in the core

Users own most of the resources here, and can lock down what they create to only allow certain users or groups to interact with them.
But there is no super-users, moderators or admins here in the core. Someone has to get a user bearer token to see or change that user's resources if permissions are set for those.

There is not much required information to make a new user: a username. Any other information is added by attributes to the user token.
There are some standard attributes.

Each user is also a token type, and a token. So a user can logically be put into sets of tokens.

Most api calls require the user's bearer token to authenticate