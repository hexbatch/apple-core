# More registration layer but with networks

Add new plugins to work with the social networks

Add new registration layer api to work with network tokens

* allows to join other social network logins to this
* allows linking different types of logins to the same user
* once a person joins using a type of login, all the tokens associated to that social account is given to them
* Handle connecting the user with an existing network entry token, which is then placed in their identity-networks.
* The user enters the account info first, the network entry is made, or found.
* Then the user proves control of that thing via plugin
* allows password or other credential resets based on agents
* plugin based (expands the plugins used earlier)

## Linking Plugins

Each social network, or type of sign up, has a way to verify the ownership of the entry with the signed-in user

## Usage of agents

Agents api might be used for some, or all, verification 


