# External user 

WIP
---------------
---------------


When a user token from another instance enters this instance for the first time, they do not have to register or manually create a new account.

Instead, the user provides their home instance, and a new user is automatically created that wraps around the outside user token.

It uses the mirroring layer to update the user token. 

However, no other tokens are imported other than the users. They can refer to their tokens in the current instance
but the info and interactions of those tokens are sourced in the original server. 