# Api docs for Gokabam (iteration apple-core)

This concept has seen several abandoned previous versions. 
This version is named apple core, because it's been eaten at for a while, but has a lot of great seeds that can turn into valuable orchards later

## What is this?

In plain english this is a general approach to sharing information and doing sales between different people. This is designed to work between servers run by different admins.

I plan to use this to do my own sales and services. However, the more people who use this to set up their own stuff, the better off my plans will be. 
So this is why its open source. Also, I have hopes that fresh ideas, and tested concepts and sales by others can be mixed into my own plans. 


## Planned stages of development

This project is still in the most early days. Right now, it's still in the planning.
There is a core api that will power about 20 microservices, listed below. The microservices here are called the layers.

This is how my end of the development here will go

* general wool-gathering: this is where we are at now. Mapping out all the concepts in the docs first. 
  * Not only will the low-lying logic of the core be done here, but the higher level logic of the layers too.
  * Low level logic here means how the primitives are expected to act, and not the implementation logic.
* Once the docs has a solid go, the api-docs will be filled in and will describe all the data structures and operations
* Implement and test the core api.
  * The core api will have a full testing coverage and suit

Each layer has its own iteration of writing the api and code. 


## The core 

The Core deals with the basic data types described in [core-overview.md](v1/docs/core-overview.md).

## Layers
The layers overview is talked about in [next-layer.txt](v1/docs/layers-overview.md)

The layers each do their own thing, but they set up jobs to be dispatched and completed, with callback urls registered by the caller, or they can do polling.

Most of the heavy lifting in the layer codes will be done by api calls to the core.

The layer framework will be storing user bearer tokens that do not expire, and they use those to create temporary token for the core to do stuff for the user.

Each api, including the core, can be different instances, containers or pods. The jobs can be executed via other things.
This allows horizontal scaling. The different api can also run in one machine, to allow testing by development

General api call in the layer:
    
    public -> outer layers -> job queue -> inner core -> callback to public or a reference they can get the data later
 

| Layer                   | Description                                                    |
|-------------------------|----------------------------------------------------------------|
| Users                   | Managers existing users; creates and changes user groups       |
| Registrations           | Does all the new user account creation                         |
| Sets                    | Create and edit token sets                                     |
| Networks                | Tracks social accounts that are not users, and then later are  |
| Distributions           | Gives new and existing tokens to people in networks            |
| Contracts               | Deals with the selling, terms, and use of token types          |
| Marketplace             | Ownerships of token sets can be bought and sold                |
| Trends                  | Public read only list of token types bought, sold,contracted   |
| Organizations           | They are companies or people who do stores                     |
| Stores                  | Stores sell inventory                                          |
| Inventory               | Items in a store for sale, need not be physical or even real   |
| Promotions              | Sets up advertising, monitors impressions                      |
| Selling                 | Sets up a sales flow that tracks different events in a sale    |
| Agents                  | Agents are those that agree to do things outside the server    |
| Admin                   | Fixes broken stuff, sets up moderators, user management        |
| Moderator               | Moderate some assigned events, locations, changes              |
| Boards                  | Discussion chat rooms and reviews                              |
| Export and Verification | How tokens are shared between servers                          |
| Token                   | High level token management by users                           |
| Jobs                    | Aid to the jobs in the queue, track job output and give notice |

## Api Pages

* [core-overview.md](v1/docs/core-overview.md)
* [core-overview.md](v1/docs/layers-overview.md)
* [user-overview.md](v1/docs/user-overview.md)


# Notes

* [my-notes.md](v1/docs/notes/my-notes.md)
