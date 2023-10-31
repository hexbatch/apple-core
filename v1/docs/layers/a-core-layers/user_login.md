# Logging In

* This api handles logging in the user using different ways by setting up plugins to handle each
  * allows logging in via api call and no web page
  * if api or console then return a me api to show the logged-in user information
  * Shows a user landing url if browser call
* Social networks logging in handled in the internet layers for the login api
* handle regulation demanded forms
* have a user landing page, or if api a me
  * in the landing page or me, show news
* set text only news items (date and news) to show
* another series of plugins here can add to the user homepage (me)

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
    user_login.show_form
shows the form to fill out to login.
The plugin will decide what form to show

## do login
    user_login.do_login
can be called via api call or webpage
the plugin handles this (oauth or other social leading to oauth)
* calls `user_services.read_layer_data`
* plugin does verification
* if login successful, returns either the json me or the webpage me,


## show me
    user_login.me
* calls `user_services.read_core_data`
* calls `user_services.read_layer_data`

if webpage, this is where any regulation forms might be at.
Shows news.
the plugins for the homepage handle the formatting and content of this page


