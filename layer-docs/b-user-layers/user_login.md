# Logging In

* This api handles logging in the user via api call done by the user-agent
* The user agent decides on how the user logs in, and hands the user token to the user api

## Authentication
The user-agent is registered as an agent, as long as the user does not cancel it, this user-agent can store that login token and hand it to the user api here.

### User api calls that are for logging in, redoing tokens, and removing users

* check if username is valid and available
* create new user with username and info provided, privides long term token
* update user info provided
* remove user
* logs the user in, returning the user home shell, and uses a token for this user that expires later, (there is no log out)
* gets a list of user-agents and their url and contact info
* shows information about the user who uses this token kept by the user-agent
* makes a new long term token, destorying the older one

