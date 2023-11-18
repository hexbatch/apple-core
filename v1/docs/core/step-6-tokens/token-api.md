# Tokens


| Method | Path                           | Route Name | Description                                                |
|--------|--------------------------------|------------|------------------------------------------------------------|
| Post   | token                          |            | Makes a new token from a token type, optional set to place |
| Patch  | token/:id                      |            | Sparse edit a token (but not its attributes or state       |
| Patch  | token/:id/states               |            | Sparse edit the states of a token                          |
| Patch  | token/:id/edit_attribute/:id   |            | Edit a live attribute value, or turn it off or on          |
| Patch  | token/:id/turn_attribute/:id   |            | turn attribute off or on                                   |
| Patch  | token/:id/turn_parent/:id      |            | Turn parent off and on                                     |
| Post   | token/:id/add_attribute/:id    |            | Add a live attribute                                       |
| Delete | token/:id/remove_attribute/:id |            | Remove a live attribute (must be added by above)           |
| Delete | token/:id                      |            | Deletes the token                                          |
| Get    | token/read/:id                 |            | Returns the token information                              |
| Get    | token/definition/:id           |            | Returns the token definition                               |


    
          user: must be one user
          token-type:
          live attributes: 
          live parents: 
          script and remote states:  


# Making a new token from the token type
Only the owner, the admin group of the owner, or someone on the allowed list (group member or individual)
can create a new token. If the token type is retired then cannot.
Also, actions on the token may prevent the creation.
The creation of the token takes one optional argument, the set the token will be placed

# Deleting a token

Only the token owner can delete a token, but actions can alter the time to live attribute

# Reading a token
 The live attribute values are returned, 
 if the user does not have permission to read some or all attributes those are filtered and not seen
 
# Reading a token definition
If someone can read a token, they can read its definition, but not its state