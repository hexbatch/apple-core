# Logging In

This api handles logging in the user using different ways
User here can log in with: id and password, social networks.

Does password resets



## Authentication

The OAuth authorization flow uses authorizationUrl, tokenUrl and refreshUrl, these are specified in the open api doc

The user logs in with oath2, always


### Next Layer authentication with the inner core

The outer layers uses Oauth, but they have to log in with the inner core via the job queues.

The outer layers have non expiring bearer token for each user, and there is an admin api that allows these token to be regenerated.

When another user, who is allowed via Oauth roles to act on behalf of a user, makes a call for this user, then when the roles are verified for the logged-in user,
the outer layer will construct the job queue using the behalf-user's token.
