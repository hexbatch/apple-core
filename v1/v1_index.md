# Apple core version 1

This is an api for a set of ideas. 

* There is an inner core that provides the general logic for the rest of the layers
* There is a layer of services that defines some interaction and introduces concepts
* The services are shown in a presentation and ui layer

This set of documentation describes the first two levels of concepts: the core and the layers.
It does not try to make any web pages or gui, but some services will generate html.

The central idea is the core, this does all the heavy lifting for the common concepts.
And then there are a set of layers, microservices, which use the core, to help expand the concepts

Each part can run on different machines. But it's planned to use kubernetes to have them together with fast networking and scaling.

The apis share some [general-api-usage](docs/core/core-api-general/general-api-usage.md)

# The core

The Core deals with the basic data types described in [core-overview.md](docs/core/core-overview.md).

The core api list is at [core-api-list.md](docs/core/core-api-list.md)

The core api will have a full testing coverage and suit. 

See [core-development-overview.md](dev/core-development-overview.md)

## List of expansions in the core

There are some cool stuff that can be done at the core level, that is not universally needed by all operations

| Expansion                        | Description                        | Link                                                                         |
|----------------------------------|------------------------------------|------------------------------------------------------------------------------|
| Overview                         | Intro how these are organized      | [aa-overview.md](docs/layers/y-core-expansions/aa-overview.md)               |
| Aggregations                     | Reduce values in sets              | [aggregations.md](docs/layers/y-core-expansions/aggregations.md)             |
| Iterations                       | Organize successive api calls      | [iterations.md](docs/layers/y-core-expansions/iterations.md)                 |
| Push Pop                         | Organize api calls done in batches | [push-pops.md](docs/layers/y-core-expansions/push-pops.md)                   |
| Dynamic Filters and requirements | Expand the concept of filters      | [filters.md](docs/layers/y-core-expansions/dynamic-filters.md)               |
| Same set location searching      | Using shape relations              | [location-searching.md](docs/layers/y-core-expansions/location.md) |
| Mutuals                          | Interlinked sets                   | [mutuals.md](docs/layers/y-core-expansions/mutuals.md)                       |
| Interfaces                       | Higher order data flow             | [interfaces.md](docs/layers/y-core-expansions/interfaces.md)                 |


# Layers
The layers overview is talked about in [layers overview](docs/layers/layers-overview.md)

The layers each do their own thing, but they have a few things in common.
Most of the heavy lifting in the layer codes will be done by api calls to the core.
They set up jobs to be dispatched and completed later. But often, the caller to these layers will not notice because that is hidden and fast.

The caller can decide how to get the results, he can wait for the api call to return, or he can use a callback url, or do polling later.

The core has its own user and authentication system. The layers use OAuth2 to register and log-in people.
The layers talk to the core by storing core user bearer tokens that do not expire, and when they need to do the core to do things,
they dispatch jobs using a temporary auth token that expires at the end of the job.

The core itself does not have a superuser, or root user.
But it does have a permission system. So the layers can be doing actions as different users to implement nested permissions.


When a public api request is made, a job is made that has a list of api core calls to make.

* A temporary bearer token is created for this job only.
* The job is put on a queue.
* When the job is run, the apis are called, using the output of earlier calls to be params for the later calls.
* The job api is updated, the temp bearer token is undone, and job result sent back via a callback url to the layer that created the job.
* If the api caller did not specify a callback and wants to wait, then the results are sent back directly.
* Otherwise, the original caller can poll or listen to the url it gave the layer for the callback

Each layer api, including the core, can be different instances, containers or pods and there can be many copies of each running behind a load balancer.
The jobs can be executed by a pool of waiting things that can grow or shrink in number as needed.
This allows horizontal scaling. All the resources can also run in one k8 or docker compose, to allow testing and development

General api call in the layer:

    public -> outer layers -> job queue 
    -> inner core -> job sends back results via the url to the outer layer
    -> outer layer sends callback to public,
        or public will use a poll reference,
        or public waits for response and data sent back in same call


# Order of writing layers

Each layer has its own iteration of writing the api and code.

[order-writing-layers.md](docs/layers/order-writing-layers.md)

# List of layers

