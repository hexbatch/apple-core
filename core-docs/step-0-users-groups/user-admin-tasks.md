# Admin api

Done via command (task to run on the command line)

## User operations

| Task             | todo | Operation                                           | Args                                                             |
|------------------|------|-----------------------------------------------------|------------------------------------------------------------------|
| create_user_auth |      | Makes/returns new token for a given user            | user guid or user element guid, or username. Optional expiration |
| logout_user      |      | Logs a given user out of all tokens                 | user guid or user element guid, or username                      |
| delete_user      | *    | Deletes a user if no elements in anyone else's sets | user guid or user element guid, or username                      |
| flag             | *    | flags a user                                        | see below                                                        |
| unflag           | *    | unflags a user                                      | see below                                                        |
| list_flags       | *    | shows who has what flag                             | can filter by flag type                                          |


# todo 
* delete_user : check for elements and types in other sets
* flag, unflag, list_flags : implement




# flagging users
adds|removes a system attribute to mark users for system stuff:
* remote_types: allow them to add sensitive remotes like command and socket remotes
* remote_activity: allow them to see all remote activity
* user_read: allows to see all a user's attributes
