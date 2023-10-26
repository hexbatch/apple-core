# Scripts

script api defined at 


Scripts cannot change ownership
Scripts can be edited if not used anywhere in any token types or tokens
Scripts deletable if the script not used in any token or type

Scripts can be tested with a test context. When created the test context will be set to the init states, contexts also have any set parameters
There can be multiple test_contexts for each script

Scripts can be seen and edited in full by anyone in the user's group admin

| Method | Path                                  | Route Name | Operation                                                | Args                                            |
|--------|---------------------------------------|------------|----------------------------------------------------------|-------------------------------------------------|
| Post   | script                                |            | Makes a new script                                       | Required name: optional states, required script |
| Patch  | script/edit/:id                       |            | Edit part of value, if possible, sparse                  | Any detail , sparse update                      |
| Put    | script/edit/:id                       |            | Edit Value , if possible, full replacement               | All the values for the definition               |
| Get    | script/:id                            |            | returns full script info                                 | can pass in optional type and token             |
| Get    | script/run/:test_context/:id          |            | Runs Script, returns value or issues                     | Runs using context created                      |
| POST   | script/:id/test_context               |            | Makes a new test context to store state for script tests | required name                                   |
| Get    | script/:id/test_contexts              |            | Lists all test contexts for this script                  |                                                 |
| Get    | script/:id/test_context/:test_context |            | Lists one test context for this script                   |                                                 |
| Patch  | script/:id/test_context/:test_context |            | Changes test context                                     | can either update local or global or both       |
| Delete | script/:id/test_context/:test_context |            | Deletes a test context                                   |                                                 |
| Delete | script/:id                            |            | Delete Script, if the user can                           |                                                 |


## Data for defining a script

    user: 
    name :
    is_retired: default false // if true then cannot be added to token types    
    local_script_state_init: 
    global_script_state_init: 
    script: 
        script_text
        extra_script_input_params
        output_keys

## Data for reading a script 

    user: required
    name : unique in scripts
    permissions: [ max allowed time and ram]
    md5 of script: makes sure the script is not changed when this is applied to any instantiated actions
    local_script_state_init: if the read was not passed a token
    global_script_state_init: if the read not passed a type
    local_script_state: if the read was passed a token
    global_script_state: if the read was passed a token type
    script: 
        script_text
        extra_script_input_params
        output_keys (if returning an object)
 
### Data for a test context

    input_data: {}
    local_status: {}
    global_state: {}