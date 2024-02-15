# Actions


Actions have an owner, version, name, target, lifecycle, recipient, charge, options,remote

actions can be attached to multiple different attributes

| Method | Path                     | Route name | TO Do | Description                        |
|--------|--------------------------|------------|:------|------------------------------------|
| Post   | action                   |            |       | Makes a new action                 |
| Put    | action/:id               |            |       | Sparse edit an action              |
| Delete | action/:id               |            |       | Delete Only if not used            |
| Get    | action/:id/test          |            |       | Test an action with dry run        |
| Get    | action/:id/read          |            |       | Gets the action definition         |
| Get    | action/:id/list          |            |       | iterator,List an action where used |
| Get    | actions/list             |            |       | iterator,List all the actions      |
| Post   | events/send_custom_event |            | *     | event attribute, target element    |

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
    

    context: normal|set|parent|children
    run-policy: always, per element, per element type, per set, once only per element type, one only per element
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

# Sending custom events
events can be sent to a search path, and if too many in search, events can be sent to the next page.
There needs to be some tracking here of pages when they are done. Which implies here for the custom there is a log going on somewhere
