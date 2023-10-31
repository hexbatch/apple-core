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

## Authentication

The OAuth authorization flow uses authorizationUrl, tokenUrl and refreshUrl, these are specified in the open api doc

The user logs in with oath2, always


## Next Layer authentication with the inner core

The outer layers uses Oauth, but they have to log in with the inner core via the job queues.

The outer layers have non expiring bearer token for each user, and there is an admin api that allows these token to be regenerated.

When another user, who is allowed via Oauth roles to act on behalf of a user, makes a call for this user, then when the roles are verified for the logged-in user,
the outer layer will construct the job queue using the behalf-user's token.


## First plugins


* Make basic auth for api calls
* Make plugin allowing a username and pw login via form
* Make plugin that can log in with: email and password. (allow form and api)
