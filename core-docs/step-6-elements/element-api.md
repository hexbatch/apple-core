# Elements


| Method | Path                              | Route Name | Description                                                     |
|--------|-----------------------------------|------------|-----------------------------------------------------------------|
| Post   | element                           |            | Makes a new element from an element type, optional set to place |
| Patch  | elements/:id                      |            | Sparse edit an element (but not its attributes or state         |
| Patch  | elements/:id/states               |            | Sparse edit the states of an element                            |
| Patch  | elements/:id/edit_attribute/:id   |            | Edit a live attribute value, or turn it off or on               |
| Patch  | elements/:id/turn_attribute/:id   |            | turn attribute off or on                                        |
| Patch  | elements/:id/turn_parent/:id      |            | Turn parent off and on                                          |
| Post   | elements/:id/add_attribute/:id    |            | Add a live attribute                                            |
| Delete | elements/:id/remove_attribute/:id |            | Remove a live attribute (must be added by above)                |
| Delete | elements/:id                      |            | Deletes the element                                             |
| Get    | elements/read/:id                 |            | Returns the element information                                 |
| Get    | elements/definition/:id           |            | Returns the element definition                                  |


    
          user: must be one user
          type:
          live attributes: 
          live parents: 
          remote states:  


# Making a new element from the element type
Only the owner, the admin group of the owner, or someone on the allowed list (group member or individual)
can create a new element. If the element type is retired then cannot.
Also, actions on the element may prevent the creation.
The creation of the element takes one optional argument, the set the element will be placed

# Deleting an element

Only the element owner can delete an element, but actions can alter the time to live attribute

# Reading an element
 The live attribute values are returned, 
 if the user does not have permission to read some or all attributes those are filtered and not seen
 
# Reading an element definition
If someone can read an element, they can read its definition, but not its state

