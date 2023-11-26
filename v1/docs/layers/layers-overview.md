# Once the api for the overview is set up, there are other apis that allow more specific usages

* Instance
* Users
* User Groups
* Sessions
* Registrations
* Authentication and Logging in
* Publishing
* Mirroring
* External Users
* Network Pools
* Networks
* Network discovery
* Distributions
* Auditing
* Contracts
* Marketplace
* Pools
* Agreements
* Transactions
* Deferred
* Organizations
* Stores
* Inventory
* Promotions
* Selling
* Admin
* Boards
* Notes
* Items
* Movement
* Public grants
* Format
* Agents
* Jobs
* Goals
* Tech Trees
* Rates
* Conversions





## Common things in all api requests

* Most require a logged-in user, when that happens, it requires them using a bearer token, acquired in oauth
* an optional checksum can be added to any token passed in, the checksum must match for that token before the api operation is carried out
* all api operations use the jobs api, the work is sent to a job queue
* all api operations use the core api 
* any user can take a resource exposed by the public api, and perform low level operations on it if they have the permissions
* each user has a working set or tells which set they are working from (so they do not leave their working set)


## Instance info
[instance.md](a-core-layers/instance.md)
Gives information about the instance the api is running at. Acts as a first step in interacting with the instance

## Authentication and logging in
[user_login.md](a-core-layers/user_login.md)
Handles users logging in and pw resets 


# Users
[users.md](a-core-layers/users.md)
Read and edit user, manage user sessions, sets up user for first time

# User Groups
[users groups](a-core-layers/user-groups.md)
Do stuff with user groups

# Sessions
[sessions.md](a-core-layers/sessions.md)
manages sessions


# Registrations
[registrations.md](a-core-layers/registrations.md)
Does all the new user account creation


# Publishing
[publishing](d-other-instances/publishing.md)
Api for broadcasting new types and changes in tokens

# Mirroring
[mirroring.md](d-other-instances/mirroring.md)
Updates followed tokens and types that are not based here

# External Users
[external-user.md](d-other-instances/external-user.md)
Coordinates users from other instances here


# Networks
[networks.md](f-interaction-layers/networks.md)
Networks are things online related to a user: social networks, friends lists

[network pools](g-trading-layers/network-pools.md). 
Pools can be used with networks.

# Network discovery
[network-discovery.md](i-promotion-layers/network-discovery.md)
Makes new network entry tokens. Scans social networks.


# Distributions
[distributions.md](i-promotion-layers/distributions.md)
Organizes new tokens and token pools,  given to users and and network entities


# Contracts
[contracts.md](g-trading-layers/contracts.md)
Deals with the selling, terms, and use of token types


# Marketplace
Ownerships of tokens is swapped as is, no refunds. Supports direct sales and auctions
[marketplace](g-trading-layers/marketplace.md)


# Transactions
[transactions.md](e-organization-layers/transactions.md)
The transaction layer changes ownership of tokens after an agreement between two or more people.
Transactions can be in many parts and swap more than one owner. All have to succeed for the ownership to be changed for any

# Auditing
[auditing](e-organization-layers/auditing.md)
Api for record keeping/verification of transactions






# Pools
[pools.md](e-organization-layers/pools.md)
Pools are a resource that generates future tokens. Each batch made has a different owner.


# Agreements
[agreements.md](e-organization-layers/agreements.md)
Are how to reach consensus and do group driven actions

# Deferred
[deferred.md](e-organization-layers/deferred.md)
Agreed things done by script or remote

# Organizations
[organizations.md](e-organization-layers/organizations.md)
Organizations are groups of users that share a wallet and use agreements by voting based on how much the org they own


# Stores
[stores.md](h-selling-layers/stores.md)
Stores sell inventory


# Inventory
[inventory.md](h-selling-layers/inventory.md)
Items in a store for sale, goods need not be physical or even real



# Promotions
[promotions](i-promotion-layers/promotions.md)
Advertisement agreements for promotion of sales inventory


# Selling
[selling](h-selling-layers/selling.md)
Sets up a sales flow that tracks different sales events from customer wanting to buy, to buying, to delivery, to issues, to feedback

# Admin
[admin.md](b-user-layers/admin-base.md)
Admins will do stuff, logged in as other users



# Jobs
[jobs.md](a-core-layers/jobs.md)
Jobs are used internally by the layers to execute stuff


# Format
[format](c-personal-layers/format.md)
  Will convert a token set to html , or markdown. Other formats can be added as plugins for that project


# Boards
[boards.md](f-interaction-layers/boards.md)
Conversations either in chat or forums or posts. Can be read only or other stuff


# Notes
[notes](c-personal-layers/notes.md)
Organize text,images, links, lists


# Items
[Items](f-interaction-layers/items.md)
Allow sharing and communities


# Movement
[movement.md](f-interaction-layers/movement.md)
Tokens can move, on their own, through set relationships by always going to the set that best fits them with their affinity. 
This only happens if the affinity or allergies are set up for the token, and its registered


# Public grants
[public-grants.md](b-user-layers/low-level-access.md)
Allow some users to do some low level operations




# Agents
[agents.md](b-user-layers/agents.md)
Agents are those that are authorized to do token changes outside the server


## Jobs
[jobs.md](a-core-layers/jobs.md)
Each public api call is put into a job queue, which is executed and then makes a private network call back to the waiting task,
which either returns the output to the user, if the http call is waiting, or calls the url the user set, or the user can poll later


## Goals
[goals](m-eco-layers/goals.md)
Get resources for achievements


## Tech trees
[tech-trees](m-eco-layers/tech-trees.md)
Figure things out, and get rewards


## Rates
[rates](a-core-layers/rates.md)
How api rate limits are granted


## Conversions
[conversions](m-eco-layers/conversions.md)
Convert data to shapes and sets

