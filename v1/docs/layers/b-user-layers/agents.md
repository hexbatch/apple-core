# Agents

Agents are those that agree to do token changes outside the server, and report back the changes to make to the tokens.
This can be used with the export, import and verification between different servers, or do some other thing

Agents are used in a grant system by users

Agents have categories to use in the api below

* Agents can be authorized to do changes to user's tokens because of things not from this server.
* Agents can update tokens based on something that is happening off the server, they can also listen to token changes and 
    update something on their end.
* Agents can be sent push notifications about changes made to the tokens when they are made by the layer api here (watcher api)

Agents get an oauth grant to optionally:
* change tokens in a set(s). The oath role is keyed to the sets you make for them
  * editing the agreed on set will destroy that grant, as well as deleting the set
* change tokens of one or more types
  * Each type is a different grant
* Only change some attributes in the above


## Logs:
* Agents keep logs for N seconds about the changes it found, and the changes it made
* Agents can be made just for logging services

# Api

* create agent (requires auth agreement)
* create agent (no agreement, private api)
* list agents the logged-in user made, or categories of agents made by group members
* turn on and off agents
* end agent
* show log of agent

