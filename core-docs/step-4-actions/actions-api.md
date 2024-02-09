# Actions


Actions have an owner, version, name, target, lifecycle, recipient, charge, options,remote

actions can be attached to multiple different attributes

| Method | Path                     | Route name | Description                        |
|--------|--------------------------|------------|------------------------------------|
| Post   | action                   |            | Makes a new action                 |
| Put    | action/:id               |            | Sparse edit an action              |
| Delete | action/:id               |            | Delete Only if not used            |
| Get    | action/:id/test          |            | Test an action with dry run        |
| Get    | action/:id/read          |            | Gets the action definition         |
| Get    | action/:id/list          |            | iterator,List an action where used |
| Get    | actions/list             |            | iterator,List all the actions      |
| Post   | events/send_custom_event |            | event attribute, target element    |

    action-name: can be any unique name for actions
    action-owner: actions are be owned by a user
    event-path: the path of the event (able to filter set context of an event), path must be using an event attribute id or child of one
    target-path: see paths (must end in attribute on the element this belongs to, ok if path is invalid, in that case no target and no changes)
    target-remembering: all|set|relationship
    action-type: permission, value change, switch on|off, live add, live remove,  or void 
    input-params: [{path: name of param on the remote}]
    run-policy: always, per element, per element type, per set, once only per element type, one only per element
    value: a remote id, or another attribute path
    priority: optional number


## Creating an action
The user running this is the owner,
needs a target, type,policy and value



## Editing an action

Any admin in the user's group can edit, but can only edit if not in use
Any part can be changed

## Test an action
Run action, set an event and an element for the action to run on, and perhaps a set,
Get back the value the action gives


## Listing where an action is used at

Gives a list of attributes this action is used at, wide option to list the element types and elements

## Listing actions owned by this user

filter for event type
