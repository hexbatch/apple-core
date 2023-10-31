# Boundaries can be on the map or in time.

Boundaries are only applied to attributes. Here we use location and time and path.

[Location](map-overview.md) is tied to the world map, and can be any region defined by sets of closed polygons with latitude and longitude coordinates

[Time](time-overview.md) is a slice of time this attribute is active, it can be a periodic or time range or any combination of this

[Set path](path-overview.md) is if the attribute is actionable, readable or writeable in the context of a set

Bounds can be simple: such as every Wednesday between 12pm and 2pm in Livingston, Tx

or it can be more complex: a complicated time series for different locations, where each location has its own schedule

Each boundary can have a location or time component, and each attribute can have multiple boundaries

An attribute can have zero , one or many bounds. The bounds can be mixes of a time rules, map areas, paths.
Bounds can be applied to an attribute as long as the user is in a member in the group of the user

Bounds can be edited only if they are not already in use

Bounds are created independently of any other resource

Bounds can be copied,  but not shared


