# Server Api

Servers

| Method | Path                       | Route name | TO Do | Description                                       |
|--------|----------------------------|------------|:------|---------------------------------------------------|
| Post   | server/create              |            | *     | Adds a new server that is known about             |
| Get    | server/:id/get             |            | *     | gets details about the server                     |
| Delete | server/:id/destroy         |            | *     | removes details about the server                  |
| Patch  | server/:id/edit            |            | *     | edits details about the server                    |
| Post   | server/:id/action/:id/call |            | *     | calls the action                                  |
| Post   | server/:id/user/register   |            | *     | links a user on that server with here             |
| Post   | server/:id/user/permission |            | *     | gives server permission for that registered token |
| Post   | server/:id/user/revoke     |            | *     | revokes a server to use that registered token     |

## create server
Anybody can call this and claim their url for a new entry. The user has to be logged in, and the logged-in user is associated with that server.
If other user already has that url, this fails.
The server has to set its dns text record with its guid, that guid has to be passed in here, and the record checked to have the user prove ownership.
If all is ok, then a token is generated and given back.
A user can only do one server, this is because that user is the server here.

servers have a default rate api and time set to not allow any calls

## get server
The logged-in user, or his admin group, can get details about the server associated with them, including that token generated above.
This token is what is sent to the action call

# delete server
The logged-in user only can remove the server associated with him, this also removes any protected tokens.
Or a user on this server with admin role can do that.

# edit server
Someone with a server admin role can edit this server to have rate api and a schedule set to anything

# call action
the logged in server/user can call this, with its token and the element guid and the remote user guid .
If the action,element, and element type match up for existing and levels, the action is run

# user register
the logged in server or its admin group can register the user guid from here as also there, and get a token back
if not revoked but exising, will get previous token. If revoked gets new token

# user give permission
The user who is registered gives permission to use that token, that user is logged in for this call, not server.
The user is associated with that token.
Optional time to live

# user revoke permission
the user who is registerd refuses that token, so the token is deleted (revoked) and will not be associated with that user


