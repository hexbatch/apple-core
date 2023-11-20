# Once the api for the overview is set up, there are other apis that allow more specific usages

* Instance
* Users
* User Groups
* Sessions
* Registrations
* Authentication and Logging in
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
* User Proxy
* Deferred
* Organizations
* Stores
* Inventory
* Promotions
* Selling
* Watchers
* Admin
* Moderator
* Boards
* Notes
* Items
* Movement
* Public grants
* Format
* Export and Verification
* Agents
* Jobs
* Shapes
* Audio
* Avatars
* Mutual Editor
* Goals
* Tech Trees
* Rates
* Conversions
* Eco





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


# Networks
[networks.md](e-interaction-layers/networks.md)
Networks are things online related to a user: social networks, friends lists

[network pools](f-trading-layers/network-pools.md). 
Pools can be used with networks.

# Network discovery
[network-discovery.md](i-promotion-layers/network-discovery.md)
Makes new network entry tokens. Scans social networks.


# Distributions
[distributions.md](i-promotion-layers/distributions.md)
Organizes new tokens and token pools,  given to users and and network entities


# Contracts
[contracts.md](f-trading-layers/contracts.md)
Deals with the selling, terms, and use of token types


# Marketplace
Ownerships of tokens is swapped as is, no refunds. Supports direct sales and auctions
[marketplace](f-trading-layers/marketplace.md)


# Transactions
[transactions.md](d-organization-layers/transactions.md)
The transaction layer changes ownership of tokens after an agreement between two or more people.
Transactions can be in many parts and swap more than one owner. All have to succeed for the ownership to be changed for any

# Auditing
[Auditing](d-organization-layers/auditing.md)
Api for record keeping of new types and public transactions




# Pools
[pools.md](d-organization-layers/pools.md)
Pools are a resource that generates future tokens. Each batch made has a different owner.


# Agreements
[agreements.md](d-organization-layers/agreements.md)
Are how to reach consensus and do group driven actions

# Deferred
[deferred.md](d-organization-layers/deferred.md)
Agreed things done by script or remote

# Organizations
[organizations.md](d-organization-layers/organizations.md)
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

# Watchers
[Watchers](b-user-layers/watcher.md) trigger events when some condition is reached with tokens and sets


# Admin
[admin.md](b-user-layers/admin-base.md)
Admins will do stuff, logged in as other users


# Moderator
[moderators.md](d-organization-layers/moderators.md)
Moderators have permissions to change and remove selected attributes from a set of token types.


# Jobs
[jobs.md](a-core-layers/jobs.md)
Jobs are used internally by the layers to execute stuff


# Format
[format](c2-personal-layers/format.md)
  Will convert a token set to html , or markdown. Other formats can be added as plugins for that project


# Boards
[boards.md](e-interaction-layers/boards.md)
Conversations either in chat or forums or posts. Can be read only or other stuff


# Notes
[notes](c2-personal-layers/notes.md)
Organize text,images, links, lists


# Items
[Items](e-interaction-layers/items.md)
Allow sharing and communities


# Movement
[movement.md](e-interaction-layers/movement.md)
Tokens can move, on their own, through set relationships by always going to the set that best fits them with their affinity. 
This only happens if the affinity or allergies are set up for the token, and its registered


# Public grants
[public-grants.md](b-user-layers/public-grants.md)
Allow some users to do some low level operations


# Export, Import and Verification
[export-import-verification.md](j-internet-layers/export-import-verification.md)
How tokens across different servers and installs can work together


# Agents
[agents.md](b-user-layers/agents.md)
Agents are those that are authorized to do token changes outside the server


## Jobs
[jobs.md](a-core-layers/jobs.md)
Each public api call is put into a job queue, which is executed and then makes a private network call back to the waiting task,
which either returns the output to the user, if the http call is waiting, or calls the url the user set, or the user can poll later

## User Proxy
[user-proxy.md](b-user-layers/user-proxy.md)
Internal api to allow one user to do things as another user


## Shapes
[shapes](k-representation-layers/shapes.md)
Sets can have 3d shapes and be in an area they intersect each other and move

## Audio
[audio](k-representation-layers/audio.md)
Sets can make sounds


## Avatars
[set-avatar](k-representation-layers/set-avatar.md)
Sets can be animated by outside programs


## Mutual Editor
[mutual-editor](k-representation-layers/mutual-editor.md)
View and edit mutual relations


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

## Eco
[eco](m-eco-layers/eco.md)
Plants and animals 

