# Agents

Agents are users that do element changes for other users.
Any user can be an agent for any other user. An agent can do changes for many users at once.

Agents can be used for reporting changes outside the server. For instance an email server or hook can have an agent, that 
records new emails as new board api. 

Agents can have a different rate setting for each user they represent.

Agents have categories to use in the api below. Agents can be authorized to only use a subset, or one or more, api calls for the user.

Agents can be assigned to do only one api call for a user, or do N api calls or do N api calls within a time range. 

Agents can be assigned to do something for anyone in a user group.

Agents can be limited to only do api calls for specific elements, this allowed element list can be updated as needed.
The whitelist of elements is maintained by this layer.

Agents can be moderators (human or bot) that can change and remove some things in chats, boards, stores, items, inventory.

A user can be his own agent, to allow for advanced api call handling.


## Logs:
* Agents keep logs for N seconds about the changes it found, and the changes it made
* Agents can be made just for logging services

# Api

* create agent (requires oauth agreement)
* create agent (no agreement, private api)
* list agents the logged-in user made, or categories of agents made by group members
* turn on and off agents
* manage element whitelist
* end agent
* show log of agent

## Agents for registration and login

Called user-agents

An agent can create new users , then handle the login and logout and cancelling of accounts. 
This elevated priv of creating new users is admin approved in this api per application.

Once the user is created, the normal agent oauth applies, so the user can revoke this later, if they wish, or add other registration agents.

The user agent will keep a non expiring token
