# Actions

Actions can be registered that run javascript functions.



Actions can run on boundary set on the attribute, cron times make it run, entering or exiting areas: see location_entering, location_leaving.

Actions can be used to change own parent or other thing's values (so token or the token sets the token is in) (permission apply).

Actions can be used to set rules for creation of a token
* To disallow creation, each token starts with a created attribute whose value must be truthful, if this value is false, then the token is not saved and creation fails.
* Creation rate limiting is handled by the creation actions script_state

Rate limiting is scripts running on token set changes, or lifecycle changes
* on a lifecycle script, it has to return a truthful value to allow (this is changed from the existing docs) 

Multiple actions can listen to the same lifecycle changes or other conditions.
* So, to rate limit token creation and charge someone have two actions. One to limit and one to charge
* But, this can also be the same action

An inheritance chain will run the actions from the ancestors to the current
* if any action fails, then there will be a db rollback, and nothing is saved

When setting a charge, if there are not enough tokens in the source token set, the action will fail
* The charge will only happen if the script returns a truthful value to the target attribute

Lifecycle for attributes:
* creation
* owner-change
* token-set addition
* token-set removal
* token-set mass attribute altering
* destruction
* value change

Input params:
input params have more data 
* target_tokens[]
* token-set
* set operation info
* lifecycle

Script returns:

depends on what the script is used for: can be a primitive to be evaluated for truthfulness, can be changed attribute values for the target



            so an action:
                action-name: can be any unique name
                action-version: can be a version (optional)
                action-owner: actions are be owned by a user
                target:
                  target token-type : null for self token
                  target attribute guid: (value changed)
                  target-from-state: literal string, number or regex (empty means always) can be used with the lifecycles
                  target-switch: the value of the action turns on or off the live attribute for this token (everywhere in all sets)
                  target-parent-switch: the value of this action turns off the parent listed here for the target 
                lifecycle: [] array of life cycles this script runs on, without looking at the target from-state, can be empty
                param_attributes: [] if not empty then these attributes must exist on the token or type-group for the action to run
                recipient: //optional
                    recipient attribute: the script can only change the recipient attribute
                    recipient token: if not empty, this token must be writable by the user of the action, the token does not have to be the target, and no other tokens will be written to
                charge : //optional sets up a token-set operation
                    charge_type: the type-group to charge with
                    charge_source_set: the token-set to remove tokens from
                    charge_destination_set: the token-set to put the tokens
                options:  
                    per-token: if true, this script runs per token that has the attribute meet requirements, and only its attribute can be changed
                               if false then script runs per set, and all the set population tokens and their target attributes are looked at,  and any recipient token in the set can be changed.
                    run-when-out-area: default false, else runs when token or type-group is outside of location bounds
                    run-when-in-area: default true runs when the token or type-group is inside the location bounds
                
                action: 
                    script: script_id
                        see input params
                        see script returns
                OR 
                    url: url_id
                        see input params
                        see script returns
                OR
                    target path specifier: a string path specifier ending with the target attribute and a value 
                    min_allowed: 
                    max_allowed:


# Requirements: making sure only so many paths exists

If needing the requirements that only so many things can or can not exists, in how they are in token sets:

Actions can be set to allow or deny any lifecycle, by seeing if the target attribute value changing will cause a target path specifier to fail.
This can be done by counting the number of path specifiers anywhere, using the current target attribute value,
and if only one, before the value change, or not in the allowed count range,
 it will block the lifecycle change

Such actions do not need scripts or urls


# Turning on and off a live attribute

A token's live attribute can be turned off and this will be everywhere

# turning on and off a token's parent

All the attributes from a parent of a token can be turned on and off at once, but if the token has dynamic attributes that overwrite this then those stay on


