# Set api


Sets are owned by the owner of the token defining it, and have an optional requirement,
an optional parent, and optional links. 

Tokens can be added or removed. There are also set operations, see the set operation api list.

The defining token cannot be swapped out in a set. The defining token can only handle one set at a time. The defining token can itself do anything other tokens can, 
and belong in unlimited other sets.

If a set as a type, that type cannot be changed if the set has any contents.

Otherwise, the set can be edited at any time, and deleted at any time

If a user can read the defining token, then the set contents can be read, and used in set operations as a read source.
If a user can write to the defining token, then the set contents can be altered.

A writing to the defining token ability is needed to change set relationships.

The id of the set is unique each time the token is used to make a set. A token can have only one current set, but have a history of different sets


| Method | Path                                 | Route Name | Operation                                          | Args                                                  |
|--------|--------------------------------------|------------|----------------------------------------------------|-------------------------------------------------------|
| Post   | set                                  |            | Creates a set                                      | Token, and optional type, parent, links               |
| Put    | set/:id/edit/type/:id                |            | Add a requirement, change a requirement, or remove | the requirement id, or null (to remove)               |
| Put    | set/:id/relationship/parent/:id      |            | Add or remove a parent                             | Change the parent by giving id, or remove any by null |
| Put    | set/:id/relationship/link/:id/add    |            | Add a link                                         | the set to link to                                    |
| Delete | set/:id/relationship/link/:id/remove |            | Remove a link                                      | the set that is already linked to                     |
| Delete | set/:id                              |            | Deletes the set                                    | the set id to delete                                  |
| put    | set/:id/truncate                     |            | Removes all the tokens in the set                  |                                                       |
| post   | set:id/tokens/add                    |            | Adds one or more tokens to the set                 | ids of tokens                                         |
| Delete | set:id/tokens/remove                 |            | Removes one or more tokens from the set            | ids of tokens                                         |
| GET    | set:id/list                          |            | lists the tokens in a set                          | iterator,optional requirements filter                 |
| GET    | sets/list                            |            | lists the sets owned by the user                   | iterator,optional filters                             |


    id: the id of the set
    token: Every set has a token to define it, which adds ways to describe the set, search for it in path operations, or give it some location and time
    tokens: []
    parent-token-set: (optional) may have a parent, used for organizing token sets. (cannot be cyclic)
    linked-sets: (optional) may have links to other sets (can be cyclic so two sets can link to each other)
    requirement: id (optional), if there are max and min requirements, or not, this types the set and filters tokens
    location_checks: true or false


Deleting a set does not change any tokens in the set, nor is any actions run on the tokens in the set when the set is deleted

listing sets, without filters, will show all sets the user can write to and alter 
other filters: by set definition token type, or its attributes. use the search api for set contents