| Layer                         | Description                                                           | Link                                                                     |
|-------------------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------------|
| Instance                      | About the instance the api is running on                              | [instance](docs/layers/a-core-layers/instance.md)                        |
| Users                         | Manages existing users (non admin)                                    | [users](docs/layers/a-core-layers/users.md)                              |
| User Groups                   | Do stuff with user groups                                             | [users groups](docs/layers/a-core-layers/user-groups.md)                 |
| Sessions                      | Provides sessions to interact with the core                           | [sessions](docs/layers/a-core-layers/sessions.md)                        |
| Registrations                 | Does all the new user account creation                                | [registrations](docs/layers/a-core-layers/registrations.md)              |
| Authentication and Logging in | Handles users logging in and pw resets                                | [user_login](docs/layers/a-core-layers/user_login.md)                    |
| Publishing                    | Api for broadcasting new types and changes in tokens                  | [publishing](docs/layers/d-other-instances/publishing.md)                |
| Mirroring                     | Updates followed tokens and types that are not based here             | [mirroring](docs/layers/d-other-instances/mirroring.md)                  |
| External Users                | Coordinates users from other instances here                           | [external-users](docs/layers/d-other-instances/external-user.md)         |
| Networks                      | Networks are things online related to a user                          | [networks](docs/layers/f-interaction-layers/networks.md)                 |
| Network Pools                 | Pools used with networks                                              | [network pools](docs/layers/g-trading-layers/network-pools.md)           |
| Network discovery             | Makes new network entry tokens. Scans social networks.                | [network-discovery](docs/layers/i-promotion-layers/network-discovery.md) |
| Distributions                 | Gives new and existing tokens to users and people in networks         | [distributions](docs/layers/i-promotion-layers/distributions.md)         |
| Contracts                     | Terms of using someone's token in your own stuff. Auto payments       | [contracts](docs/layers/g-trading-layers/contracts.md)                   |
| Marketplace                   | Ownerships of token sets can be bought and sold                       | [marketplace](docs/layers/g-trading-layers/marketplace.md)               |
| Pools                         | Pools are a resource that generates future tokens                     | [pools](docs/layers/e-organization-layers/pools.md)                      |
| Organizations                 | They are companies or people who do stores                            | [organizations](docs/layers/e-organization-layers/organizations.md)      |
| Agreements                    | Reach consensus to do group driven actions                            | [agreements](docs/layers/e-organization-layers/agreements.md)            |
| Transactions                  | Changes ownership of tokens after an agreement                        | [transactions.md](docs/layers/e-organization-layers/transactions.md)     |
| Auditing                      | Api for record keeping/verification of transactions                   | [Auditing](docs/layers/e-organization-layers/auditing.md)                |
| Deferred                      | Agreed things done by script or remote                                | [deferred.md](docs/layers/e-organization-layers/deferred.md)             |
| Stores                        | Stores sell inventory                                                 | [stores](docs/layers/h-selling-layers/stores.md)                         |
| Inventory                     | Items in a store for sale, need not be physical or even real          | [inventory](docs/layers/h-selling-layers/inventory.md)                   |
| Memberships                   | Sell or subscription for membership in a group                        | [memberships](docs/layers/h-selling-layers/memberships.md)               |
| Promotions                    | Sets up advertising, monitors impressions                             | [promotions](docs/layers/i-promotion-layers/promotions.md)               |
| Selling                       | Sets up a sales flow that tracks different events in a sale           | [selling](docs/layers/h-selling-layers/selling.md)                       |
| Admin                         | Fixes broken stuff, sets up moderators, user management               | [admin](docs/layers/b-user-layers/admin-base.md)                         |
| Moderator                     | Moderate some assigned events, locations, changes                     | [moderators](docs/layers/e-organization-layers/moderators.md)            |
| Boards                        | Discussion chat rooms and reviews. Private individual and group chats | [boards](docs/layers/f-interaction-layers/boards.md)                     |
| Notes                         | Organize text,images, links, lists                                    | [notes](docs/layers/c-personal-layers/notes.md)                          |
| Items                         | Allow sharing and communities                                         | [items](docs/layers/f-interaction-layers/items.md)                       |
| Movement                      | Tokens move around connected sets                                     | [movement](docs/layers/f-interaction-layers/movement.md)                 |
| Public grants                 | Allow some users to do some low level operations                      | [public-grants](docs/layers/b-user-layers/public-grants.md)              |
| Format                        | Converts token sets to different things: html and markup ..           | [format](docs/layers/c-personal-layers/format.md)                        |
| Agents                        | Agents are authorized to do things outside the server                 | [agents](docs/layers/b-user-layers/agents.md)                            |
| Jobs                          | Aid to the jobs in the queue, track job output and give notice        | [jobs](docs/layers/a-core-layers/jobs.md)                                |
| User Proxy                    | Internal api to allow one user to do things as another user           | [user-proxy.md](docs/layers/b-user-layers/user-proxy.md)                 |
| Goals                         | Get resources for achievements                                        | [goals](docs/layers/m-eco-layers/goals.md)                               |
| Tech trees                    | Figure things out, and get rewards                                    | [tech-trees](docs/layers/m-eco-layers/tech-trees.md)                     |
| Rates                         | how api limits are enforced                                           | [rates](docs/layers/a-core-layers/rates.md)                              |
| Conversions                   | Convert data to shapes and sets                                       | [conversions](docs/layers/m-eco-layers/conversions.md)                   |

# Concepts

* [Environment](docs/concepts/environment.md)
* [Money](docs/concepts/real_money.md)
* [Shipping](docs/concepts/shopping.md)
* [Interfaces](docs/concepts/interfaces.md)
* [Data Flow](docs/concepts/data-flow.md)
* [Instances](docs/concepts/instances.md)
* [Coding with tokens](docs/concepts/coding-with-tokens.md)


# Calender

| Event                              | Date         |                                                                                                                                                               |
|------------------------------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Project first started              | Oct 8, 2023  | While this is a repeated attempt, started from scratch . First commit made                                                                                    |
| Core api first planning version    | Oct 30, 2023 | Wrote out in md files each api call, method and a rough idea of expected args and behavior                                                                    |
| Layers, extension, changes to core | Nov 20, 2023 | Semi stable plans for all layers in the first version. Some ideas for the core are in extensions. Core updated to be able to do plans in layers and extensions |


# Future Milestones

* (currently working on this) List all the api calls done in each layer, with at least a rough description. Layers can still be altered at this stage. Core can still have tweaks.
* Fill in the description of all the layer api calls, and list all the core api used in those layers
* Define input and output data structures in all the layer api
* Write open api specs for the core
* Write open api specs for the layers and extensions
* Code the core
* Code the testing and tutorial and experimental environment for the core
* Build the layers in group order



* [my-notes](notes/my-notes.md)


