# Once the api for the overview is set up, there are other apis that allow more specific usages

* [instance.md](a-inner-layers/instance.md)
* [rates.md](a-inner-layers/rates.md)
* [sessions.md](b-user-layers/sessions.md)
* [jobs.md](a-inner-layers/jobs.md)
* [low-level-access.md](a-inner-layers/low-level-access.md)


* [agents.md](b-user-layers/agents.md)
* [registrations.md](b-user-layers/registrations.md)
* [user_login.md](b-user-layers/user_login.md)
* [users.md](b-user-layers/users.md)
* [user-groups.md](b-user-layers/user-groups.md)


* [notes.md](c-personal-layers/notes.md)
* [format.md](c-personal-layers/format.md)


* [publishing.md](d-connection-layers/publishing.md)
* [mirroring.md](d-connection-layers/mirroring.md)
* [external-user.md](d-connection-layers/external-user.md)


* [agreements.md](e-organization-layers/agreements.md)
* [deferred.md](e-organization-layers/deferred.md)
* [pools.md](e-organization-layers/pools.md)
* [organizations.md](e-organization-layers/organizations.md)

* [auditing.md](f-transactions/auditing.md)
* [transactions.md](f-transactions/transactions.md)
* [contracts.md](f-transactions/contracts.md)


* [boards.md](g-interaction-layers/communication.md)
* [items.md](g-interaction-layers/items.md)







## Common things in all api requests

* Most require a logged-in user, when that happens, it requires them using a bearer element, acquired in oauth
* an optional checksum can be added to any element passed in, the checksum must match for that element before the api operation is carried out
* all api operations use the jobs api, the work is sent to a job queue
* all api operations use the core api 
* any user can take a resource exposed by the public api, and perform low level operations on it if they have the permissions
* each user has a working set or tells which set they are working from (so they do not leave their working set)


## Instance info
[instance.md](a-inner-layers/instance.md)
Gives information about the instance the api is running at. Acts as a first step in interacting with the instance

## Authentication and logging in
[user_login.md](b-user-layers/user_login.md)
Handles users logging in and pw resets 


# Users
[users.md](b-user-layers/users.md)
Read and edit user, manage user sessions, sets up user for first time

# User Groups
[users groups](b-user-layers/user-groups.md)
Do stuff with user groups

# Sessions
[sessions.md](b-user-layers/sessions.md)
manages sessions


# Registrations
[registrations.md](b-user-layers/registrations.md)
Does all the new user account creation


# Publishing
[publishing](d-connection-layers/publishing.md)
Api for broadcasting new types and changes in elements

# Mirroring
[mirroring.md](d-connection-layers/mirroring.md)
Updates followed elements and types that are not based here

# External Users
[external-user.md](d-connection-layers/external-user.md)
Coordinates users from other instances here



# Contracts
[contracts.md](f-transactions/contracts.md)
Deals with the selling, terms, and use of element types




# Transactions
[transactions.md](f-transactions/transactions.md)
The transaction layer changes ownership of elements after an agreement between two or more people.
Transactions can be in many parts and swap more than one owner. All have to succeed for the ownership to be changed for any

# Auditing
[auditing](f-transactions/auditing.md)
Api for record keeping/verification of transactions






# Pools
[pools.md](e-organization-layers/pools.md)
Pools are a resource that generates future elements. Each batch made has a different owner.


# Agreements
[agreements.md](e-organization-layers/agreements.md)
Are how to reach consensus and do group driven actions

# Deferred
[deferred.md](e-organization-layers/deferred.md)
Agreed things done by script or remote

# Organizations
[organizations.md](e-organization-layers/organizations.md)
Organizations are groups of users that share a wallet and use agreements by voting based on how much the org they own





# Jobs
[jobs.md](a-inner-layers/jobs.md)
Jobs are used internally by the layers to execute stuff


# Format
[format](c-personal-layers/format.md)
  Will convert an element set to html , or markdown. Other formats can be added as plugins for that project


# Boards
[boards.md](g-interaction-layers/communication.md)
Conversations either in chat or forums or posts. Can be read only or other stuff


# Notes
[notes](c-personal-layers/notes.md)
Organize text,images, links, lists


# Items
[Items](g-interaction-layers/items.md)
Allow sharing and communities




# Public grants
[public-grants.md](a-inner-layers/low-level-access.md)
Allow some users to do some low level operations




# Agents
[agents.md](b-user-layers/agents.md)
Agents are those that are authorized to do element changes outside the server


## Jobs
[jobs.md](a-inner-layers/jobs.md)
Each public api call is put into a job queue, which is executed and then makes a private network call back to the waiting task,
which either returns the output to the user, if the http call is waiting, or calls the url the user set, or the user can poll later





## Rates
[rates](a-inner-layers/rates.md)
How api rate limits are granted




