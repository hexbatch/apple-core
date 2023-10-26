# Scripts

Javascript with saved state for the token its attached to, and saved state for the token type its attached to (via the attribute)

Scripts that are run, are not able to access the api, so the passed current_attributes changes will be thrown away after the script exits
When a script changes the local and global script states,  then those values will be saved (so the script changes those param values)

Scripts can change the local and global settings for themselves.

A script is passed in an object, the object will have all the attributes of the token in a name value , this will be under the current_attributes.

The script can return a primitive or a simple object to be converted to json

Actions will pass in more data to the input_param, and the return values are more defined

input_param:
* write_value: {} empty except when a script attribute is written to
* current_attributes: {}
* current token owner, current api user
* local script_state (stored in the token its attribute parent is attached to)
* global script state (stored in the token type attribute that is made when an attribute having the script is attached to the token type)


##  immutability

Sometimes a script will not change its value for a time range, this is the data good timestamp. This can be saved to the global or the local settings.
If the local is set, that is the timestamp to use. Else the global, if that is set, will be used

If the value of the script is queried before this timestamp, the cached value will be used. If the global is set, but not the local, then the global cached is used.
A value of null will mean not cached


## definition

        script:
                user: required
                name : unique in scripts
                is_retired: default false // if true then cannot be added to token types
                md5 of script: (calculated) makes sure the script is not changed when this is applied to any instantiated actions
                local_script_state: stored json and passed to script as an object, updated in the script. This is per instantiation
                local_script_state_init: the initial local_script_state
                global_script_state_init: template for the global state on init of token type 
                global_script_state: shared by all scripts of the same token type 
                script: 
                    script_text
                    extra_script_input_params
                    output_keys

## script permissions

* Scripts are run in a sandbox not allowing file access
* The users who can create a script is in the script_creation group 
