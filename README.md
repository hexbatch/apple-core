# api start for Gokabam (iteration apple-core)

This concept has seen several abandoned previous versions. This version is named apple core, for reasons only known by me :-)

## Planned stages of development

* general wool-gathering: this is where we are at now. Mapping out all the concepts in the docs first. Not only will the low-lying logic be done here, but the higher level logic too.
    Low level logic here means how the primitives are expected to act, and not the implementation logic.
* Once the docs has a solid go, the api-docs will be filled in and will describe all the data structures and operations
* Implement the api.

The api has several different layers. Each layer has its own iteration of writing the api and code. 

The first layer is the one that deals with the basic data types described in [core-overview.md](v1/docs/core-overview.md).
This will be coded and tested, then only after that will be the next layer of api stuff talked about in [next-layer.txt](v1/docs/next-layer.md) 

## Api Pages

* [core-overview.md](v1/docs/core-overview.md)
* [user-overview.md](v1/docs/user-overview.md)


# notes:

## Implementation

### Next Layer authentication with the inner core

The outer layers uses Oauth, but they have to log in with the inner core via the job queues.

The outer layers have non expiring bearer token for each user, and there is an admin api that allows these token to be regenerated.

When another user, who is allowed via Oauth roles to act on behalf of a user, makes a call for this user, then when the roles are verified for the logged-in user,
the outer layer will construct the job queue using the behalf-user's token.

### Job Queues 

Because there is reliance for executed javascript, as well as some db intensive operations. 
Then some operations, if not all, should be done by a job queue, and the api caller should get back a callback reference 
and if the api caller provides a url, or another form of callback, then the api will let them know when its done.

The core api does not do callback, but the next layer api will, and what the layers will do is set up some nested operations into a job queue.
The operations will have ties so that they are done in order, and the needed values from the yet to be executed ops are fed into the ops waiting for them.
For example, when making a new token, then doing something with it, like putting it into a set.

So the job data should have both the user that is logged in at the time, and the operations are done in the context of that user.
This implies that the user should have a token to be used, when calling the core api. And the token should expire at the end of the job.
This means that the core api should use Bearer tokens, and have the api to revoke it


* see https://swagger.io/docs/specification/authentication/bearer-authentication/
* https://laravel.com/docs/10.x/sanctum#api-token-authentication

## General notes

These are notes used by myself for reference


OpenAPI (OAS3/Swagger) definition for GeoJSON objects
* https://gist.github.com/zit0un/3ac0575eb0f3aabdc645c3faad47ab4a
* 
* https://swagger.io/specification/
* https://swagger.io/docs/specification/data-models/data-types/
* https://stackoverflow.com/questions/14203122/create-a-regular-expression-for-cron-statement


older notes:

* https://docs.google.com/document/d/1S1C40nuKbKuJ89IEOLbtQLDoMeJYNs8SodILw4kkEew/edit  (older db flow)
* https://drive.google.com/file/d/1x8__LPRIFcZANSuzXwrpj7preNuAjnva/view (object flow)
* https://docs.google.com/document/d/1sePxG0G4MMc9klXVdCkaTg2xL8EaiuOAgOaFZHSx90I/edit ( sales flow)
* https://docs.google.com/document/d/1Y-5dHE-WBCT3690wuIXeiJdfwg_gwFJHYzsCmCS2PJk/edit (koin flow)
* https://docs.google.com/document/d/1yLjXhNiCytMGQhlJucBByoKr9wvyubSAQY8CGVdl4Vg/edit (owner flow)
* https://drive.google.com/file/d/1D0L1i27KxRQ8MdiGKMuF77bVqfmc_MHf/view (bucket flow)
* https://drive.google.com/file/d/1kkCQYU41DBzQtrASMFX0HXspUnYu5k7J/view (company flow)
* 
* https://davidgarcia.dev/posts/how-to-split-open-api-spec-into-multiple-files/
* https://github.com/dgarcia360/openapi-boilerplate





