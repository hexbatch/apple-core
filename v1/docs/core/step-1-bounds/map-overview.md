# Location in Map Bounds

Map bounds is a set of closed polygons denoting map coordinates

Each map bounds can have between one and many closed polygons. These polygons can be unconnected, overlapping or bordering

Each map bounds can be paired with a time bounds, so that the location is only bounded if the current time is in the time bounds.

An attribute's total map bounds is the union of all the map bounds in the attribute that is on during the time queried.

Map bounds always exist inside a created bounds

    so a map-bound:
        user: id
        name: name of the bounds (unique to the user's bounds)
        polygon array: at least one polygon, they can overlap or not be connected or join


# how map bounds work with locations defined by tokens and sets

Location: if a token does not define its location, then its location can be that of a set it is in. This means such tokens can have many locations at once.

Each token location is used when determining which tokens in a set are readable and writable. But if no location set, then this bounds not applied.

The same token can be readable or not, writable or not, in different sets at the same time