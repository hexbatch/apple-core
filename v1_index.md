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

The apis share some [general-api-usage](core-docs/core-api-general/general-api-usage.md)

# The core

The Core deals with the basic data types described in [core-overview.md](core-docs/core-overview.md).

The core api list is at [core-api-list.md](core-docs/core-api-list.md)

The core api will have a full testing coverage and suit. 

See [core-development-overview.md](other-docs/dev/core-development-overview.md)
Some selected links below cover the main parts, the overview has more

| Concept    | Description                   | Link                                                            |
|------------|-------------------------------|-----------------------------------------------------------------|
| Bounds     | Limits of an element          | [bounds](core-docs/step-1-bounds/bound-overview.md)             |
| Attributes | Data in an element            | [attributes](core-docs/step-2-attributes/attribute-overview.md) |
| Actions    | Event listeners on an element | [actions](core-docs/step-4-actions/action-overview.md)          |
| Types      | A definition of an element    | [types](core-docs/step-5-types/type-overview.md)                |
| Elements   | Definition of an element      | [elements.md](core-docs/step-6-elements/element-overview.md)    |
| Sets       | Elements are put into a set   | [sets](core-docs/step-7-sets/set-overview.md)                   |

## List of expansions in the core

There are some cool stuff that can be done at the core level, that is not universally needed by all operations

| Expansion                        | Description                        | Link                                                             |
|----------------------------------|------------------------------------|------------------------------------------------------------------|
| Overview                         | Intro how these are organized      | [aa-overview.md](core-docs/y-core-expansions/aa-overview.md)     |
| Aggregations                     | Reduce values in sets              | [aggregations.md](core-docs/y-core-expansions/aggregations.md)   |
| Iterations                       | Organize successive api calls      | [iterations.md](core-docs/y-core-expansions/iterations.md)       |
| Push Pop                         | Organize api calls done in batches | [push-pops.md](core-docs/y-core-expansions/push-pops.md)         |
| Dynamic Filters and requirements | Expand the concept of filters      | [filters.md](core-docs/y-core-expansions/dynamic-filters.md)     |
| Same set location searching      | Using shape relations              | [location-searching.md](core-docs/y-core-expansions/location.md) |
| Mutuals                          | Interlinked sets                   | [mutuals.md](core-docs/y-core-expansions/mutuals.md)             |
| Interfaces                       | Higher order data flow             | [interfaces.md](core-docs/y-core-expansions/interfaces.md)       |


# Layers
The layers overview is talked about in [layers overview](layer-docs/layers-overview.md)

The layers each do their own thing, but they have a few things in common.
Most of the heavy lifting in the layer codes will be done by api calls to the core.
They set up jobs to be dispatched and completed later. But often, the caller to these layers will not notice because that is hidden and fast.

The caller can decide how to get the results, he can wait for the api call to return, or he can use a callback url, or do polling later.

The core has its own user and authentication system. The layers use OAuth2 to register and log-in people.
The layers talk to the core by storing core user bearer elements that do not expire, and when they need to do the core to do things,
they dispatch jobs using a temporary auth element that expires at the end of the job.

The core itself does not have a superuser, or root user.
But it does have a permission system. So the layers can be doing actions as different users to implement nested permissions.


When a public api request is made, a job is made that has a list of api core calls to make.

* A temporary bearer element is created for this job only.
* The job is put on a queue.
* When the job is run, the apis are called, using the output of earlier calls to be params for the later calls.
* The job api is updated, the temp bearer element is undone, and job result sent back via a callback url to the layer that created the job.
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




# List of layers

