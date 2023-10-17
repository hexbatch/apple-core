# Administration

Admins will do stuff, logged in as other users, when the core api is executed.

Super admins can log in as anyone to do anything.

Restricted admins can only log in as some people to do some actions.

Moderators are restricted further, able to log in as some people, and change a list of attributes.

The administration layer will find the tokens and users the admins and moderators can use by using the set operations.

One thing that helps this is that different user groups can be made, by changing the base user token. Also, giving users attributes that they cannot read or write to allows sorting


## User operations

* makes sure the next layers have a good bearer token for the users registered in the inner core.
* makes sure the user accounts in the next layers are matched correctly with the user accounts in the inner core
* Freezes a user (by setting an attribute in the user token that disallows any set transfers, and the attribute cannot be removed or changed by the user)
* Deletes a user info

## Tokens

* Can change who owns tokens

## Contracts
* can change the terms of a contract

## setting up moderators

* Sets up moderators for region, tags, or time, and for specific attributes they can edit
* For example, a moderator can be setup to review all feedback for sales in the livingston area. Or a moderator can review all media for a special event on Tuesday
* Can also remove or adjust moderators setup in the admin panel or in the moderator api

## Jobs

* Reviews stuck jobs, and can terminate them
* Sees job metrics and outputs

## Promotions

* Reviews promotions and can alter the promotion deal

## Sells

Views sell metrics and reviews