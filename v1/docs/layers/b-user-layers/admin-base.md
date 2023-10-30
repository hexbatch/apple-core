# Administration

* Does maintenance on the tokens used by the outer layers
* Reviews stuck jobs, and can terminate them
* User operations: freeze, delete



Admins will do stuff, logged in as other users, when the core api is executed.

Super admins can log in as anyone to do anything.

Restricted admins can only log in as some people to do some actions.



The administration layer will find the tokens and users the admins and moderators can use by using the set operations.

One thing that helps this is that different user groups can be made, by changing the base user token. Also, giving users attributes that they cannot read or write to allows sorting


## User operations

* makes sure the next layers have a good bearer token for the users registered in the inner core.
* makes sure the user accounts in the next layers are matched correctly with the user accounts in the inner core
* Freezes a user (by setting an attribute in the user token that disallows any set transfers, and the attribute cannot be removed or changed by the user)
* Deletes a user info
* Sets up a whitelist api calls for user groups




## Jobs

* Reviews stuck jobs, and can terminate them
* Sees job metrics and outputs



