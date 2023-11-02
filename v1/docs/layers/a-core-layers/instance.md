# Instance 

can only be called by logged-in users who are approved

* Gives instance information (api here allows setting the instance info to permitted users)
* Adds or removes users from the groups that can execute commands to this interface api
  * info user is set by username and pw in .env and makes a regular user from the layers using simple registration
* Allows instance to be put in maintenance mode 
* provides a way to attach plugin listeners for any, or some api calls
* gives a route all api calls to, to be dispatched to the appropriate layer
  * figures out format asked for (json, html) and passes that format to the route being dispatched


# instance description and admin lists for instance

The instance is represented by a user (will create it here, if not existing, and store reference to it).
The instance description and allowed groups does the user api to manage that

The instance user's landing set is the public intro area for the instance

# instance maintenance mode

blocks the route call, returning the maintenance message instead in the call return with http

# plugins are set by composer

use command line to enable or disable listeners to routes.
Logging services are a great way to use the plugins.

# routing

all api calls are sent through the instance.route_call

# Api

## route all calls
    instance.route_call 
  this is where all calls are forwarded 

  * calls `permissions_layer.can_i_do_this`, if cannot return or throw 
  * will use event filter find out where to route, to allow dynamic adding of routes
  * will use event action before and after call to route to allow plugin listeners

## instance info
    instance.info
lists info about the user 


## instance maintenance
    instance.maintenance
someone in the user admin group can set this to be on or off, with optional message set, and optional http code set