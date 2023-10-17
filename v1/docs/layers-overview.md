# Once the api for the overview is set up, there are other apis that allow more specific usages

* Users
* Registrations
* Sets
* Networks
* Distributions
* Contracts
* Marketplace
* Trends
* Organizations
* Stores
* Inventory
* Promotions
* Selling
* Agents
* Admin
* Moderator
* Boards
* Export and Verification
* Events
* Format
* Token
* Jobs

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

* Manages existing users
* Manages and creates user groups


# Sets 

create and edit token sets



# Registrations

Does all the new user account creation

* allows people to create accounts using different social media
* allows to join other social network logins to this
* once a person joins using a type of login, all the tokens associated to that social account is given to them

# Networks

Networks are stored in the core as token sets. It creates social account entries (each entry a token) which is a token set
and then for each entry has a structure of tokens representing the social people

These social tokens are owned by the person who discovered them, and can be traded on the marketplace

* discover networks connected to users
* create subnetworks by filtering a network of social accounts by different attributes. The subnetwork is a new token that inherits from the network token

# Distributions

* generates new tokens of type(s) and quantity to networks of people 
* the people in the networks are not users, but once they join, by registration, then any tokens assigned to them previously are theirs 

# Contracts

Deals with the selling, terms, and use of token types

Contracts is the ability to use a token type, owned by someone else, as a parent for new token types

* Can set up rates, terms, limits and costs
* Can set up how the costs are paid

# Marketplace

Ownerships of token sets can be bought and sold

Deals with token sets

* There is no sales flow here, or buying rights to use future tokens, all sales are immediate and final
* A token set, or collection of token sets, is  marked as up for sale
  * A sale can have a closing time, after which the user can make a new sale 
* Users can make offers
* The seller selects an offer

# Trends

Public read only list of token types and quantity bought and sold, or contracted (who, when, amount, payment)

# Organizations

Organizations are groups that have tokens that use some specialized attributes to use in commerce and promotion of inventory to be sold

# Stores

Stores sell inventory

* Store inherits from the organization token
* Stores promote collections of inventory
* Users can be registered as salesmen for the store, and they can be selling the inventory
* Manages sells flows

# Inventory
Items in a store for sale, goods need not be physical or even real

* creates a token, based on the store
* specialized attributes for selling and displaying

# Promotions

Sets up time and location of advertising by users who will promote this. Uses marketplace and inventory

For example, say that I, as a user, sets up a map app on my website and agree to do X impressions in searches and map pins, etc

* sets up the inventory to promote, and the terms
* sets up callback urls to verify the promotions were actually seen in a browser, or app
* sets up the looks and feels of the promotions
* keeps track of impressions

# Selling
Sets up a sales flow that tracks different sales events from customer wanting to buy, to buying, to delivery, to issues, to feedback

# Admin

* Does maintenance on the tokens used by the outer layers
* Reviews stuck jobs, and can terminate them
* User operations: freeze, delete
* Token operations and sets: change their ownership
* Contracts: can change terms of a contract
* Moderators: sets up and manages

# Moderator

Moderators can see all the changed attribute values that they have dominion over.
They have ability to edit attribute values they have permissions for.

Additionally, users can chose to designate another user to moderator something they control. So company moderators can exist, for example (or sales managers)

# Jobs

a job can update its status using the job reference, only users who have the job-write role can use this.

job metrics can be queried, only users who have the job-read role can use this

job metrics allow hooks to be added to allow for events below

# Events 
  
  Events hook into the job metrics, and allow users to set up url callbacks with changes to things that they see

# Format

  Will convert a token set to html , or markdown. Other formats can be added as plugins for that project

# Boards

There can be both general discussion chat rooms and review area. Some chat rooms can have upvotes.

Board entries can have media as well as markdown, and have options to allow replies

# Export, Import and Verification

* can send a token set as serialized
* can import a serialized token set
* can query the originating server, of a copied token, to see if data is accurate, or if an attribute is in a range or regex
* a logged-in user to the originating server, can alter the original token, and then the changes of state can be propagated out in the next export

# Agents

Agents are those that agree to do token changes outside the server, and report back the changes to make to the tokens.
This can be used with the export, import and verification between different servers, or do some other thing 


# Token

Allow high level token operations

* Users can create tokens that inherit from their own token
* Create and edit attributes, create new token types and tokens, edit token attribute values 
* Allow media uploads to attributes that support those
* Script attributes cannot be added or edited 


