# Registrations

Does all the new user account creation

* allows people to create accounts using different social media
* allows to join other social network logins to this
* once a person joins using a type of login, all the tokens associated to that social account is given to them

Account linking:
* Handle connecting the user with an existing network entry token, which is then placed in their identity-networks.
* The user enters the account info first, the network entry is made, or found.
* Then the user proves control of that thing via plugin

Handles password reset if user lost it

## Signup Plugins

Each social network, or type of sign up such as email,
has its own plugin that gets the data, perhaps requires extra api calls by the client to fill in stuff.

Plan to do the default email first

## Linking Plugins

Each social network, or type of sign up, has a way to verify the ownership of the entry with the signed in user

Plan to do email verification first.


## Usage of agents

Agents api might be used for some, or all, verification and sign in, using a base user account 

(all users inherit from a base user token, which is system defined token but this can be a real user account too, so can grant access to the agent)