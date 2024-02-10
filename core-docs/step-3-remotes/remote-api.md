# Remotes

remote api defined at


Remotes cannot change ownership
Remotes can be fully edited if not used anywhere in any element types or elements. They can be turned off though (things happen to the server). Or given a redirect
Remotes deletable if the remote not used in any element or type

Remotes can be tested with a test context. When created the test context will be set used to remember stats to follow the rules of cool-down
There can be multiple test_contexts for each remote.




| Method | Path                                  | Route Name | Operation                                                | Args                                            |
|--------|---------------------------------------|------------|----------------------------------------------------------|-------------------------------------------------|
| Post   | remote                                |            | Makes a new remote                                       | Required name: optional states, required remote |
| Patch  | remote/edit/:id                       |            | Edit part of value, if possible, sparse                  | Any detail , sparse update                      |
| Put    | remote/edit/:id                       |            | Edit Value , if possible, full replacement               | All the values for the definition               |
| Get    | remote/:id                            |            | returns full remote info                                 | can pass in optional type and element           |
| Get    | remotes/list                          |            | searches for remotes                                     | iterator,can pass in filtering info             |
| Get    | remote/write/:test_context/:id        |            | Writes to the Remote, returns value or issues            | Runs using context created                      |
| Get    | remote/read/:test_context/:id         |            | Reads from the Remote, returns value or issues           | Runs using context created                      |
| POST   | remote/:id/test_context               |            | Makes a new test context to store state for remote tests | required name                                   |
| Get    | remote/:id/test_contexts/list         |            | Lists all test context names for this remote             | iterator                                        |
| Delete | remote/:id/test_context/:test_context |            | Deletes a test context                                   |                                                 |
| Delete | remote/:id                            |            | Delete Remote, if the user can                           |                                                 |


## Data for defining a remote


        user: required
        name : unique in remotes
        is_retired: default false // if true then cannot be added to element types
        is_on : if off then all read and writes will fail and the remote not called
        timeout_seconds: if an attempt is made to sent to the remote, this is how many seconds until the read or write of the attribute ends in failure
       uri:
            uri_type: (none,url,socket,console,manual)
            uri_method (post, get, patch, put, delete)
            uri_port:
            uri_string 
                
        read_policy:
            allow: bool
            cache: bool, if true then each last call updates the cache, and if same cache param key values then cache is used
            cache_ttl_seconds: how old the cache is allowed to be
            cache_keys: array of string keys to use for the cache, empty means cache returned always
        write_policy:
            allow: bool,
        data:
            input_attribute_map: array<name of attribute, name of key this is sent under>
            output_map: array<name of server output key or xml path, name of key output object will have>
            remote_data : key value pairs with remote_data_type ('none','basic_auth','bearer_auth','data','header') and name, value and is_secret
        call_schedule:
            rate_limit_max_per_unit: x
            rate_limit_unit_in_seconds: x
        state
            local_state_init: the initial state for per attribute or action
            element_state_init: the initial shared state for any element that has this an attribute or action with this remote
            type_state_init: the initial shared state for all elements of the same type that has this remote in an attribute or action
            global_state: shared by all usages of this remote

## Data for a test context

    local_data: {}
    element_data: {}
    type_data: {}
    global_data: {}
