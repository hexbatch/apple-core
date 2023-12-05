# Admin api

Done via command (task to run on the command line)

## User operations

| Task             | todo | Operation                                         | Args                                                           |
|------------------|------|---------------------------------------------------|----------------------------------------------------------------|
| create_user_auth |      | Makes/returns new token for a given user          | user guid or user token guid, or username. Optional expiration |
| logout_user      |      | Logs a given user out of all tokens               | user guid or user token guid, or username                      |
| delete_user      | *    | Deletes a user if no tokens in anyone else's sets | user guid or user token guid, or username                      |


# todo 
check for tokens and types in other sets