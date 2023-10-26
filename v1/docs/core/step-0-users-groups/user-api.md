# Users

user and groups api defined at [users.yaml](../../../api-docs/users.yaml)


Users authenticate via bearer token created. Many bearer tokens can be created, and then destroyed. Its possible to destroy all tokens and lock out the user.


There is an admin layer to list users and reset tokens see [admin-api.md](admin-api.md)

Once created, there is no editing the basic user object. Attributes for the user, and changes to the user groups is done by other api.

Anyone can read the user info. All api must be using the token except for the register call

## Users operations

| Method | Path                      | Route Name           | Operation                 | Description                                         | Args                                                       | Notes                  |
|--------|---------------------------|----------------------|---------------------------|-----------------------------------------------------|------------------------------------------------------------|------------------------|
| Post   | user/register/{lang-code} | user.create          | Create User               | Makes a new user, puts the username in the aliases  | username (must be unique)                                  | returns a bearer token |
| Post   | user/create_token         | user.create_token    | Make/return a user token  | makes a new bearer token for the authenticated user |                                                            |                        |
| Delete | user/destroy_token        | user.destroy_token   | Remove the user token     | Deletes the bearer token  (must belong to the user) | token                                                      |                        |
| Get    | user/:id                  | user.read            | Read User                 | Shows the user information                          | optional wide flag to show standard attributes of the user |                        |

### User Data returned in the user.create or user.read

    id: number
    guid: string
    user_token_type: string-guid / the base token type for this user
    token: string-guid / the token representing the user
    group: string-guid / the token representing the group
    group_token_type: string-guid / the base token type for this group