# Users

user and groups api defined at [users.yaml](../../../api-docs/users.yaml)


Users can authenticate via basic authentication in the api call header, or by bearer token created.
Many bearer tokens can be created, and then destroyed.

Passwords can be changed but only if the user is using a token or basic auth (so no lost pw recovery, the registration layer can handle that)

There is an admin layer to reset passwords and tokens see [admin-api.md](admin-api.md)

Once created, there is no editing the basic user object. Attributes for the user, and changes to the user groups is done by other api

## Users operations

| Method | Path                 | Route Name           | Operation                 | Description                                         | Args                 | Notes |
|--------|----------------------|----------------------|---------------------------|-----------------------------------------------------|----------------------|-------|
| Post   | user/register        | user.create          | Create User               | Makes a new user                                    | username,password    |       |
| Put    | user/change_password | user.change_password | Changes the user password | Changes the password for the authenticated user     | password, confirm pw |       |
| Post   | user/create_token    | user.create_token    | Make/return a user token  | makes a new bearer token for the authenticated user |                      |       |
| Delete | user/destroy_token   | user.destroy_token   | Remove the user token     | Deletes the bearer token  (must belong to the user) | token                |       |
| Get    | user/:id             | user.read            | Read User                 | Shows the user information                          |                      |       |

### User Data returned in the user.create or user.read

    id: number
    guid: string
    user_token_type: string-guid / the base token type for this user
    token: string-guid / the token representing the user
    group: string-guid / the token representing the group
    group_token_type: string-guid / the base token type for this group