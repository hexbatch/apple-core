# Once the api for the overview is set up, there are other apis that allow more specific usages

* Users
* Registrations
* Authentication and Logging in
* Networks
* Network discovery
* Distributions
* Contracts
* Marketplace
* Trends
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
* Events
* Format
* Export and Verification
* Agents
* Jobs

## Common things in all api requests

* Most require a logged-in user, when that happens, it requires them using a bearer token, acquired in oauth
* an optional checksum can be added to any token passed in, the checksum must match for that token before the api operation is carried out
* all api operations use the jobs api, the work is sent to a job queue
* all api operations use the core api 

## Authentication and logging in

Handles users logging in and pw resets [user_login.md](layers/user_login.md)




# Users

* read and edit user , do user group stuff, handles some system data
* Manages and creates user groups

[users.md](layers/users.md)



# Registrations

Does all the new user account creation

* allows people to create accounts using different social media
* allows to join other social network logins to this
* once a person joins using a type of login, all the tokens associated to that social account is given to them

# Networks
[networks.md](layers/networks.md)

Networks are things related to a user. These resources might become future users, or become other resources.
Tracks social accounts that are not users, and then later are

# Network discovery
[network-disovery.md](layers/network-disovery.md)
Makes new network entry tokens. Scans social networks.

# Distributions
[distributions.md](layers/distributions.md)
Organizes new tokens and token pools,  given to users and and network entities

# Contracts
[contracts.md](layers/contracts.md)

Contracts is the ability to use a token type, owned by someone else, as a parent for new token types

* Can set up rates, terms, limits and costs
* Can set up how the costs are paid

# Marketplace

Ownerships of tokens is swapped as is, no refunds. Supports direct sales and auctions
[marketplace](layers/marketplace.md)


# Trends

Public read only list of token types and quantity bought and sold, or contracted (who, when, amount, payment)

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

Sets up time and location of advertising by users who will promote this. Uses marketplace and inventory

For example, say that I, as a user, sets up a map app on my website and agree to do X impressions in searches and map pins, etc

* sets up the inventory to promote, and the terms
* sets up callback urls to verify the promotions were actually seen in a browser, or app
* sets up the looks and feels of the promotions
* keeps track of impressions

# Selling

Ownerships of token sets is swapped  [selling](layers/selling.md)
Sets up a sales flow that tracks different sales events from customer wanting to buy, to buying, to delivery, to issues, to feedback

# Watchers 

[Watchers](layers/watcher.md) trigger events when some condition is reached with tokens and sets


# Admin
[admin.md](layers/admin.md)
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

[jobs.md](layers/jobs.md)

Jobs are used internally by the layers to execute stuff

# Events 
  
  Events hook into the job metrics, and allow users to set up url callbacks with changes to things that they see

# Format

  Will convert a token set to html , or markdown. Other formats can be added as plugins for that project

# Boards
[boards.md](layers/boards.md)
There can be both general discussion chat rooms, read only review area. Some chat rooms can have upvotes.

Board entries can have media as well as markdown, and have options to allow replies.

Private individual chats and group chats.

# Export, Import and Verification
[export-import-verification.md](layers/export-import-verification.md)

How tokens across different servers and installs can work together


# Agents
[agents.md](layers/agents.md)
Agents are those that are authorized to do token changes outside the server


## Job Queues

Each public api call is put into a job queue, which is executed and then makes a private network call back to the waiting task,
which either returns the output to the user, if the http call is waiting, or calls the url the user set, or the user can poll later

[jobs.md](layers/jobs.md)

