# Map and area Bounds


Create and manage map bounds. These bounds are made up of geo json polygons
Bounds can only be deleted if they are not used anywhere.

Bounds cannot be edited, remove a bounds from an attribute and add in a new one

Bound names can be unique to the bounds of the user, and follow the same rules with numbers, spaces and punctuation
Bound names are not public, nobody is going to see your bound names

:id here is either the guid of the bounds, or the bound name. The id must be owned by the user 

| Method | Path                                             | Route Name                  | Operation                                    | Args                      |
|--------|--------------------------------------------------|-----------------------------|----------------------------------------------|---------------------------|
| Post   | bounds/location/create/{map or shape}            | core.bounds.location.create | Makes a new map boundary                     | name, geo json info       |
| Delete | bounds/location/:id/delete                       | core.bounds.location.delete | Deletes an unused map boundary               |                           |
| Get    | bounds/location/:id/get                          | core.bounds.location.get    | shows the map bound data with geo json       |                           |
| Get    | bounds/location/list/:user                       | core.bounds.location.list   | Shows a list of all the bounds the user has  | iterator  , user optional |
| Get    | bounds/location/:id/ping/{location_json_to_ping} | core.bounds.location.ping   | returns info if a given point is in a bounds | geojson of hit area       |

        user: id
        bound_name: name of the bounds (unique to the user's bounds)
        geo_json: a polygon or multipolygon, they can overlap or not be connected or join
        unit: either map or shape
