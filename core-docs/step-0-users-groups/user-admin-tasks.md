# Admin api

Done via command (task to run on the command line)

## User operations

| Task             | todo | Operation                                           | Args                                                             |
|------------------|------|-----------------------------------------------------|------------------------------------------------------------------|
| create_user_auth |      | Makes/returns new token for a given user            | user guid or user element guid, or username. Optional expiration |
| logout_user      |      | Logs a given user out of all tokens                 | user guid or user element guid, or username                      |
| delete_user      | *    | Deletes a user if no elements in anyone else's sets | user guid or user element guid, or username                      |
| list_users       | *    | paginates users                                     | see below                                                        |
| flag             | *    | flags a user                                        | see below                                                        |
| unflag           | *    | unflags a user                                      | see below                                                        |


# todo 
* delete_user : check for elements and types in other sets
* list_users : implement

## listing users
option to sort (by when created or by username)
option to filter: (by start of username or flag status)
option to page: (next, prev, start, default start)

## info shown
* shows basic user info, but can use the wide flag to show extended info from the element attributes
* can show stats (how many resources of each type made)


# flagging users
adds|removes a system attribute to mark users for system stuff:
* allow them to add sensitive remotes like command and socket remotes
* allow them to see all remote activity
