# Elements
Elements are the only thing which can change ownership. Elements always have an owner.

Elements are made from element types, and have live values of those attributes.
Only the allowed users for a type can make an element from it.

When an element is made, the attributes of the element type have values copied over,
and an on/off state, found in the live attributes.

When the attribute of an element is written to or read from, it is using this live state.

Elements can have all the attributes of a parent turned off or on by an action.
Elements have a live parent section that shows which parents are on.


Elements have their aggregate values: bounds, affinities, allergies. This is the union of each.
This also means that some elements cannot be taken to some locations or usable at some times.
Element's behavior in a set depends on these aggregate values for affinities, allergies and path bounds.
When an attribute is off, the bounds are still counted, but the allergies and affinities are not.

Elements by themselves do not have a location, they can have an attribute though that is standard defined, called current_location.
This is only valid for lat and lon. The current_location can be anywhere in the element bounds, and this is not used to determine if the element matches a set location.
A single element can have many current_location values at once, if the values are not global, but set based.

The shape bounds also can set their current location too, with current_location_shape attributes
 
Elements can describe their shape or area, this description is clipped to their locations bounds. The standard attributes shape_shape, shape_map.
if there are more than one attribute that inherits from this, on the element, then each family of attributes is unionized to make the shape, which is still clipped to the bounds.
The shape is centered at the current location (map to map and shape to shape never the two shall meet )


When an element defines a set, it's location bounds is what defines the membership in a set:
deciding how it interacts with entering or being visible in a set that has a bounds or no bounds.


The time of the element is always the current time. When looking at the time attributes.
Path bounds work by the api making calls using the working set


Only the element owner or those in the user's admin group can change who owns his element. To give it to another user.
Ownership of elements can take place in bulk via set operations.

AN element may be in any number of sets at once.
The element bounds does not change when the set bounds changes.

AN element can have the date set so that after it, it's not used or usable, and eventually is recycled. This is determined by the types time to live option


      So an element:
          user: must be one user
          type:
          expiration_at: (optional by type)  
          live attributes: (see attributes)
          live parents:  
          states: for remotes  


## Live parents
[live parents overview](live-parent-overview.md)

Each inherited parent has a live state, and can be turned off and on

## Live attributes
[Live attributes](live-attribute-overview.md)

the list of active attributes for an element.
The active attributes from the parents are chosen as the top most attribute for each name, ordered by parent inheritance list 
The attributes can be toggled on or off

## Personal attributes
[personal-attribute-overview.md](personal-attribute-overview.md)
Can organize elements with personal attributes which do not affect the target element, and can be seen only by the group of the user who owns this attribute 

## time to live

is like a very hard set time boundary for the element, and in many ways is just that, it's factored into any time boundaries the element has.
Once it is past the time to live, the element is not usable, because of the time boundary ending, and there is an api in the admin area to start gc

# Creating elements

Elements are created from a type, and when this happens, the element is made, but then can be destroyed if any constructor events are forbidden.
Each ancestor and parent of the type can have an event that says no, only one needs to say no to prevent the creation, and detroy the element (without destruction event)
See types for more discussion on this.

# Destroying elements

When an element is properly destroyed, each parent and ancestor has a notice, there is no ability to stop the destruction
