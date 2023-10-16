# Boundaries can be on the map or in time.

Boundaries are only applied to attributes. Here we use location and time.

[Location](location_bounds.md) is tied to the world map, and can be any region defined by sets of closed polygons with latitude and longitude coordinates

[Time](time_bounds.md) is a slice of time this attribute is active, it can be a periodic or time range or any combination of this

Bounds can be simple: such as every Wednesday between 12pm and 2pm in Livingston, Tx

or it can be more complex: a complicated time series for different locations, where each location has its own schedule

Each boundary can have a location or time component, and each attribute can have multiple boundaries

An attribute can have zero , one or many bounds. Each bound can have either a time component, a location component or both.

Bounds can be edited only if they are not already in use

Bounds are created independently of any other resource

    so a map-bound:
    user: must be one user.
    name: name of the bounds (unique to the user's bounds)
    location_bounds array: 0 or more locations
    time_bounds array: 0 or more times

