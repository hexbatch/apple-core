# Location bounds

Location is one or more closed polygons.These polygons can be unconnected, overlapping or bordering.

Units can either be in latitude and longitude, or cartesian coordinate.

map coordinates use (lat, lon), cartesian coordinates use (x,y,z) 

coordinates can be very tiny polygons to be used as points (or planes in 3d). 

Locations of the same unit type can stack, and be compared. Is A in B? does A intersect B ?

When attributes stack the locations, there are two stacks set up. One for map, one for cartesian.

When adding a token to a set, both the token being added and a set can have one or more location bounds stacked.
If both stacking units are used in A and B, then both stacking units need to intersect for the token to join the set.

If they only have bounds in different units, this is the same as no bounds calculation and are not considered.

If a set has a location bounds, then it has an option to only accept tokens inside it that have no location set.

If a set has a smaller area or volume than a token entering it, that token can still be active with the set.
A token's location area is its area of possibility. 

locations of the same units can be compared (is this point or plane in this 3d object), is this shape located in my town, is this point in the ocean,
is this cube intersecting this boundary. But different units are not comparable. 

When doing location comparisons between A and B, only the locations that are on at the time due to time or path constraints are used.


    so a map-bound:
        user: id
        name: name of the bounds (unique to the user's bounds)
        polygon array: at least one polygon, they can overlap or not be connected or join. Polygons can be a point
        unit: either geo or cart



