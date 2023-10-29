# Actions

actions api defined at [actions.yaml](../../../api-docs/actions.yaml)

Actions have an owner, version, name, target, lifecycle, recipient, charge, options,script

actions can be attached to multiple different attributes

| Method | Path            | Description                 |
|--------|-----------------|-----------------------------|
| Post   | action          | Makes a new action          |
| Put    | action/:id      | Sparse edit an action       |
| Delete | action/:id      | Delete Only if not used     |
| Get    | action/:id/test | Test an action with dry run |
| Get    | action/:id/list | List an action where used   |
| Get    | actions/list    | List all the actions        |

    action-name: can be any unique name for actions
    action-owner: actions are be owned by a user
    target-path: see paths
    action-type: value change or switch or void (just runs a script or remote)
    input-params: [{path: name of param on the script or remote}]
    run-policy: always, per token, per token type, per set, once only per token type, one only per token
    value: a script, or remote id, or another attribute path

## Creating an action
The user running this is the owner,
needs a target, type,policy and value



## Editing an action

Any admin in the user's group can edit, but can only edit if not in use
Any part can be changed

## Test an action
Run action, set an event and a token for the action to run on, and perhaps a set,
Get back the value the action gives


## Listing where an action is used at

Gives a list of attributes this action is used at, wide option to list the token types and tokens

## Listing actions owned by this user

filter for event type