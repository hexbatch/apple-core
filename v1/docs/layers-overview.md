# Once the api for the overview is set up, there are other apis that allow more specific usages

* Users
* Registrations
* Authentication and Logging in
* Networks
* Network discovery
* Distributions
* Contracts
* Marketplace
* Pools
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
* Public grants
* Format
* Export and Verification
* Agents
* Jobs

## Common things in all api requests

* Most require a logged-in user, when that happens, it requires them using a bearer token, acquired in oauth
* an optional checksum can be added to any token passed in, the checksum must match for that token before the api operation is carried out
* all api operations use the jobs api, the work is sent to a job queue
* all api operations use the core api 
* any user can take a resource exposed by the public api, and perform low level operations on it if they have the permissions



## Authentication and logging in
[user_login.md](layers/user_login.md)
Handles users logging in and pw resets 


# Users
[users.md](layers/users.md)
Read and edit user, user group stuff, handles some system data


# Registrations
[registrations.md](layers/registrations.md)
Does all the new user account creation


# Networks
[networks.md](layers/networks.md)
Networks are things online related to a user: social networks, friends lists


# Network discovery
[network-disovery.md](layers/network-disovery.md)
Makes new network entry tokens. Scans social networks.


# Distributions
[distributions.md](layers/distributions.md)
Organizes new tokens and token pools,  given to users and and network entities


# Contracts
[contracts.md](layers/contracts.md)
Deals with the selling, terms, and use of token types


# Marketplace
Ownerships of tokens is swapped as is, no refunds. Supports direct sales and auctions
[marketplace](layers/marketplace.md)


# Pools
[pools.md](layers/pools.md)
Pools are a resource that generates future tokens. Each batch made has a different owner.


# Organizations
[organizations.md](layers/organizations.md)
Organizations are groups of users that share a wallet and can vote on things to do


# Stores
[stores.md](layers/stores.md)
Stores sell inventory


# Inventory
[inventory.md](layers/inventory.md)
Items in a store for sale, goods need not be physical or even real


# Promotions
[promotions](layers/promotions.md)
Advertisement agreements for promotion of sales inventory


# Selling
[selling](layers/selling.md)
Sets up a sales flow that tracks different sales events from customer wanting to buy, to buying, to delivery, to issues, to feedback

# Watchers
[Watchers](layers/watcher.md) trigger events when some condition is reached with tokens and sets


# Admin
[admin.md](layers/admin.md)
Admins will do stuff, logged in as other users


# Moderator
[moderators.md](layers/moderators.md)
Moderators have permissions to change and remove selected attributes from a set of token types.


# Jobs
[jobs.md](layers/jobs.md)
Jobs are used internally by the layers to execute stuff


# Format
[format](layers/format.md)
  Will convert a token set to html , or markdown. Other formats can be added as plugins for that project


# Boards
[boards.md](layers/boards.md)
Conversations either in chat or forums or posts. Can be read only or other stuff


# Notes
[notes](layers/notes.md)
Organize text,images, links, lists


# Items
[Items](layers/items.md)
Allow sharing and communities


# Public grants
[public-grants.md](layers/public-grants.md)
Allow some users to do some low level operations


# Export, Import and Verification
[export-import-verification.md](layers/export-import-verification.md)
How tokens across different servers and installs can work together


# Agents
[agents.md](layers/agents.md)
Agents are those that are authorized to do token changes outside the server


## Jobs
[jobs.md](layers/jobs.md)
Each public api call is put into a job queue, which is executed and then makes a private network call back to the waiting task,
which either returns the output to the user, if the http call is waiting, or calls the url the user set, or the user can poll later



