# Map and area Bounds


Create and manage map bounds. These bounds are made up of geo json polygons
Bounds can only be deleted if they are not used anywhere.

Bounds cannot be edited, remove a bounds from an attribute and add in a new one

Bound names can be unique to the bounds of the user, and follow the same rules with numbers, spaces and punctuation
Bound names are not public, nobody is going to see your bound names

:id here is either the guid of the bounds, or the bound name. The id must be owned by the user 

| Method | Path                | Route Name | Operation                                             | Args                |
|--------|---------------------|------------|-------------------------------------------------------|---------------------|
| Post   | bounds/map          |            | Makes a new map boundary                              | name, geo json info |
| Delete | bounds/map/:id      |            | Deletes an unused map boundary                        |                     |
| Get    | bounds/map/:id      |            | shows the map bound data with geo json                |                     |
| Get    | bounds/maps/list    |            | Shows a list of all the bounds the user has           | iterator            |
| Get    | bounds/map/:id/ping |            | returns true or false if a given point is in a bounds | lat, lng or x,y,z   |

        user: id
        name: name of the bounds (unique to the user's bounds)
        polygon array: at least one polygon, they can overlap or not be connected or join
        unit: either geo or cart
