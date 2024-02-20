# Server Api

Servers

| Method | Path                                   | Route name | TO Do | Description                                       |
|--------|----------------------------------------|------------|:------|---------------------------------------------------|
| Post   | server/create                          |            | *     | Adds a new server that is known about             |
| Get    | server/:id/get                         |            | *     | gets details about the server                     |
| Get    | server/:id/list                        |            | *     | gets details all the servers, cursor              |
| Delete | server/:id/destroy                     |            | *     | removes details about the server                  |
| Patch  | server/:id/edit                        |            | *     | edits details about the server                    |
| Post   | server/:id/action/:id/call             |            | *     | calls the action from the remote                  |
| Get    | server/:id/attributes/read             |            | *     | reads attributes from the remote                  |
| Post   | server/:id/attributes/write            |            | *     | writes attributes from the remote                 |
| Post   | server/:id/elements/add                |            | *     | adds new elements from the remote                 |
| Get    | server/:id/elements/request            |            | *     | a remote requests one or more elements by uuid    |
| DELETE | server/:id/elements/:element_id/remove |            | *     | adds new elements from the remote                 |
| Post   | server/:id/types/add                   |            | *     | adds new types from the remote                    |
| Get    | server/:id/types/request               |            | *     | a remote requests one or more types by uuid       |
| DELETE | server/:id/types/:type_id/remove       |            | *     | adds new types from the remote                    |
| Post   | server/:id/sets/add                    |            | *     | adds new types from the remote                    |
| Post   | server/:id/user/register               |            | *     | links a user on that server with here             |
| Post   | server/:id/user/permission             |            | *     | gives server permission for that registered token |
| Post   | server/:id/user/revoke                 |            | *     | revokes a server to use that registered token     |
| Post   | server/:id/user/register               |            | *     | tells a server they want to come in               |


#Api 

## create server
Anybody can call this and claim their url for a new entry. The user has to be logged in, and the logged-in user is associated with that server.
If other user already has that url, this fails.
The server has to set its dns text record with its guid, that guid has to be passed in here, and the record checked to have the user prove ownership.
If all is ok, then a token is generated and given back.
A user can only do one server, this is because that user is the server here.

servers have a default rate api and time set to not allow any calls.
The target server, will also call the originating server to register itself, and can pass in any schedule here

## get server
The logged-in user, or his admin group, can get details about the server associated with them, including that token generated above.
This token is what is sent to the action call

## delete server
The logged-in user only can remove the server associated with him, this also removes any protected tokens.
Or a user on this server with admin role can do that.

## edit server
Someone with a server admin role can edit this server to have rate api and a schedule set to anything

## call action
the logged in server/user can call this, with its token and the element guid and the remote user guid .
If the action,element, and element type match up for existing and levels, the action is run.
If contructor actions are run, then they will return new element information

## read attributes
The logged in server user will call this, with the user token and an array of element,attribute combinations.
if user token is not set, then uses the server's user for context

## write attributes
The logged in server user will call this, with the user token and an array of element,attribute, new value combinations
if user token is not set, then uses the server's user for context

## adding elements
Any server can call and introduce elements from itself.
These are put into sets or changed after they are added.
The type has to be already registered.
The attributes on the elements have to match all the visible attributes to the server (see server level for a type)


## Removing elements
a server can call to remove one or more elements, listed by uuid, in an array
the element is deleted from the records (so removed from all sets)

## adding types
A server can call and set new types from it to here.

## removing types
A server can call and remove a type, this also removes all elements of that type

## requesting types and elements
when someone wants to move a set from one server to another, the elements may be from different servers.
The users owning/moving the set must be known to the target server first.
The recieving server will see which servers are not on its list, and do the create server handshake,
then once that is done, will request the element and types needed.
Once all this succeeds, the new set is created

## Adding sets
a server can call and add in a set, but cannot remove the set once created

## The server registers a user
the logged in server or its admin group can register the user guid from here as also being used there. 
This make a token just for that user and server. If one already is made , that is the one returned.
This token will not represent the user here, in calls for actions to be done, until that user gives permission.

## user give permission
The user who is registered gives permission to use that token in called actions from that server.
The user is associated with that token.
Optional time to live

When the action is called by the server user or its admin group, that token is passed in to show this call is being made on behalf of that user.


## user revoke permission
can be called by the server or token's user, or their  admin groups,
will delete this token so further use on that server will not be associated with the token's  user


## The user registers on a server 
The user can give his uuid, and the server url he is from. Then that server this call is made on will contact the other server to register it.
The user then has to give permission.

