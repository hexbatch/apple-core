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
A server can call another and say this user is being referenced on my server.
The server gets a token to associate that user with in calls to run actions. When the action is run, the token is passed in,
and represents the user this action is for, even though the server user is making that call to run the action

But, the user this token is about has to first approve this. Until then, an action run with that token will result in an error 
(because everyone needs to be logged in)

Each server has its own token done like this for each user.

Users can register with other servers by passing in their uuid for this server

# rate limits and allowed times
each server can optionally be given an api rate limit per unit of time, and a schedule


# Existing user visits a server
The user tells the server his uuid, and the server url he is from.
This is different from new user signup, the user already exists, but not in there.

Then that server calls the user's home server to get a token to use in actions.
Then that server gets the user token to do the registration for that user. See username conflicts below.

The user does not have to give permissions after this, but then the action will not be called to run when he does stuff. Automatically failing events
The user can give or remove permission.

# Elements and types changing servers.
A server can add in types and elements from their stuff to other servers.
The added in types cannot be sent to yet another server, instead the origining server has to be told about it and it will do this.

If the type has a constructor event, seen by that server, then calling the constructor action remotely returns the new element information

The server can remove elements and types from that server at any time.

Before an element is added, there is an optional event listener that can be called before_server_add
this can deny the move to the server
each element transfer is connected to the remote activity

# Adding sets to servers
a server can add in an entire set to another server.
The elements in the set can be from that or other servers.
The non-local elements, which can include the set definition element, are sourced from their servers, and all have to succeed, before the set is added
So this is a remote tree when done here.


# Each server is a user here
Inherits from the server element type

# The User table username can have conflicts
Same username on different servers? The new username prefixes the server's name to his username

# Server Data we keep
    
    Server:
        user:
        time bounds: (optional)
        server_token: uuid 
        domain: (has to be reverse lookable)
        confirmed_at: null for unconfirmed
        calls_per_unit:
        seconds_in_unit:
        calls_made_current_unit:
        unit_ends_at: 
        server_paused_at: null or when, if not null, then server cannot call actions here
        server_allowed: bool, depending on whitelist options, may need admin editing to turn this server on
        
* The current server registers its own user here too
* The user with this server has its name and description attributes, or any other attributes, applied to any server data seen 

store user tokens for each user on a server (we do not need user tokens on their home server)
    
    user token:
        user_id:
        server_id:
        permitted_at: (null for not)

When an element type is imported, it has the server_id in the type

when a server gets remote elements, or calls a remote for attribute values, it stores them in the live table, and a time to live.    

when an operation to transfer stuff between servers is made, then we need a remote tree, for each server api call there is a remote made by the system.
when that api call is needed, then the regular remote system is used for any communication with the other server.
The affected users, types and elements are linked into the remote activity
