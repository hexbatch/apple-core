# Once the api for the overview is set up, there are other apis that allow more specific usages

* Users
* Wallet
* Distributions
* Contracts
* Stores
* Inventory
* Selling
* Admin
* Moderator
* Boards
* Internal

## Authentication

Each next layer api call should have the option to immediately execute its job rather than putting it on the job queue, and always return the results.
This is used for testing. The option is only honored if the logged-in user has the tester role

### Next Layer authentication with the inner core

The outer layers uses Oauth, but they have to log in with the inner core via the job queues.

The outer layers have non expiring bearer token for each user, and there is an admin api that allows these token to be regenerated.

When another user, who is allowed via Oauth roles to act on behalf of a user, makes a call for this user, then when the roles are verified for the logged-in user,
the outer layer will construct the job queue using the behalf-user's token.

## Job Queues

Because there is reliance for executed javascript, as well as some db intensive operations.
Then some operations, if not all, should be done by a job queue, and the api caller should get back a callback reference
and if the api caller provides a url, or another form of callback, then the api will let them know when its done.

The core api does not do callback, but the next layer api will, and what the layers will do is set up some nested operations into a job queue.
The operations will have ties so that they are done in order, and the needed values from the yet to be executed ops are fed into the ops waiting for them.
For example, when making a new token, then doing something with it, like putting it into a set.

So the job data should have both the user that is logged in at the time, and the operations are done in the context of that user, and the callback reference and url.
This implies that the user should have a token to be used, when calling the core api. And the token should expire at the end of the job.
This means that the core api should use Bearer tokens, and have the api to revoke it


* see https://swagger.io/docs/specification/authentication/bearer-authentication/
* https://laravel.com/docs/10.x/sanctum#api-token-authentication

### Polling or callback or both

The callback does not need to be defined, instead, there is an api call to get the results using the job reference.
This job data/status data is only seen by using the reference and if the logged-in user is the one who made the reference, or the user who had the api done by permission
This implies there needs to be a data storage for the job reference, and has the calling user, the operational user, the job status and job api call response data, and the callback url,
and whether the callback url call was successful or not.

This way there can be cron jobs to try the callback url later, maybe.

This also means there needs to be an api to update the job reference by the job. but that api should not be exposed to the public.
Instead, the job itself is logged in as its own user to the outer layers, and has its permission set to use this api.
Probably all jobs can be the same user. See internal api

# Users

* Manages and creates users
* Manages and creates user groups



# Admin

## User operations

makes sure the next layers have a good bearer token for the users registered in the inner core.

makes sure the user accounts in the next layers are matched correctly with the user accounts in the inner core

Freezes a user

Deletes a user

## setting up moderators

Sets up moderators for region, tags, or time, and for specific attributes they can edit

For example, a moderator can be setup to review all feedback for sales in the livingston area. Or a moderator can review all media for a special event on Tuesday

Can also remove or adjust moderators setup in the admin panel or in the moderator api

# Moderator

Moderators can see all the changed attribute values that they have dominion over.
They have ability to edit attribute values they have permissions for.

Additionally, users can chose to designate another user to moderator something they control. So company moderators can exist, for example (or sales managers)

# Internal

a job can update its status using the job reference, only users who have the job-write role can use this.

job metrics can be queried, only users who have the job-read role can use this

# Boards

There can be both general discussion chat rooms and review area. Some chat rooms can have upvotes.

Board entries can have media as well as markdown, and have options to allow replies
