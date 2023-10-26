# Map and area Bounds

bounds api defined at [bounds.yaml](../../../api-docs/bounds.yaml)

Create and manage map bounds. These bounds are made up of geo json polygons
Bounds can only be deleted if they are not used anywhere.

Bounds cannot be edited, remove a bounds from an attribute and add in a new one

Bound names can be unique to the bounds of the user, and follow the same rules with numbers, spaces and punctuation
Bound names cannot be aliased, but they are not public either, nobody is going to see your bound names

:id here is either the guid of the bounds, or the bound name. The id must be owned by the user 

| Method | Path                                    | Route Name | Operation                                                     | Args                |
|--------|-----------------------------------------|------------|---------------------------------------------------------------|---------------------|
| Post   | bounds/map                              |            | Makes a new map boundary                                      | name, geo json info |
| Delete | bounds/map/:id                          |            | Deletes an unused map boundary                                |                     |
| Get    | bounds/map/:id                          |            | shows the map bound data with geo json                        |                     |
| Get    | bounds/maps                             |            | Shows a list of all the bounds the user has                   | maybe pagination    |
| Get    | bounds/map/:id/ping                     |            | returns true or false if a point or area is in bounds         | lat, lng            |


