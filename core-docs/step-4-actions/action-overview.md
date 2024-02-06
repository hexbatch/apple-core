# Actions

Event listeners, they can approve an action or can change attributes values on the same element , or can turn attributes on the element on or off.
Actions can also turn on and off parents of elements.
The attributes do not need to be attached to the same element as the attribute that holds the action,
but as long as the attribute can be changed by the user who owns the element, it can be changed.


Actions can be registered that run scripts or remotes. 
The values returned by these are the new values of the attribute,
or the truthful value that turns on or off attributes or parent clusters.

But an action results can also be a constant value.

An action runs on the bounds of the attribute it is attached to (and not the entire element).
This means an action can be restricted, and different bounds can do different things for the same event.

Actions listen to events, and can cancel them. If multiple actions are listening to the same event, 
Only one has to cancel it for the event to not be allowed to happen.
In that case, if any actions listening to the event is changing attribute values on the element, then those changes are not used

An action can only listen to one event.

-------------------------------
## Events 

see [events.md](events.md)

--------------------------------


## Actions can be used to set rules for creation of an element:

* To disallow creation, each element starts with a created attribute whose value must be truthful, if this value is false, then the element is not saved and creation fails.
* Creation rate limiting is handled by the creation actions script_state

Rate limiting is scripts running on element set changes, or lifecycle changes
* on a lifecycle script, it has to return a truthful value to allow (this is changed from the existing docs)

Multiple actions can listen to the same lifecycle changes or other conditions.
* So, to rate limit element creation and charge someone have two actions. One to limit and one to charge
* But, this can also be the same action

An inheritance chain will run the actions from the ancestors to the current
* if any action fails, then there will be a db rollback, and nothing is saved

Some life cycle attributes are not events, but can be changed by actions.
* time to live - set in seconds and compared to the creation ts

# parts of an action

* what attribute the action targets, each action can only change one attribute type. 
  * But, any children or descendants of that type can also be affected, so many attributes can possibly be changed.
  * Optionally, the target can be a parent of an element to turn it on and off 
* What the action does to the target, it can be a switch, or a value change. 
  * If targeting element parents, it can only be a switch
* Can select one or more attributes to have their values set to params to a script or remote call
* Can select a target path for the attribute, to only affect an attribute of certain elements, types, sets or owners
  * to select an attribute on same element, no path needed. 
  * to select a parent of the element this is on, no path needed

When making an action to charge elements for an event, use a remote set to quickly run api to check balance and transfer


            so an action:
                action-name: can be any unique name for actions
                action-owner: actions are be owned by a user
                event-path: the path of the event (able to filter set context of an event), path must be using an event attribute id or child of one
                target-path: see paths (must end in attribute on the element this belongs to  ok if path is invalid, in that case no target and no changes)
                target-remembering: all|set|relationship
                action-type: permission, value change, switch on|off, live add, live remove,  or void (just runs a script or remote)
                input-params: [{path: name of param on the script or remote}]
                run-policy: always, per element, per element type, per set, once only per element type, one only per element
                value: a script, or remote id, or another attribute path for setting values
                  value_param_name: when changing value, the older value is passed via an input param name of the script or remote
                  static_other_params: passed to the remote or script unchanged
                priority: optional number



# Requirements: making sure only so many paths exists

If needing the requirements that only so many things can or can not exist, in how they are in element sets:

Actions can be set to allow or deny any lifecycle, by seeing if the target attribute value changing will cause a target path specifier to fail.
This can be done by counting the number of path specifiers anywhere, using the current target attribute value,
and if only one, before the value change, or not in the allowed count range,
it will block the lifecycle change

Such actions do not need scripts or remotes

# event path
  the event path needs to include an attribute, but can have another element to listen to its events too.
  granting permission can only happen on the element the event is for
  however an element can change its own values or state or do things by remotes if another element does something (like change value, enter the same set, only exist in N sets etc.)

# type of action
  * an action can be to grant permission , they return a value that is truthful or not to approve it. Only one action needs to approve an action even if others deny.

The other types of actions only happen if the events they are listening to are approved by permission actions:
  * or to change a value. The value they hold is applied. If this is a script or remote then the return from that is applied.
    * The values to change must be located on the same element as the action running
    * Can only change attribute values, not properties of anything
  * Turn off or on  attributes or clusters on the element
    * depends on the target if this is an attribute or cluster
  * Apply, update or remove  a live attribute
    * value needs to be a json of the attribute id and selected value.
    * If run and live is there, the value will be updated. If removing will remove attribute.
  * or do nothing (just run the script or remote)



--------------------

# turning on and off an element's parent

All the attributes from a parent of an element can be turned on and off at once,
but if the element has dynamic attributes that overwrite this then those stay on

# Multiple target paths

If selecting multiple target attributes to listen to, then they all have to have events fired for them first before the action will activate and do its own thing.
It can remember the counts, and this resets for each api operation

# Action run order (priority)

* Actions that respond to the same event can be given an optional run order, and the actions are run from the lowest to the highest
* Once the first action approves an event, the others are not called
* Once the first action to turn on or off or toggle an attribute, cluster or live is run, the others are not run
* Voids are always run
* If more than one action is responding to the same approved event, and they are changing the same attribute value this becomes a filter
  * Only if this action is running a remote or script
  * the lowest priority will run first, and its value to set is passed to the next highest one, until all the actions have run. The highest priority action will have final say
  * the value can change data type, earlier actions can send up json with flags, and the final one can produce a primitive, or filter out json 
  * The passed value will be put into the script or remote params as the original value to change
  


# Actions changing values by script or remote

  While an action can set a constant value , it can call a remote or script to do that. In this case, the remote and script 
  will be passed the original value via the set value_param_name.

  If given priority, this becomes a filter for the same attribute and same event

# Actions listening to value_change_filtered

When there are multiple actions (more than one) listening on the same element, and listening to the same path, they can take that changed value, alter it and pass it to the next.


# static params passed to script or remote
  The static_other_params will be passed to allow scripts and remotes to have context

# action hooks

to allow extensions to use different sorts of actions, there is a hook done before the action is triggered, and after the action is done


