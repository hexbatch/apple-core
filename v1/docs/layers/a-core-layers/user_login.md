# Logging In

* This api handles logging in the user via api call
* different ways of logging in provided by plugins
* Social networks logging in handled in the internet layers for the login api
* have an identity api call, and also shows this information after a login with the call return


## Authentication

The OAuth authorization flow uses authorizationUrl, tokenUrl and refreshUrl, these are specified in the open api doc

The user logs in with oath2, always


## Next Layer authentication with the inner core

The outer layers uses Oauth, but they have to log in with the inner core via the job queues.

The outer layers have non expiring bearer token for each user, and there is an admin api that allows these token to be regenerated.

When another user, who is allowed via Oauth roles to act on behalf of a user, makes a call for this user, then when the roles are verified for the logged-in user,
the outer layer will construct the job queue using the behalf-user's token.


## First plugins

Logins:

* Make basic auth for api calls
* Make plugin allowing a username and pw login via form
* Make plugin that can log in with: email and password. (allow form and api)

# API 

## login choice
    user_login.login_choice
shows the list of login choices, reading from its plugins here
each login choice is its own url inside the user_login_layer, created by that plugin
output can be either an html page, or a json response

## show login form
    user_login.show_fields
the plugin handles this.
shows the fields required, and some description for each, to login.
Will give the url to call.
The plugin will decide what to show, and the fields may vary a lot

## do login
    user_login.do_login

the plugin handles this 
* calls `user_services.read_layer_data`
* plugin does verification
* if login successful, returns `user_login.me`


## show me
    user_login.me
* calls `user_services.read_core_data`
* calls `user_services.read_layer_data`

* Shows the user logged in
* Plugin used to log in may have some extra information


