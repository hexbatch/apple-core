# Events

There are many events that are fired off when several different sorts of things happen.
Actions are the only thing that can listen to events.

Many events are hardwired into the code

Each event has a system attribute that must have a value of truthful for the event to be allowed.
When something is going to happen, any action has the ability to decide to set the event attribute to false or 0,
or event_success of false in a json value

For any event, the attribute is the same, so all tokens can listen to the same things

if an attribute or token is out of bounds, or comes back in bounds, there is no event.
Either the thing exists or not.

* token creation
* owner-change
* token-set mass attribute altering
* destruction
* value change
* value_change_filtered (allows the ordering of actions to filter the read value)
* live attribute added to token
* live attribute removed from token
* parent in token turned on
* parent in token turned off
* token enters a set
* token leaves a set

On the type token definer: the events for token creation and destruction are sent:
* before creation (can refuse)
* after creation (notification)
* before destruction (can refuse)
* after destruction (notification)


Set operations (run on the token defining a set)

* Token was added to the set
* Token was removed from the set
* Child was added to the set
* Parent was added to the set
* Link was made from the set
* Link was made to the set
* each set operation has its own event, to allow to disallow the operation


Requirements have a token, events here can be done on it when it's used to filter
* allow_token


## custom events 

Sometimes extensions and layers need to fire off their own events.
Here, we can send a custom event, anything that inherits from the custom even attribute.
And the target can be one token per api call

The token has to have the actions listening to that custom event, to act on it



