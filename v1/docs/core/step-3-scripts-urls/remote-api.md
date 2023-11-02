# Remotes

remote api defined at


Remotes cannot change ownership
Remotes can be fully edited if not used anywhere in any token types or tokens. They can be turned off though (things happen to the server). Or given a redirect
Remotes deletable if the remote not used in any token or type

Remotes can be tested with a test context. When created the test context will be set used to remember stats to follow the rules of cool-down
There can be multiple test_contexts for each remote. Unlike scripts, these cannot be edited

Remotes can be seen and edited in full by anyone in the user's group admin, or in the remote_permission admin group



| Method | Path                                  | Route Name | Operation                                                | Args                                            |
|--------|---------------------------------------|------------|----------------------------------------------------------|-------------------------------------------------|
| Post   | remote                                |            | Makes a new remote                                       | Required name: optional states, required remote |
| Patch  | remote/edit/:id                       |            | Edit part of value, if possible, sparse                  | Any detail , sparse update                      |
| Put    | remote/edit/:id                       |            | Edit Value , if possible, full replacement               | All the values for the definition               |
| Get    | remote/:id                            |            | returns full remote info                                 | can pass in optional type and token             |
| Get    | remotes/list                          |            | searches for remotes                                     | iterator,can pass in filtering info             |
| Get    | remote/write/:test_context/:id        |            | Writes to the Remote, returns value or issues            | Runs using context created                      |
| Get    | remote/read/:test_context/:id         |            | Reads from the Remote, returns value or issues           | Runs using context created                      |
| POST   | remote/:id/test_context               |            | Makes a new test context to store state for remote tests | required name                                   |
| Get    | remote/:id/test_contexts/list         |            | Lists all test context names for this remote             | iterator                                        |
| Delete | remote/:id/test_context/:test_context |            | Deletes a test context                                   |                                                 |
| Delete | remote/:id                            |            | Delete Remote, if the user can                           |                                                 |


## Data for defining a remote


        user: required
        name : unique in urls
        is_retired: default false // if true then cannot be added to token types
        is_on : if off then all read and writes will fail and the remote not called
        redirect: id of another remote
        uri: 
            url: (can be ip)
                method:
                port:
            socket: ( if set the url is ignored) 
                port:
        auth:
            auth_type:
            token:
            user:
            pw:
        data:
            additional_post_data : constant json
            extra_input_params
            output_keys
        read_policy:
            allow: yes or no
            cool_down: (optinal)
            allow_during_cool_down: yes or no
        write_policy:
            allow:
            cool_down: (optinal)
            allow_during_cool_down: yes or no
            cool_down_policy: cluster or use last write only
        call_schedule:
        max_calls_per_unit: x
        unit_in_seconds: x