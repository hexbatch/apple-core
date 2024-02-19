# Servers

There can be multiple copies of this libary running at the same time, and they can talk to each other
Elements and types can be exchanged between the servers, and events are sent to the original server.
But which events are sent depends on the server data sharing level.

Much like object-oriented data is, there are three levels of servers for an action.
* Private means just on this server.
* Protected means both servers agree to be on each other's protected lists
* Public means all other servers.


## Actions know the maximum server level they can operate at.

If an action is marked as private, then when this type is copied over to another server, then this action will not run.
Some event listeners are marked as automatically failed if they are on a server above the level set for this action:
* constructions
* destructions
* owner-change
* value change

Other events are assumed accepted or allowed if the action handler is above its level
* any set operation permission

## Calling an action remotely

When an action is at its level in another server, that action is called via that server's api. 
And the results of that action is sent back, and after that its processed normally in that other server.

# Validating protected forwarding
The servers on the public and protected lists is kept by the type:

Each type has a protected list of servers, when a server is added to that list, an api call is made to that server to get a protection id,
the protection id is stored on both servers, when the server forwards the protected action, it also sends the protection id

This protected server list can be shared between types. A server can be dropped from the list, or added, during the lifetime of the action(s) using it

# Validating public forwarding
Each server has its own id (the server type id), that is sent with every forwarding, this will keep track of calls from uknown servers.

A type can turn off any actions for public servers. A type can be expected to be shared outside the protected list even if all actions are off for public


# Sharing the action 
When a type is shared, its actions that can be run on that server are sent over, when a server is added or dropped from a protection, then that server gets new action list

# Values for attributes 
Values for elements not on their own server are always set and read from the originating server, these reads can be cached with a time to live for each element
The writes are always sent

Attributes also have a read and write server level

# attributes using user permissions on other servers
Users can register with other servers by passing in their id for this server
That server will call this and leave a token for that user, when that server is making api calls from the other server, all calls include this token.
The token is not valid until the user runs an api call, logged in verifying this token as theirs.
Once this token is verified, then the remote server call user will be mapped to this user, and all permissions work in the attributes.

# rate limits and allowed times
each server can optionally be given an api rate limit per unit of time, and a schedule
