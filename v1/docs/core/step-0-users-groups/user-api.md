# Users

user and groups api defined at [users.yaml](../../../api-docs/users.yaml)


Users authenticate via bearer token created. Many bearer tokens can be created, and then destroyed. Its possible to destroy all tokens and lock out the user.


There is an admin layer to list users and reset tokens see [admin-api.md](admin-api.md)

Once created, there is no editing the basic user object. Attributes for the user, and changes to the user groups is done by other api.

Anyone can read the user info. All api must be using the token except for the register call.
Some attributes, and even some standard definition attributes will be marked as readable by user or his admin group only.

## Users operations

| Method | Path                   | Route Name                  | Description                                         | Args                                  | Notes                             |
|--------|------------------------|-----------------------------|-----------------------------------------------------|---------------------------------------|-----------------------------------|
| Post   | user/register          | core.user.register          | Makes a new user                                    | username (must be unique)             | returns a bearer token            |
| Post   | user/auth/create       | core.user.auth.create       | makes a new bearer token for the authenticated user | optional pass through data to store   |                                   |
| Get    | user/auth/pass_through | core.user.auth.pass_through | gets associated data in the token                   |                                       | uses the log in token to get data |
| Delete | user/auth/delete       | core.user.auth.destroy      | Deletes the token being used in this call           |                                       | cannot delete last token          |
| Get    | user/:id               | core.user.read              | Shows the user information                          | optional wide flag to show attributes |                                   |

### User Data returned in the user.create or user.read

    id: number
    guid: string 
    user_token_type: string-guid / the base token type for this user
    token: string-guid / the token representing the user
    group: string-guid / the token representing the group
    group_token_type: string-guid / the base token type for this group
    attributes:[] --empty unless wide

When the wide flag is used in the read, then it will be a list of attribute name: attribute value

When the editable flag is used, only the attributes that are editable, via permissions of the calling user, will be returned