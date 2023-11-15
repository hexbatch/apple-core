# Apple core version 1

This is an api for a set of ideas. 

* There is an inner core that provides the general logic for the rest of the layers
* There is a layer of services that defines some interaction and introduces concepts
* The services are shown in a presentation and ui layer

This set of documentation describes the first two layers. It does not try to make any web pages or gui, but some services will generate html.

The central idea is the core, this does all the heavy lifting for the common concepts.
And then there are a set of layers, microservices, which use the core, to help expand the concepts

Each part can run on different machines. But it's planned to use kubernetes to have them together with fast networking and scaling.

The apis share some [general-api-usage](docs/core/core-api-general/general-api-usage.md)

# The core

The Core deals with the basic data types described in [core-overview.md](docs/core/core-overview.md).

The core api list is at [core-api-list.md](docs/core/core-api-list.md)

The core api will have a full testing coverage and suit. 

See [core-development-overview.md](dev/core-development-overview.md)

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

| Layer                         | Description                                                           | Link                                                                                      |
|-------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| Instance                      | About the instance the api is running on                              | [instance](docs/layers/a-core-layers/instance.md)                                         |
| Users                         | Manages existing users (non admin)                                    | [users](docs/layers/a-core-layers/users.md)                                               |
| User Groups                   | Do stuff with user groups                                             | [users groups](docs/layers/a-core-layers/user-groups.md)                                               |
| Sessions                      | Provides sessions to interact with the core                           | [sessions](docs/layers/a-core-layers/sessions.md)                                         |
| Registrations                 | Does all the new user account creation                                | [registrations](docs/layers/a-core-layers/registrations.md)                               |
| Authentication and Logging in | Handles users logging in and pw resets                                | [user_login](docs/layers/a-core-layers/user_login.md)                                     |
| Networks                      | Tracks social accounts that are not users, and then later are         | [networks](docs/layers/g-network-layer/networks.md)                                       |
| Network discovery             | Makes new network entry tokens. Scans social networks.                | [network-discovery](docs/layers/i-promotion-layers/network-discovery.md)                  |
| Distributions                 | Gives new and existing tokens to users and people in networks         | [distributions](docs/layers/i-promotion-layers/distributions.md)                          |
| Contracts                     | Terms of using someone's token in your own stuff. Auto payments       | [contracts](docs/layers/f-trading-layers/contracts.md)                                    |
| Marketplace                   | Ownerships of token sets can be bought and sold                       | [marketplace](docs/layers/f-trading-layers/marketplace.md)                                |
| Pools                         | Pools are a resource that generates future tokens                     | [pools](docs/layers/d-organization-layers/pools.md)                                       |
| Organizations                 | They are companies or people who do stores                            | [organizations](docs/layers/d-organization-layers/organizations.md)                       |
| Agreements                    | Reach consensus to do group driven actions                            | [agreements](docs/layers/d-organization-layers/agreements.md)                             |
| Transactions                  | Changes ownership of tokens after an agreement                        | [transactions.md](docs/layers/d-organization-layers/transactions.md)                      |
| Deferred                      | Agreed things done by script or remote                                | [deferred.md](docs/layers/d-organization-layers/deferred.md)                              |
| Stores                        | Stores sell inventory                                                 | [stores](docs/layers/h-selling-layers/stores.md)                                          |
| Inventory                     | Items in a store for sale, need not be physical or even real          | [inventory](docs/layers/h-selling-layers/inventory.md)                                    |
| Promotions                    | Sets up advertising, monitors impressions                             | [promotions](docs/layers/i-promotion-layers/promotions.md)                                |
| Selling                       | Sets up a sales flow that tracks different events in a sale           | [selling](docs/layers/h-selling-layers/selling.md)                                        |
| Watchers                      | Trigger events when some condition is reached with tokens and sets    | [Watchers](docs/layers/b-user-layers/watcher.md)                                          |
| Admin                         | Fixes broken stuff, sets up moderators, user management               | [admin](docs/layers/b-user-layers/admin-base.md)                                          |
| Moderator                     | Moderate some assigned events, locations, changes                     | [moderators](docs/layers/d-organization-layers/moderators.md)                             |
| Boards                        | Discussion chat rooms and reviews. Private individual and group chats | [boards](docs/layers/e-interaction-layers/boards.md)                                      |
| Notes                         | Organize text,images, links, lists                                    | [notes](docs/layers/c-personal-layers/notes.md)                                           |
| Items                         | Allow sharing and communities                                         | [items](docs/layers/e-interaction-layers/items.md)                                        |
| Movement                      | Tokens move around connected sets                                     | [movement](docs/layers/e-interaction-layers/movement.md)                                  |
| Public grants                 | Allow some users to do some low level operations                      | [public-grants](docs/layers/b-user-layers/public-grants.md)                               |
| Format                        | Converts token sets to different things: html and markup ..           | [format](docs/layers/c-personal-layers/format.md)                                         |
| Export and Verification       | How tokens are shared between servers                                 | [export import verification](docs/layers/j-internet-layers/export-import-verification.md) |
| Agents                        | Agents are authorized to do things outside the server                 | [agents](docs/layers/b-user-layers/agents.md)                                             |
| Jobs                          | Aid to the jobs in the queue, track job output and give notice        | [jobs](docs/layers/a-core-layers/jobs.md)                                                 |
| User Proxy                    | Internal api to allow one user to do things as another user           | [user-proxy.md](docs/layers/b-user-layers/user-proxy.md)                                  |
| Shapes                        | Sets can have 3d shapes, intersect each other and move                | [shapes](docs/layers/k-representation-layers/shapes.md)                                   |
| Audio                         | Sets can make sounds                                                  | [audio](docs/layers/k-representation-layers/audio.md)                                     |
| Avatars                       | Sets can be animated by outside programs                              | [set-avatar](docs/layers/k-representation-layers/set-avatar.md)                           |
| Mutual Editor                 | View and edit mutual relations                                        | [mutual-editor](docs/layers/k-representation-layers/mutual-editor.md)                     |
| Goals                         | Get resources for achievements                                        | [goals](docs/layers/m-eco-layers/goals.md)                                                |
| Tech trees                    | Figure things out, and get rewards                                    | [tech-trees](docs/layers/m-eco-layers/tech-trees.md)                                      |
| Rates                         | how api limits are enforced                                           | [rates](docs/layers/a-core-layers/rates.md)                                                |
| Conversions                   | Convert data to shapes and sets                                       | [conversions](docs/layers/m-eco-layers/conversions.md)                                    |
| Eco                           | Plants and animals                                                    | [eco](docs/layers/m-eco-layers/eco.md)                                                    |