| Group        | Layer                         | Description                                                           | Link                                                               |
|:-------------|-------------------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------|
| Inner        | Instance                      | About the instance the api is running on                              | [instance](layer-docs/a-inner-layers/instance.md)                  |
|              | Jobs                          | Aid to the jobs in the queue, track job output and give notice        | [jobs](layer-docs/a-inner-layers/jobs.md)                          |
|              | Rates                         | how api limits are enforced                                           | [rates](layer-docs/a-inner-layers/rates.md)                        |
|              | Low level                     | Allow some users to do some low level operations                      | [low level](layer-docs/a-inner-layers/low-level-access.md)         |
| User         | Users                         | Manages existing users (non admin)                                    | [users](layer-docs/b-user-layers/users.md)                         |
|              | User Groups                   | Do stuff with user groups                                             | [users groups](layer-docs/b-user-layers/user-groups.md)            |
|              | Sessions                      | Provides sessions to interact with the core                           | [sessions](layer-docs/b-user-layers/sessions.md)                   |
|              | Agents                        | Agents are authorized to do things outside the server                 | [agents](layer-docs/b-user-layers/agents.md)                       |
|              | Registrations                 | Does all the new user account creation                                | [registrations](layer-docs/b-user-layers/registrations.md)         |
|              | Authentication and Logging in | Handles users logging in and pw resets                                | [user_login](layer-docs/b-user-layers/user_login.md)               |
| Personal     | Notes                         | Organize text,images, links, lists                                    | [notes](layer-docs/c-personal-layers/notes.md)                     |
|              | Format                        | Converts element sets to different things: html and markup ..         | [format](layer-docs/c-personal-layers/format.md)                   |
| Connection   | Publishing                    | Api for broadcasting new types and changes in elements                | [publishing](layer-docs/d-connection-layers/publishing.md)         |
|              | Mirroring                     | Updates followed elements and types that are not based here           | [mirroring](layer-docs/d-connection-layers/mirroring.md)           |
|              | External Users                | Coordinates users from other instances here                           | [external-users](layer-docs/d-connection-layers/external-user.md)  |
|              | Pools                         | Pools are a resource that generates future elements                   | [pools](layer-docs/e-organization-layers/pools.md)                 |
| Organization | Organizations                 | They are companies or people who do stores                            | [organizations](layer-docs/e-organization-layers/organizations.md) |
|              | Agreements                    | Reach consensus to do group driven actions                            | [agreements](layer-docs/e-organization-layers/agreements.md)       |
|              | Deferred                      | Agreed things done by script or remote                                | [deferred.md](layer-docs/e-organization-layers/deferred.md)        |
| Transaction  | Transactions                  | Changes ownership of elements after an agreement                      | [transactions.md](layer-docs/f-transactions/transactions.md)       |
|              | Auditing                      | Api for record keeping/verification of transactions                   | [Auditing](layer-docs/f-transactions/auditing.md)                  |
|              | Contracts                     | Terms of using someone's element in your own stuff. Auto payments     | [contracts](layer-docs/f-transactions/contracts.md)                |
| Interaction  | Boards                        | Discussion chat rooms and reviews. Private individual and group chats | [Communication](layer-docs/g-interaction-layers/communication.md)  |
|              | Items                         | Allow sharing and communities                                         | [items](layer-docs/g-interaction-layers/items.md)                  |



# Concepts

* [Environment](other-docs/docs/concepts/environment.md)
* [Shopping](other-docs/docs/concepts/money.md)
* [Interfaces](other-docs/docs/concepts/interfaces.md)
* [Data Flow](other-docs/docs/concepts/data-flow.md)
* [Instances](other-docs/docs/concepts/instances.md)
* [Coding with elements](other-docs/docs/concepts/coding-with-elements.md)


# Calender

| Event                              | Date         |                                                                                                                                                                |
|------------------------------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Project first started              | Oct 8, 2023  | While this is a repeated attempt, started from scratch . First commit made                                                                                     |
| Core api first planning version    | Oct 30, 2023 | Wrote out in md files each api call, method and a rough idea of expected args and behavior                                                                     |
| Layers, extension, changes to core | Nov 20, 2023 | Semi stable plans for all layers in the first version. Some ideas for the core are in extensions. Core updated to be able to do plans in layers and extensions |




* [my-notes](other-docs/notes/my-notes.md)


