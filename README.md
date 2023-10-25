# Api docs for Gokabam (iteration apple-core)

This concept has seen several abandoned previous versions. 
This version is named apple core, because it's been eaten at for a while, but has a lot of great seeds that can turn into valuable orchards later

## What is this?

In plain english this is a general approach to sharing information and doing sales between different people. This is designed to work between servers run by different admins.

I plan to use this to do my own sales and services. However, the more people who use this to set up their own stuff, the better off my plans will be. 
So this is why its open source. Also, I have hopes that fresh ideas, and tested concepts and sales by others can be mixed into my own plans. 


## Planned stages of development

This project is still in the most early days. Right now, it's still in the planning.
There is a core api that will power 25 microservices, listed below. The microservices here are called the layers.

This is how my end of the development here will go

* general wool-gathering: this is where we are at now. Mapping out all the concepts in the docs first. 
  * Not only will the low-lying logic of the core be done here, but the higher level logic of the layers too.
  * Low level logic here means how the primitives are expected to act, and not the implementation logic.
* Once the docs has a solid go, the api-docs will be filled in and will describe all the data structures and operations
* Implement and test the core api.
  * The core api will have a full testing coverage and suit
  * See [core-development-overview.md](v1/dev/core-development-overview.md)

### Order of writing layers

Each layer has its own iteration of writing the api and code. 

[order-writing-layers.md](v1/docs/layers/order-writing-layers.md)


# The core 

The Core deals with the basic data types described in [core-overview.md](v1/docs/core/core-overview.md).

The api list is at [core-api-list.md](v1/docs/core/core-api-list.md)

# Layers
The layers overview is talked about in [layers overview](v1/docs/layers/layers-overview.md)

The layers each do their own thing, but they set up jobs to be dispatched and completed, with callback urls registered by the caller, or they can do polling.

Most of the heavy lifting in the layer codes will be done by api calls to the core.

The layer framework will be storing user bearer tokens that do not expire, and they use those to create a temporary token in each api call.
The core itself does not have a superuser, or root user. But it does have a permission system. So the layers doing actions as different users for a single call takes care of the nested permissions.


When a public api request is made, a job (a class instance) is made that has a list of api calls to make.
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
 

| Layer                         | Description                                                           | Link                                                                       |
|-------------------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------|
| Instance                      | About the instance the api is running on                              | [instance](v1/docs/layers/instance.md)                                     |
| Users                         | Managers existing users; creates and changes user groups              | [users](v1/docs/layers/users.md)                                           |
| Registrations                 | Does all the new user account creation                                | [registrations](v1/docs/layers/registrations.md)                           |
| Authentication and Logging in | Handles users logging in and pw resets                                | [user_login](v1/docs/layers/user_login.md)                                 |
| Networks                      | Tracks social accounts that are not users, and then later are         | [networks](v1/docs/layers/networks.md)                                     |
| Network discovery             | Makes new network entry tokens. Scans social networks.                | [network-disovery](v1/docs/layers/network-disovery.md)                     |
| Distributions                 | Gives new and existing tokens to users and people in networks         | [distributions](v1/docs/layers/distributions.md)                           |
| Contracts                     | Terms of using someone's token in your own stuff. Auto payments       | [contracts](v1/docs/layers/contracts.md)                                   |
| Marketplace                   | Ownerships of token sets can be bought and sold                       | [marketplace](v1/docs/layers/marketplace.md)                               |
| Pools                         | Pools are a resource that generates future tokens                     | [pools](v1/docs/layers/pools.md)                                           |
| Organizations                 | They are companies or people who do stores                            | [organizations](v1/docs/layers/organizations.md)                           |
| Stores                        | Stores sell inventory                                                 | [stores](v1/docs/layers/stores.md)                                         |
| Inventory                     | Items in a store for sale, need not be physical or even real          | [inventory](v1/docs/layers/inventory.md)                                   |
| Promotions                    | Sets up advertising, monitors impressions                             | [promotions](v1/docs/layers/promotions.md)                                 |
| Selling                       | Sets up a sales flow that tracks different events in a sale           | [selling](v1/docs/layers/selling.md)                                       |
| Watchers                      | Trigger events when some condition is reached with tokens and sets    | [Watchers](v1/docs/layers/watcher.md)                                      |
| Admin                         | Fixes broken stuff, sets up moderators, user management               | [admin](v1/docs/layers/admin.md)                                           |
| Moderator                     | Moderate some assigned events, locations, changes                     | [moderators](v1/docs/layers/moderators.md)                                 |
| Boards                        | Discussion chat rooms and reviews. Private individual and group chats | [boards](v1/docs/layers/boards.md)                                         |
| Notes                         | Organize text,images, links, lists                                    | [notes](v1/docs/layers/notes.md)                                           |
| Items                         | Allow sharing and communities                                         | [items](v1/docs/layers/items.md)                                           |
| Public grants                 | Allow some users to do some low level operations                      | [public-grants](v1/docs/layers/public-grants.md)                           |
| Format                        | Converts token sets to different things: html and markup ..           | [format](v1/docs/layers/format.md)                                         |
| Export and Verification       | How tokens are shared between servers                                 | [export import verification](v1/docs/layers/export-import-verification.md) |
| Agents                        | Agents are authorized to do things outside the server                 | [agents](v1/docs/layers/agents.md)                                         |
| Jobs                          | Aid to the jobs in the queue, track job output and give notice        | [jobs](v1/docs/layers/jobs.md)                                             |

# Concepts

* [Environment](v1/docs/concepts/environment.md)
* [Money](v1/docs/concepts/real_money.md)
* [Shipping](v1/docs/concepts/shopping.md)
* [Interfaces](v1/docs/concepts/interfaces.md)
* [Data Flow](v1/docs/concepts/data-flow.md)
* [Instances](v1/docs/concepts/instances.md)
* [Coding with tokens](v1/docs/concepts/coding-with-tokens.md)

# Notes

* [my-notes](notes/my-notes.md)
