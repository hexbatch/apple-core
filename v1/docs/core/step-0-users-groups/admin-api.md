# Admin api

Done via command (task to run on the command line)

## User operations

| Task             | Operation                                | Args                                          |
|------------------|------------------------------------------|-----------------------------------------------|
| create_user_auth | Makes/returns new token for a given user | user id, or username with optional expiration |
| logout_user      | Logs a given user out of all tokens      | user id, or username                          |

