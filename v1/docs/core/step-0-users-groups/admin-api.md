# Admin api

can only be used on localhost, or a list of ips defined in the .env ,  or via command (task to run on the command line)

## Users operations

| Method | Path                              | Route Name                        | Operation                                   | Args                            | Notes |
|--------|-----------------------------------|-----------------------------------|---------------------------------------------|---------------------------------|-------|
| delete | admin/users/destroy_tokens        | admin.users.destroy_tokens        | Revokes all tokens for the given users      | user id or guids to do this for |       |
| post   | admin/users/create_tokens         | admin.users.create_tokens         | Makes/returns new token for each given user | user id or guids to do this for |       |
| get    | admin/users/list                  | admin.users.list_users            | Returns user info in pages, can filter      | iterator, optional search path  |       |
| patch  | admin/system_groups/add_member    | admin.system_groups.add_member    | Adds a user to a system group               | user id                         |       |
| patch  | admin/system_groups/add_admin     | admin.system_groups.add_admin     | Adds an admin to a system group             | user id                         |       |
| delete | admin/system_groups/remove_member | admin.system_groups.remove_member | removes a user from a system group          | user id                         |       |   
| delete | admin/system_groups/remove_admin  | admin.system_groups.remove_admin  | removes an admin from a system group        | user id                         |       |
| delete | admin/tokens/gc                   | admin.tokens.garbage_collection   | removes expired tokens                      | time to run or number tokens    |       |


Standard system groups: membership
* script_permission , allows a user to create scripts
* remote_permission , allows a user to create remotes

Standard system groups: admin
* script_permission , can list scripts and see details, turn on and off scripts
* remote_permission , can list and search for remotes and see details, turn on and off remotes


## admin.users.list_users
options to search also token pass-through data, if given something will see if any token info matches a user