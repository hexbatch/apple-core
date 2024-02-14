# Remotes

remote api defined at


Remotes cannot change ownership
Remotes can be fully edited if not used anywhere in any element types or elements. They can be turned off though (things happen to the remote). Or given a redirect
Remotes deletable if the remote not used in any element or type

Remotes can be tested with a test context. When created the test context will be set used to remember stats to follow the rules of cool-down
There can be multiple test_contexts for each remote.




| Method | Path                              | Route Name                  | ToDo | Operation                                             | Args                                                                     |
|--------|-----------------------------------|-----------------------------|:-----|-------------------------------------------------------|--------------------------------------------------------------------------|
| Post   | remote                            | core.remote.create          |      | Makes a new remote                                    | Required name                                                            |
| Patch  | remote/:id/edit                   | core.remote.edit            |      | Edit part of value, if possible, sparse               | Any detail , sparse update                                               |
| Get    | remote/:id/get                    | core.remote.get             |      | returns full remote info                              | flags for detail level                                                   |
| Get    | remotes/list                      | core.remote.list            |      | searches for remotes that can use                     | iterator                                                                 |
| Get    | remote/:id/test                   | core.remote.test            |      | Sends to the Remote, returns remote activity to track | add json body for the values it draws on                                 |
| Delete | remote/:id/destroy                | core.remote.destroy         |      | Delete Remote, if the user can                        |                                                                          |
| POST   | remotes/activity/:activity/update | core.remote.activity.update |      | completes a manual waiting remote                     | json or xml or http code or headers or text                              |
| get    | remotes/activity/list/:status     | core.remote.activity.list   |      | lists activity                                        | iterator,can filter it for manual(types), activity state (or all states) |
| get    | remotes/activity/:activity/get    | core.remote.activity.get    |      | gets a remote activity                                |                                                                          |

## Data for defining a remote


        user: required
        usage_group: (optional)
        name : unique in remotes
        is_retired: default false // if true then cannot be added to element types
        is_on : if off then all read and writes will fail and the remote not called
        uri:
            uri_type: (none,url,socket,console,manual)
            uri_method (post, get, patch, put, delete)
            uri_port:
            uri_string 
            uri_to_remote_format
            uri_from_remote_format
        cache:
            is_caching: bool, if true then each last call updates the cache, and if same cache param key values then cache is used
            cache_ttl_seconds: how old the cache is allowed to be
            cache_keys: array of set of allowed keys to use for the cache comparisons, empty means each response resets the cache
        data:
            from_remote_map: array<rule to convert data from the remote to value in (attr or action)>
            to_remote_map: array<rule to convert either pre-set value, or data in (attr or action) to some part of a data format to the remote>
            is_sending_context_to_remote: bool (default false)
        call_schedule:
            rate_limit_max_per_unit: x
            rate_limit_unit_in_seconds: x
            max_concurrent_calls: default 1

# List activity 
can optionally list for status or just the single activity
can also show all remotes in system  if flag passed and the user has that admin attribute to see other remotes
