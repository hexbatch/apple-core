# Shapes
# (changelist todo or ponder about)
------------------------
There have been updates about the core supporting some of these features

Also, binders in the transactions should be addressed?

---------------------------------------------
---------------------------------------------


A Set can be represented by a shape, with texture and color. The model is stored as json but can be converted and rendered by something else.
All images are stored elsewhere, and the json has urls

A set can be a 3d area, or map, and children sets in it can have position inside of it.
    This map can have a bounds

The set's visual can be represented by the children, and not have any shape itself.
But a child set will have a position inside the parent set in order for it to be seen and interacted with by shape.
Other sets and tokens inside the set can affect behavior and other things though.

When a user token enters a set that is also a map, then software can render the shapes recorded, 
because child sets will be seen as objects inside the parent set, those objects can be entered by the user also, and then that new set is the map
This can be nested to any level.
Also, entering a child set allows users to visit links to other sets, and revisit the parent or go deeper into the child objects.
Links can be shapes, if they have visuals set

Position of the child set is decided by attributes on the child, which can be altered by any writer

In a set, when two child sets have overlapping shape boundaries, they are given an event there is a collision.
When the intersection ends, the previously overlapping sets are given an all clear event.

When entering a set map, the new users can be assigned a position via an event (event fired when user enters because token enters set, normal event)

A parent set can move its children in concert, to have different parts of the same visual be processed by different sets (different hit regions and interactions in the same unit)

-----------------------------------------------------

Can use a container of an interface to have a shape, and can link that shape to the values of that interface being read.
Pipelines can be matched to turn on and off parts of the shape definition. When one or more things comes through the pipeline, then that shape part is activated for the next N time

This allows complex associations to be marked by simpler shapes and colors.