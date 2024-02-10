# Actions

Event listeners, they can approve an action or can change attributes values on the same element , or can turn attributes on the element on or off.
Actions can also turn on and off parents of elements.
The attributes do not need to be attached to the same element as the attribute that holds the action,
but as long as the attribute can be changed by the user who owns the element, it can be changed.


It holds a remote, or reads an attribute elsewhere to make a decision when an event is fired

If remote, then it calls that, if it can (rate limiting or in process), when it gets an event it listens to
Can overwrite/add some params going to the remote.
Can have a list of rules:
Can map the remote's out keys to attributes and things it will do with them.
Can use another out key to approve event, set value, or decide if switch on or off, or add/remove a live attribute, or nothing (just ran the remote)
Except for adding live attributes, must target an attribute attached to the element, or must target the element parent

If using value, it can read an attribute from anywhere via a path.
If that value is truthful, then it will do one or more actions, and if setting values of other attributes just copies that attribute value over


Remote rules:

remote out param A| -> attribute listens to see if truthful|-> targets an attribute 
decides to use B to set value, or be a switch, or approve event, or add or remove live attributes
remote out param B| -> attribute listens to see if truthful (switch, approval, add or remove) or get value (to set value)|-> targets an attribute 


and based on what is listened to in the remote, if that is truthful it will do its thing 
(event acceptance or turning on or off switches, or change value of one or more attributes on the element, or add or remove live attributes to the element)

so:
    remote
    event to listen to (parent or leaf), this can be a path to only listen to events in certain cicumstances
    target map (remote param A, path to attribute,remote param B, action it does with B)

Remotes can have unlimited map entries but can only target attributes in the element it is part of for value changes, or target the parent of the element

action-type: permission, value change, switch parents on|off, live add, live remove,  or void (just runs remote)

so an action:

    

note: when making this before paths, just add a table that is called the selection, and only have the attribute id in it until later



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

* To disallow creation, do not approve the creation event, then the element is not saved and creation fails.

Multiple actions can listen to the same events.
* So, to rate limit element creation and charge someone have two actions. One to limit and one to charge
* But, this can also be the same action

if listening to a parent event of more than one type, An inheritance chain will run the actions from the ancestors to the current


# parts of an action

* each attribute the action targets can only change one attribute type. 
  * But, any children or descendants of that type can also be affected, so many attributes can possibly be changed.
  * This can be modified in the selection
  * Optionally, the target can be a parent of an element to turn it on and off 
* What the action does to the target, it can be a switch, or a value change. 
  * If targeting element parents, it can only be a switch
* Can select one or more attributes to have their values set to params  or remote call
* Can select a target path for the attribute, to only affect an attribute of certain elements, types, sets or owners
  * to select an attribute on same element, no path needed. 
  * to select a parent of the element this is on, no path needed




so an action:

    action-name: can be any unique name for actions
    action-owner: actions are be owned by a user
    logic:
        remote:
            remote it holds: remote_id
            extra constant params to override remote input params
            map: (array of) 
                remote param a id, remote param b id, action type to do, target attribute path id (same element)
        value:
            other attribute id path (does not have to be in the same element but if not readable no action done)
            map: (array of)
                action type to do, target attribute path id, (value to write with, if not logic action, is the value of the other attribute above)

    event-path: the path of the event (able to filter set context of an event), path must be using an event attribute id or child of one
    

    target-remembering: all|set|relationship
    run-policy: always, per element, per element type, per set, once only per element type, one only per element
    priority: optional number



# event path
  the event path needs to include an attribute, but can have another element to listen to its events too.
  granting permission can only happen on the element the event is for
  however an element can change its own values or state or do things by remotes if another element does something (like change value, enter the same set, only exist in N sets etc.)

# type of action
  * an action can be to grant permission , they find a value that is truthful or not to approve it. Only one action needs to approve an event even if others deny.
But actions can change things, regardless if they approve or do not approve the event. While every action only is activated by events, 
they do not have to approve or disapprove it.
  * Change a value. The value they have in the rules is applied. 
    * The values to change must be located on the same element as the action running
    * Can only change attribute values, not properties of anything
  * Turn off or on  attributes or clusters on the element
    * depends on the target if this is an attribute or cluster
  * Apply, update or remove  a live attribute
    * value needs to be a json of the attribute id and selected value.
    * If run and live is there, the value will be updated. If removing will remove attribute.
  * or do nothing (just run the remote)



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
  * Only if this action is running a remote
  * the lowest priority will run first, and its value to set is passed to the next highest one, until all the actions have run. The highest priority action will have final say
  * the value can change data type, earlier actions can send up json with flags, and the final one can produce a primitive, or filter out json 
  * The passed value will be put into the remote params as the original value to change
  


# Actions changing values by remote

  While an action can set a constant value , it can call a remote to do that. In this case, the remote 
  will be passed the original value via the set value_param_name.

  If given priority, this becomes a filter for the same attribute and same event

# Actions listening to value_change_filtered

When there are multiple actions (more than one) listening on the same element, and listening to the same path, they can take that changed value, alter it and pass it to the next.


# static params passed tol remote
  The static_other_params will be passed to allow remotes to have context

# action hooks

to allow extensions to use different sorts of actions, there is a hook done before the action is triggered, and after the action is done