# Concepts

* [Environment](docs/concepts/environment.md)
* [Money](docs/concepts/real_money.md)
* [Shipping](docs/concepts/shopping.md)
* [Interfaces](docs/concepts/interfaces.md)
* [Data Flow](docs/concepts/data-flow.md)
* [Instances](docs/concepts/instances.md)
* [Coding with tokens](docs/concepts/coding-with-tokens.md)


# Calender

| Event                           | Date         |                                                                                            |
|---------------------------------|--------------|--------------------------------------------------------------------------------------------|
| Project first started           | Oct 8, 2023  | While this is a repeated attempt, started from scratch                                     |
| Core api first planning version | Oct 30, 2023 | Wrote out in md files each api call, method and a rough idea of expected args and behavior |


# Timeline

## Timeline for finishing the first version of the open source here

| Event                                                                            | Expected Date   |                                                                                       |
|----------------------------------------------------------------------------------|-----------------|---------------------------------------------------------------------------------------|
| Complete planning of all layer api                                               | Feb 15, 2024    | Map out api and high level logic for 27 microservices                                 |
| Write api definitions for core and layers in open api format                     | March 30, 2024  | All api fully documented in the open api specifications                               |
| Finish writing core library first version                                        | August 30, 2024 | Fully working core according to spec. Updated layer api changes                       |
| Write javascript playground and test and refine core, making core second version | Oct 30, 2024    | More documentation, able to play with core in graphical way. Updated layers as needed |
| Write and test core layers                                                       | Dec 21, 2024    | Starting to go through the layer implementations                                      |
| Write and test user layers                                                       | Jan 21, 2025    |                                                                                       |
| Write and test personal layers                                                   | Feb 21, 2025    |                                                                                       |
| Write and test organization layers                                               | March 21, 2025  |                                                                                       |
| Write and test interaction layers                                                | April 21, 2025  |                                                                                       |
| Write and test trading layers                                                    | May 21, 2025    |                                                                                       |
| Write and test network layers                                                    | June 21, 2025   |                                                                                       |
| Write and test selling layers                                                    | July 21, 2025   |                                                                                       |
| Write and test promotion layers                                                  | Aug 21, 2025    |                                                                                       |
| Write and test internet layers                                                   | Sep 21, 2025    |                                                                                       |



## Timeline for finishing the closed source delivery and selling service based on the open source

| Event                                            | Expected Date   |                                                                                         |
|--------------------------------------------------|-----------------|-----------------------------------------------------------------------------------------|
| Write out requirements, high level part planning | Jan 15, 2026    | Start to plan details of what is needed, and what things will be used in the deliveries |
| Have working delivery service                    | August 15, 2026 | Start to plan details of what is needed, and what things will be used in the deliveries |
| Be my own first test delivery person             | Sept 15, 2026   | Test in selected area                                                                   |


* [my-notes](notes/my-notes.md)


