# Location events and bounds


## add new core events
*  start intersection (map and cartesian)
*  intersection move (when a shape moves while intersecting, the one who is moving does not get the message)
*  end of intersection (to all that were intersected, but now are not)
*  start bordering
*  end bordering ( when shapes are next to each other)
*  Shape entered (to the set)
*  Shape moved (to set, can forbid. Can change the set position)
*  Shape left (to the set)

While events are decided on the set level, anything can listen in on the stuff moving around

internally have trigger keep up table(s) of intersecting shapes (2d and 3d)

Parents can organize children shapes in response to events
can have parent send all children custom events for specific behavior


## Add new search terms

Searches can select on the spacing (@intersection, @bordering, @seperated) of the tokens in a same set.


# Discussion

A token can be represented by a shape, with texture and colors and models.

A token can have a 3d or 2d shape, or both at the same time. Sets are tokens also, and can show their children shapes inside.
Children sets can have position inside their parents, that is relative to the parent and not the grandparent.
There is no limit to parent child shape depth.


The set's visual can be represented by the children, and not have any shape itself.
But a child set will have a position inside the parent set in order for it to be seen and interacted with by shape.
Other sets and tokens inside the set can affect behavior and other things though.

When a user token enters a set that is also a map, then software can render the shapes using the standard attributes for shapes (defined in the core).

Because child sets will be seen as objects inside the parent set, those objects can be entered by the user also, and then that new set is the rendered view.
This can be nested to any level.
Also, entering a child set allows users to visit links to other sets, and revisit the parent or go deeper into the child objects.
Links can be shapes, if they have visuals set



In a set, when two elements have overlapping shape boundaries, they are given an event there is a collision.
If each shape moves in an api call, while intersecting, the non-moving shapes being intersected getting the move events.
When the intersection ends, the previously overlapping elements are given an all clear event.

A bordering event is sent to each element when they are touching but not intersecting. So intersection bounds is when go one unit past bordering.

When entering a set , sets and tokens that are shapes can be assigned a position via an event.
Sets have ultimate ability to position their tokens and sets inside, but cannot violate their bounds at all.

A set can position its elements the same in all paths, or in a set context (if the parent set is somewhere else it can have different positioning)
Due to attribute value context.

-----------------------------------------------------

Container of an interface can have a shape, and can link that shape to the values of that interface being read.
Binders can change shapes depending on what they are holding.
Binders can have a shape anywhere in the set, and have shape interaction

Avatars can touch shapes to turn on and off binder areas.


Pipelines can be matched to turn on and off parts of the shape definition. When one or more things comes through the pipeline, then that shape part is activated for the next N time

This allows complex associations to be marked by simpler shapes and colors.

Also, if you need animation, or certain frames per time, have process call on a timer, and let user make a lot of api calls. This is probably best done in local install.




