# Pathing Bounds

bounds api defined at [bounds.yaml](../../../api-docs/bounds.yaml)

Create and manage a set path rule. The token's set context must match the path rule.
This will allow the same token to do different things based on the set it uses as its context in an api call.

Bounds can only be deleted if they are not used anywhere.

Bounds cannot be edited, remove a bounds from an attribute and add in a new one

Bound names can be unique to the bounds of the user, and follow the same rules with numbers, spaces and punctuation
Bound names cannot be aliased, but they are not public either, nobody is going to see your bound names

:id here is either the guid of the bounds, or the bound name. The id must be owned by the user



| Method | Path                     | Route Name | Operation                                  | Args              |
|--------|--------------------------|------------|--------------------------------------------|-------------------|
| Post   | bounds/path              |            | Makes a new path                           | name, search string |
| Delete | bounds/path/:id          |            | Deletes an unused path                     |                   |
| Get    | bounds/path/:id          |            | shows the path associated with this        |                   |
| Get    | bounds/paths             |            | Shows a list of all the paths the user has | maybe pagination  |
| Get    | bounds/schedule/:id/ping |            | returns true or false if in the path       | a set id          |


