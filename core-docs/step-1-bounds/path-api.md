# Pathing Bounds


Create and manage a set path rule. The element's set context must match the path rule.
This will allow the same element to do different things based on the set it uses as its context in an api call.

Bounds can only be deleted if they are not used anywhere.

Bounds cannot be edited, remove a bounds from an attribute and add in a new one

Bound names can be unique to the bounds of the user, and follow the same rules with numbers, spaces and punctuation
Bound names are not public, nobody is going to see your bound names

:id here is either the guid of the bounds, or the bound name. The id must be owned by the user



| Method | Path                     | Route Name | Operation                                  | Args                |
|--------|--------------------------|------------|--------------------------------------------|---------------------|
| Post   | bounds/path              |            | Makes a new path                           | name, search string |
| Delete | bounds/path/:id          |            | Deletes an unused path                     |                     |
| Get    | bounds/path/:id          |            | shows the path associated with this        |                     |
| Get    | bounds/paths/list        |            | Shows a list of all the paths the user has | iterator            |
| Get    | bounds/schedule/:id/ping |            | returns true or false if in the path       | a set id            |


        user: id
        name: name of the bounds (unique to the user's bounds)
        search_expressions: array of search expressions ending at a set the element can belong to, or a sibling element in a set the element can belong to
