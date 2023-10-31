# Instance 

can only be called by logged-in users who are approved

* Gives instance information (api here allows setting the instance info to permitted users)
* Adds or removes users from the groups that can execute commands to this interface api
* Allows instance to be rebooted, shut down, maintenance mode (not the servers, but the instance itself)
* Sets up an optional whitelist of allowed visitors, and what they can do
* set up logging contact info 
* provides a way to attach plugin listeners for any, or some api calls
* gives a route all api calls to, to be dispatched to the appropriate layer
  * figures out format asked for (json, html) and passes that format to the route being dispatched
* able to show terms of service page to anyone
* able to show privacy page to anyone
* able to show admin login area, admin landing page, give way to do all the above via web or console

# Api

## route all calls
    instance.route_call
  * calls `permissions_layer.can_i_do_this`, if cannot return or throw 
  * will use event filter find out where to route, to allow dynamic adding of routes
  * will use event action before and after call to route to allow plugin listeners
