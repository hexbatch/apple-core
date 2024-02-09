# Events

There are many events that are fired off when several different sorts of things happen.
Actions are the only thing that can listen to events.

Many events are hardwired into the code

Each event has a system attribute that must have a value of truthful for the event to be allowed.
When something is going to happen, any action has the ability to decide to set the event attribute to false or 0,
or event_success of false in a json value

For any event, the attribute is the same, so all elements can listen to the same things

if an attribute or element is out of bounds, or comes back in bounds, there is no event.
Either the thing exists or not.

* element creation
* owner-change
* element-set mass attribute altering
* destruction
* value change
* value_change_filtered (allows the ordering of actions to filter the read value)
* live attribute added to element
* live attribute removed from element
* parent in element turned on
* parent in element turned off
* element enters a set
* element leaves a set

On the type element definer: the events for element creation and destruction are sent:
* before creation (can refuse)
* after creation (notification)
* before destruction (can refuse)
* after destruction (notification)


Set operations (run on the element defining a set)

* Element was added to the set
* Element was removed from the set
* Child was added to the set
* Parent was added to the set
* Link was made from the set
* Link was made to the set
* each set operation has its own event, to allow to disallow the operation


Requirements have an element, events here can be done on it when it's used to filter
* allow_element


Group sets have events for membership
* member_added
* member_removed
* admin_added
* admin_removed


## custom events 

Sometimes extensions and layers need to fire off their own events.
Here, we can send a custom event, anything that inherits from the custom even attribute.
And the target can be one element per api call

The element has to have the actions listening to that custom event, to act on it

## remote errors
* remote_error 

An action can listen to errors happening to the elements, on one,some or all of the events. Remotes can have issues connecting, or return bad http codes



