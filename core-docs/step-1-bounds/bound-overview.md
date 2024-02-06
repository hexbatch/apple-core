# Boundaries can be on the map or in time.

Boundaries are only applied to attributes. Here we use location and time and path.
Attributes can merge their bounds, but never intersect their bounds. If an element has two attributes that have a location and time and/or path,
then that element's time, location and path is both of them.

Each attribute can only have one bounds of each of the three types, at most.
This allows one attribute to have some map bounds, on a schedule and in certain set relations.
For any of the bounds in an attribute to be used, they all have to be on at that time.

The element can mix any attributes together to make simple or complex bounds.

Bounds of an element is only important when it's included in a set, or search result (looking for elements not in a set context).
The set has some area or shape, or time or path. A search has a time

Should the bounds of the set change, this will not remove elements from that set,
but can make those now incompatible elements not seen or used in anything that uses the contents of that set.
When the set is back in a location ,time or path, that the element can intersect, then these members are visible again.
Likewise, a set changing its bounds can turn on and off element's ability to be read and/or written 

Time sensitive elements will be included in a search again , or set contents again, when the time matches when it exists.

Path sensitive elements respond to the relationships in a set that it is in.

Location sensitive elements matter when compared to a set location, or searches using location (give me everything south of that town on the map)


The ability to read or write to an attribute on an element is also determined by bounds. It is possible to read an element in one bounds, and write to it in another

[Location](location-overview.md)  can be any point, 2d or 3d polygon. It can either be geographic for lat and long and altitude, or use a cartesian coordinates.

[Time](time-overview.md) is a slice of time this attribute is active, it can be a periodic or time range or any combination of this

[Set path](path-overview.md) is if the attribute is actionable, readable or writeable in the context of a set

Bounds can be simple: such as every Wednesday between 12pm and 2pm in Livingston, Tx

or it can be more complex: a complicated time series for different locations, where each location has its own schedule

Each boundary can have a location or time component, and each attribute can have multiple boundaries

Bounds can be edited only if they are not already in use

Bounds are created independently of any other resource

Bounds can be copied,  but not shared


