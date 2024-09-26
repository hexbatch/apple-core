# Events

There are many events that are fired off when several different sorts of things happen.
Actions are the only thing that can listen to events.

Many events are hardwired into the code

Each event has a system attribute that must have a value of truthful for the event to be allowed.
When something is going to happen, any action has the ability to decide to set the event attribute to false or 0,
or event_success of false in a json value

For any event, the attribute is the same, so all elements can listen to the same things

if an attribute or element is out of bounds during when an event would otherwise fire, then there is no event fired.
Either the thing exists or not.

* element creation
* element batch creation (many created by one operation)
* owner-change
* element-set mass attribute altering
* destruction
* value change
* value_change_filtered (allows the ordering of actions to filter the read value)
* live attribute toggled on or off
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


Each group operation has its own event attribute
* allow_operation




server transfer and copying
* before_server_add_element
    If an action denies, then this element is not copied over to the server in question
* is_server_allowed
  * if existing on the server object, then this can auto accept or reject the server being registered
  * can be decided manually by admin role
  * tri value, nullish, truthful, or falsy. nullish means just keep pending 
* before_server_register_user
  * called on the user in question, and can automatically allow the user agreeing to be used in actions in another server
  * can be decided manually by the user later using the api


## remote errors
* remote_error 

An action can listen to errors happening to the with a call to a remote, on other actions in the same element.
This is sent off to be processed after the other remote tree completely ends.
The action can map into the fields of the remote_error event

## custom events

inherits from the base attribute of custom_events

two use cases:

A user can create a custom event with action listeners for that. This helps automate.
Sometimes extensions and layers need to fire off their own events.



# Event messages can  have data

Events can be designed to hold structured data. They can have accepted top level keys and even a json path to make sure things are as they should be.

An action can plug in these values to its value mapping to send to the remote or rules to change the value.

When action is run, the remote can give back data, which can be added to the event by the action mapping rules, before that event is passed to a lower priority handler.

The event can be defined to require some or all its data to be filled in before being given to the actions

For example, in element creation , a remote server can decide, for any reason, to not allow something, when there are many elements doing things.
If the server has a message attribute or key or field in the response, then this will be added to the api response here when something does not succeed

# DB structure
each event definition is defined as an  attribute, the event attribute does not have bounds 
This parent attribute is a standard attribute

in the attribute, the value is json and has two optional objects: all_keys and required_keys

When an event is fired, its fired as a child of the attribute



